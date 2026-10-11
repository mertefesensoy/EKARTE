# EKARTE clinical knowledge model

Date: 2026-10-11. Status: design, responds to expert review ("too basic, generic examples, not usable in a working ED").

## 1. What was wrong with v0

The proposal showed the shape of the loop but no clinical substance:

- Differential states were words ("açık", "zayıfladı", "dışlandı") with no numbers behind them. A working system needs a probability per diagnosis and a defined closing threshold per diagnosis.
- Exam items were generic ("boğaz, toraks, batın"). A working system needs specific findings with a measured effect on each diagnosis, i.e. likelihood ratios where they exist.
- There was no question bank. The expert's core requirement is that the system asks detailed, discriminating questions. That requires a per-complaint bank of 30 to 60 structured questions, each tagged with the diagnoses it moves and by how much.
- Tests had no thresholds. A working system needs assay-specific cut-offs (hs-troponin by analyser), age-adjusted rules (D-dimer), and named decision rules with their published performance.
- Nothing was cited. A head physician cannot trust a rule without its source.

`docs/clinical/protokoller/gogus-agrisi.md` shows the corrected depth for one complaint. This document defines the model that holds that content for all complaints.

## 2. Knowledge objects

Everything the engine reasons over is one of seven object types. All are versioned YAML or JSON in the repository, each with `source`, `evidence_grade`, `owner`, `reviewed_at`.

### 2.1 ChiefComplaint
```yaml
id: chest_pain
tr: Göğüs ağrısı
scope: ">=18y, non-traumatic, acute <=7d"
immediate_actions: [ecg_10min, iv_monitor, bilateral_bp, troponin_t0]
diagnoses: [acs, pe, aortic_dissection, pneumothorax, tamponade, boerhaave, pericarditis, pneumonia, gerd, msk, zoster]
```

### 2.2 Diagnosis
```yaml
id: aortic_dissection
icd10: I71.0
snomed: 308546005
cant_miss: true
pretest:                      # prior probability, stratified; calibrated per hospital in Phase 1
  default: 0.003
  strata: [{age: ">=60", htn: true, p: 0.006}]
close_threshold: 0.005        # posterior below this AND exclusion_path complete → closed
exclusion_paths:
  - [addrs_le1, ddimer_lt500]           # ADvISED
  - [ct_aortography_negative]
confirmation: [ct_aortography_flap]
time_critical: true
never_closes_on: [normal_cxr, normal_troponin, symmetric_pulses]
```

### 2.3 Finding
A finding is a coded clinical fact: a history item, an exam sign, a vital sign band, an ECG pattern, a lab band, an imaging result.
```yaml
id: pain_tearing
tr: Yırtıcı / parçalayıcı ağrı
code: {snomed: 426396005}
type: history
effects:
  - {dx: aortic_dissection, lr_pos: 10.8, lr_neg: 0.95, source: klompas_2002}
  - {dx: acs, weight: qualitative_minus, source: tintinalli_9}
```
Effects are either a likelihood ratio pair (preferred, from the JAMA Rational Clinical Examination series, McGee, or the primary study) or a qualitative weight (`strong_plus`, `plus`, `minus`, `strong_minus`) mapped to conservative LR bands (3, 1.5, 0.7, 0.3) and flagged as unvalidated.

### 2.4 Question
```yaml
id: q_onset_abrupt
tr: Ağrı aniden mi başladı, saniyeler içinde en şiddetli haline mi ulaştı?
answer: yes_no
yields: {yes: [onset_abrupt], no: [onset_gradual]}
ask_if: [chest_pain]
skip_if: [addrs_known]
cost: 1          # seconds of clinician time, relative
```
Questions are chosen at run time by expected information gain over the open can't-miss diagnoses, weighted by miss cost, divided by question cost (BALAR-style selection). The clinician can always override and answer any question.

### 2.5 DecisionRule
Computable, with inputs that are findings, and an output that is a finding.
```yaml
id: perc
inputs: [age_lt50, hr_lt100, spo2_ge95, no_hemoptysis, no_estrogen, no_prior_vte, no_unilateral_leg_swelling, no_recent_surgery]
logic: all_true AND clinician_pretest_low
output: perc_negative
effect: {dx: pe, posterior_cap: 0.02, closes_with: [pretest_low]}
performance: {sens: 0.976, spec: 0.216, source: kline_2004}
```
Rules are authored in a restricted expression language and compiled to CQL (Clinical Quality Language) so they can also run inside any FHIR-capable HBYS.

### 2.6 Test
```yaml
id: hs_tnt_elecsys
loinc: 67151-1
sut_code: TBD          # Sağlık Uygulama Tebliği code, filled per hospital
turnaround_min: 60
cost_try: TBD
interpretation:
  algorithm: esc_0_1h
  cutoffs: {very_low: 5, low: 12, delta_low: 3, high: 52, delta_high: 5, unit: ng/L}
  requires: [symptom_onset_gt_3h for very_low]
```
Assay is selected at deployment; cut-offs load from the ESC table for that assay.

### 2.7 Pathway
Per can't-miss diagnosis, the ordered steps that close or confirm it, with time targets (e.g. door-to-ECG 10 min, door-to-balloon 90 min) and the actions the system keeps pinned until marked done.

## 3. Inference

1. **Prior.** Each diagnosis starts at its stratified pretest probability for the complaint.
2. **Update.** Each finding multiplies the odds of each affected diagnosis by its LR. LRs from the same study on the same diagnosis are assumed conditionally independent only when the source reports them as independent predictors; otherwise the engine uses the study's multivariable score instead of stacking LRs. Posteriors are capped to [0.001, 0.99] to prevent runaway certainty.
3. **Rules override.** When a validated rule fires (PERC negative, ESC rule-out, ADvISED negative), it caps the posterior at the rule's published failure rate regardless of stacked LRs. Rules are more trustworthy than our LR arithmetic.
4. **Closing.** A diagnosis closes when posterior < close_threshold AND at least one exclusion path is complete. "Never closes on" lists block false closures (a normal ECG never closes ACS).
5. **Next step.** Among questions, exam items and tests not yet done, pick the one with the highest (expected reduction in miss-weighted uncertainty) / (cost). Tests carry SUT cost and turnaround; questions carry seconds.
6. **Explain.** Every change in posterior is logged with the finding, the LR, and the source. The Turkish explanation is generated from that log, not from the language model's imagination.

The language model's role is limited to: parsing free text into findings (with clinician confirmation), drafting the Turkish explanation from the structured log, and answering "why" questions by citing the loaded sources. It does not decide probabilities.

## 4. Depth target per complaint

| Object | Per complaint | Ten complaints |
|---|---|---|
| Diagnoses with priors and thresholds | 8 to 15 | ~120 |
| Questions | 30 to 60 | ~450 |
| Exam findings | 15 to 30 | ~220 |
| Findings with LR evidence | 20 to 40 | ~300 |
| Decision rules | 3 to 8 | ~50 |
| Tests with interpretation | 10 to 20 | ~150 |
| ECG / imaging pattern definitions | as needed | ~60 |

The ten complaints, in order of build: chest pain, dyspnea, abdominal pain, headache, syncope, acute neurological deficit, head and neck trauma, fever and sepsis, upper GI bleeding, low back pain. Together these cover the majority of adult non-trauma ED presentations and almost all time-critical misses.

## 5. Sources, by role

Full inventory with licences in `docs/clinical/sources.md`. Roles:

- **Differential lists and red flags per complaint:** Tintinalli (symptom chapters), Rosen's (Cardinal Presentations), Mahadevan & Garmel (complaint-based), Stern "Symptom to Diagnosis".
- **Likelihood ratios for history and exam:** JAMA Rational Clinical Examination series and the Simel & Rennie book; McGee "Evidence-Based Physical Diagnosis".
- **Decision rules and thresholds:** primary derivation and validation papers; MDCalc as index (not as source); ESC, AHA/ASA, ACEP clinical policies, NICE, Surviving Sepsis.
- **Imaging choice:** ACR Appropriateness Criteria.
- **ECG patterns:** fourth universal definition of MI; Life in the Fast Lane ECG library as teaching index; primary papers for Sgarbossa, de Winter, Wellens.
- **Turkish grounding:** Ministry triage and emergency service communiqués, ATUDER and TATD guidance, Turkish translations of Tintinalli, SKRS code lists, SUT.
- **Open text for the retrieval layer (answering "why"):** StatPearls (CC BY), WikEM (CC BY-SA), NICE CKS, guideline PDFs.

Copyrighted textbooks are used as the clinicians' authoring reference, not copied into the system. What enters the knowledge base is structured facts (a finding, an LR, a threshold) with a citation, which is not a reproduction of the text.

## 6. Authoring pipeline

1. Software team drafts the complaint file from the sources above (as done for chest pain).
2. Expert reviews line by line in the markdown: accepts, edits, or strikes each row; adds Turkish practice specifics (which assay, which imaging is actually available at 03:00, which SUT codes).
3. Reviewed markdown is transcribed to YAML objects; each object carries the reviewer and date.
4. Automated checks: every LR has a source; every rule has performance and citation; every can't-miss diagnosis has at least one complete exclusion path; every test has an interpretation rule.
5. Simulation: the engine runs the complaint's synthetic case set (50 to 100 cases per complaint, written by the expert) and reports which cases closed a can't-miss diagnosis wrongly. Zero tolerance before release.
6. Versioned release; HBYS deployments pin a version.

## 7. Validation beyond simulation

- **DDXPlus** (synthetic differential-diagnosis dataset with symptom and antecedent questions, 49 pathologies) to test the question-selection engine mechanically, before any real data.
- **MIMIC-IV-ED** (de-identified US ED visits with triage, vitals, diagnoses) to test prior calibration and rule firing at scale; US case mix, so only for engine behaviour, not Turkish priors.
- **Turkish retrospective set** (Phase 1) for priors, Turkish free-text parsing, and closure safety against specialist consensus.
- **Turkish sequential set** (Phase 1b): real cases converted to step-by-step scripts, scored on misses and SUT cost.

## 8. What changes in the product

- The "zayıfladı" chip becomes a probability bar with the threshold marked and the last three findings that moved it, each with its LR and source on hover.
- The next-step panel shows why this question or test was chosen: which diagnosis it targets and the expected movement.
- Each can't-miss diagnosis shows its exclusion path as a checklist (e.g. for PE: PERC, Wells, D-dimer, CTPA) with the current position.
- The discharge rationale is generated from the structured log and cites rules by name.
- The expert's review state is visible inside the product: every rule shows "onaylayan, tarih".

## 9. Immediate asks of the expert

1. Review `gogus-agrisi.md` row by row. Mark each row: kabul / düzelt / sil.
2. State the hospital's troponin assay and D-dimer unit.
3. List what imaging and lab is available at night and on weekends, since pathways must branch on availability.
4. Write 20 real-pattern chest-pain cases (de-identified or synthetic) including at least 5 near-misses, for the simulation gate.
5. Name the next two complaints to build.
