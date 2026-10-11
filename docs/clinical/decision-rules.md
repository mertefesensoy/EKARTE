# Validated decision rules, likelihood ratios and test thresholds for ten ED chief complaints

Date: 2026-10-11. Research compendium for the EKARTE knowledge base (`knowledge-model.md`). Every number is tagged: **[v]** confirmed against a web source listed at the end; **[k]** from the primary literature as recalled and not re-verified in this pass. Treat [k] values as "probably right, check against the primary paper before shipping". Each rule or LR must be re-verified from its primary citation by the clinical authoring step before it enters a YAML object. Source disagreements are listed in the cross-cutting section near the end and must be encoded, not resolved silently.


**Legend.** **[v]** = number confirmed this session against a web source (listed in Sources). **[k]** = from the primary literature as recalled; not re-verified this session because the shared web-search budget ran out and outbound fetch/curl is blocked in this sandbox. Treat [k] values as "probably right, check before shipping." Where sources disagree I say so inline.

**Global conventions for the engine**
- Troponin in ng/L; D-dimer in ng/mL FEU (500 ng/mL FEU ≈ 250 ng/mL DDU — assays differ; store the unit with the value) [k]. Lactate mmol/L. BNP/NT-proBNP pg/mL. CRP mg/L. PCT µg/L (= ng/mL).
- LR+ > 10 or LR− < 0.1 = large shift; 5–10 / 0.1–0.2 moderate; 2–5 / 0.2–0.5 small (Jaeschke/McGee convention) [k].
- A rule intended for **rule-out** should be used only when ALL criteria are negative; never invert a rule-out rule into a rule-in.

---

## 1. CHEST PAIN

### A. Can't-miss
ACS (STEMI/NSTEMI/UA); acute aortic syndrome (dissection, IMH, PAU); pulmonary embolism; tension pneumothorax; cardiac tamponade; esophageal rupture (Boerhaave); also consider myocarditis/pericarditis, pneumonia/mediastinitis. [k, standard EM list]

### B. Decision rules

**HEART score** (Six, Backus, Kelder, Neth Heart J 2008; validation Backus, Int J Cardiol 2013) [v]
- History: highly suspicious 2 / moderately 1 / slightly-non 0. ECG: significant ST depression 2 / nonspecific repolarisation 1 / normal 0. Age: ≥65 2 / 45–64 1 / <45 0. Risk factors: ≥3 or known atherosclerotic disease 2 / 1–2 1 / none 0. Troponin: ≥3× ULN 2 / 1–3× 1 / ≤ULN 0. Range 0–10. [v]
- Derivation 2008 (122 pts): any endpoint 0–3: 2.5%; 4–6: 20.3%; ≥7: 72.7%. [v]
- Validation 2013 (2,440 pts, 10 Dutch EDs, 6-week MACE): 0–3 (36.4% of pts): 1.7% MACE; 4–6: 16.6%; 7–10: 50.1%; c-statistic 0.83 (TIMI 0.75, GRACE 0.70). Authors: low score excludes MACE with >98% certainty. [v] Sensitivity not reported in abstract.
- Pooled (Van Den Berg & Body, Eur Heart J ACC 2018): low-risk HEART sensitivity ≈96.7%, specificity ≈47% [k]. Fanaroff 2015 JAMA RCE: HEART ≤3 LR 0.20 (0.13–0.30); TIMI 0 LR 0.31 [k].
- Use: rule-out of 30-day/6-week MACE at 0–3 (with negative troponin[s]); not a rule-in.

**ESC 0 h/1 h hs-cTn algorithm** (ESC NSTE-ACS 2020, Eur Heart J 2021;42:1289, Table 5; carried into ESC ACS 2023) 
- Rule-out: 0 h "very low" (only if chest-pain onset >3 h) OR 0 h "low" AND 1 h Δ < "no 1h Δ". Rule-in: 0 h "high" OR 1 h Δ ≥ "1h Δ". Otherwise = observe zone (repeat at 3 h ± echo/CCTA).
- Assay-specific cut-offs (ng/L): 
  - **hs-cTnT Elecsys (Roche)**: very low <5; low <12; no-1h-Δ <3; high ≥52; 1h-Δ ≥5. [v: 5/12/3/≥52 confirmed via Rev Esp Cardiol summary; the Δ≥5 value appeared garbled in extraction but is the guideline value [k]]
  - **hs-cTnI Architect (Abbott)**: very low <4; low <5; no-1h-Δ <2; high ≥64; 1h-Δ ≥6. [k — search engine's own summary agreed but no document confirmed; verify against ESC Table 5]
  - Other assays [k]: Centaur 3/6/3/≥120/12; Access 4/5/4/≥50/15; Clarity 1/2/1/≥30/6; Vitros 1/2/1/≥40/4; Pathfast 3/4/3/≥90/20; TriageTrue 4/5/3/≥60/8.
  - 0 h/2 h variant [k]: Elecsys 5/14/4/≥52/10; Architect 4/6/2/≥64/15.
- Performance [k, from APACE/TRAPID/High-STEACS literature, Twerenbold JACC 2019; Boeddinghaus]: rule-out NPV ≈99.5–99.9%, sensitivity ≈99%, assigns ~55–60% to rule-out; rule-in PPV ≈70–75%; 0h hs-cTnT <5 ng/L alone → no missed NSTEMI in prospective validation [v, JACC 2018]. Rule-out is for MI, not for unstable angina.

**ADD-RS and ADvISED pathway** (Rogers, Circulation 2011; Nazerian, Circulation 2018) 
- ADD-RS: 1 point per category present (max 3). (1) High-risk conditions: Marfan/connective tissue disease, family history aortic disease, known aortic valve disease, recent aortic manipulation, known thoracic aneurysm. (2) High-risk pain: abrupt onset, severe intensity, ripping/tearing. (3) High-risk exam: pulse deficit/SBP differential, focal neuro deficit with pain, new murmur of AR with pain, hypotension/shock. [k]
- Rogers 2011 (IRAD, 2,538 pts): ADD-RS ≥1 sensitivity 95.7%; 4.3% of dissections scored 0 [k].
- ADvISED 2018: 1,850 pts, 241 (13%) AAS. D-dimer <500 ng/mL: sensitivity 96.7% (93.6–98.6), specificity 64% (61.6–66.4); 8 AAS were DD-negative overall. [v] ADD-RS ≤1 + DD-negative: sensitivity 98.8%, NPV 99.7%, LR− 0.02 (secondary report) [v]; failure 0.3% (ADD-RS 0 + DD−: 1 missed) [k]. Not externally validated in an RCT; observational. [v]
- Use: rule-out pathway (ADD-RS ≤1 AND D-dimer <500); ADD-RS 2–3 → go straight to CTA.

**Wells PE** (Wells, Thromb Haemost 2000; Ann Intern Med 2001) [k]
- Clinical signs of DVT 3; PE most likely diagnosis 3; HR >100 1.5; immobilisation ≥3 d or surgery <4 wk 1.5; previous DVT/PE 1.5; haemoptysis 1; malignancy (treated <6 mo or palliative) 1.
- Three-tier: <2 low (1.3%), 2–6 moderate (16.2%), >6 high (37.5–40.6%). Two-tier: ≤4 "PE unlikely". Unlikely + negative D-dimer: 3-month VTE 0.5% (Christopher Study, JAMA 2006, 2,206 pts). Use: pre-test stratification; "unlikely" + negative DD = rule-out.

**Revised Geneva** (Le Gal, Ann Intern Med 2006) / **Simplified** (Klok, Arch Intern Med 2008) [k]
- Age >65 1; prior DVT/PE 3; surgery/fracture <1 mo 2; active malignancy 2; unilateral limb pain 3; haemoptysis 2; HR 75–94 3; HR ≥95 5; pain on deep venous palpation + unilateral oedema 4. Low 0–3 (PE 8%), intermediate 4–10 (28%), high ≥11 (74%). Simplified: all items 1 point (HR ≥95 = 2); 0–1 low, 2–4 intermediate, ≥5 high; or ≤2 "unlikely". Fully objective (no gestalt item).

**PERC** (Kline, J Thromb Haemost 2004 derivation; 2008 validation) 
- All 8 must be negative: age <50; HR <100; SaO2 ≥95%; no haemoptysis; no oestrogen; no prior VTE; no unilateral leg swelling; no surgery/trauma requiring hospitalisation <4 wk. [v]
- Derivation (3,148 pts): sensitivity 96%, specificity 27% in low-risk [v]. Validation 2008 (8,138 pts, 12 US + 1 NZ EDs): 1,666 (20%) PERC-negative with low gestalt; 45-day VTE/death 1.0% (below 2% test threshold) [v]; overall sensitivity 97.4%, specificity 21.9% [k]. PROPER RCT (Freund, JAMA 2018): PERC strategy non-inferior, 1 missed PE (0.1%) [k].
- Use: rule-out only, and only when gestalt pre-test probability is low (<15%).

**Age-adjusted D-dimer** (ADJUST-PE, Righini, JAMA 2014) [v]
- Cut-off = age × 10 µg/L (FEU) for age >50. 3,346 pts; among those excluded by age-adjusted (but not conventional) cut-off: 1/331 (0.3%) 3-month VTE; absolute increase in negative DD 11.6% (6.4% → 29.7% in ≥75 y [k]).

**YEARS** (van der Hulle, Lancet 2017) 
- Items: clinical signs of DVT; haemoptysis; PE most likely diagnosis. 0 items → DD <1000 ng/mL excludes; ≥1 item → DD <500 excludes. [v] 3,465 pts; 48% managed without CTPA; 3-month VTE 0.61% overall / 0.43% in those managed without CT [v]; CTPA reduction 14% absolute vs Wells/500 strategy [k]. External validation (JTH 2020, 3,314 pts): 1.2% PE at initial testing in the DD-only group — caution when DD is >age-adjusted but <1000 [v]. 2024 meta-analysis (10 studies): pooled sensitivity 96%, specificity 50%, imaging RR 0.78 [v].

### C. Likelihood ratios

**ACS/AMI — Swap & Nagurney, JAMA 2005;294:2623** (history) [v for ranges; individual values k]
- Increase: radiation to right arm/shoulder LR 4.7 (1.9–12); both arms/shoulders 4.1 (2.5–6.5) [v]; exertional 2.4 (1.5–3.8); radiation to left arm 2.3 (1.7–3.1); diaphoresis 2.0 (1.9–2.2); nausea/vomiting 1.9 (1.7–2.3); worse than prior angina/similar to prior MI 1.8 (1.6–2.0); "pressure" 1.3 (1.2–1.5). Abstract range for radiation/exertion: 2.3–4.7 [v].
- Decrease: pleuritic 0.2 (0.1–0.3); positional 0.3 (0.2–0.5); sharp/stabbing 0.3 (0.2–0.5); reproducible by palpation 0.3 (0.2–0.4); inframammary location 0.8; not exertional 0.8. Abstract: stabbing/pleuritic/positional/palpation LR 0.2–0.3 [v].
- Physical exam (Panju, JAMA 1998 "Is this patient having an MI?", cited by Swap): S3 LR 3.2; hypotension (SBP ≤80) 3.1; pulmonary crackles 2.1; chest-wall tenderness LR 0.2–0.4 [k]. An older review lists radiation to both arms 7.1 and right shoulder 2.9 — do not mix with the 2005 figures [v].
- Fanaroff, JAMA 2015 update (58 studies): radiation to both arms LR 2.6 (1.8–3.7); pain similar to prior ischaemia 2.2; change in pattern over 24 h 2.0; ECG ischaemic ST depression LR ~10; HEART ≤3 LR 0.20; TIMI 0 LR 0.31 [k].

**Aortic dissection — Klompas, JAMA 2002;287:2262** [v unless noted]
- Sudden-onset pain: sensitivity 84% (80–89), LR+ 1.6, LR− 0.3 (0.2–0.5) [v].
- Tearing/ripping: LR+ 1.2–10.8 across two studies (upper value 10.8, CI 5.2–22) [v]; migrating pain LR+ 1.1–7.6 (upper 7.6, CI 3.6–16) [v].
- History of hypertension LR+ 1.6 (1.2–2.0) [k]; secondary source lists 1.5 (0.8–3.0) [v] — minor disagreement.
- Pulse/BP differential LR+ 5.7 (1.4–23) [v]; focal neurological deficit LR+ 6.6–33 [v]; diastolic murmur LR+ 1.4 (1.0–2.0), LR− 0.9 [v].
- CXR: abnormal in 90%; widened mediastinum LR+ 2.0 [k]; normal aorta/mediastinum LR− 0.3 (0.2–0.4) [v]; enlarged aorta/wide mediastinum LR+ 3.4 (2.4–4.8) in Ohle 2018 meta-analysis [v].
- Later meta-analysis (Ohle, Acad Emerg Med 2018) gives pulse deficit LR+ 2.7 (0.7–9.8) — much weaker than Klompas [v]. Conclusion of both: exam cannot rule out dissection.

**Pulmonary embolism — Chunilal, JAMA 2003;290:2849** [k]: no single symptom/sign has useful LR; Wells low/moderate/high prevalence ≈ 3–10% / 16–28% / 38–78% across studies; gestalt comparable. Kohn 2017 (Acad Emerg Med, interval LRs): at 15% pre-test, only DD <500 ng/mL brings post-test <3% [v].

### D. Test thresholds
- **STEMI (Fourth Universal Definition of MI, 2018)** [k]: new ST elevation at the J-point in 2 contiguous leads: ≥1 mm (0.1 mV) in all leads except V2–V3; V2–V3: ≥2 mm men ≥40 y, ≥2.5 mm men <40 y, ≥1.5 mm women; posterior V7–V9: ≥0.5 mm (≥1 mm men <40); right V3R–V4R: ≥0.5 mm (≥1 mm men <30). New ST depression ≥0.5 mm in 2 contiguous leads and/or T inversion ≥1 mm with prominent R = ischaemia.
- **Sgarbossa (NEJM 1996)**: concordant STE ≥1 mm = 5; concordant STD ≥1 mm V1–V3 = 3; discordant STE ≥5 mm = 2; score ≥3 → derivation spec 90%/sens 78%, validation spec 96%/sens 36% [v]; meta-analysis (Tabas 2008) spec 98%, sens 20% [v].
- **Modified Sgarbossa (Smith, Ann Emerg Med 2012)**: replace the 5-mm rule with discordant STE/S-wave ratio ≤ −0.25 (any lead; also discordant STD/R ≤ −0.30 in some versions); sensitivity 91% vs 52% (weighted) / 67% (unweighted), specificity 90% [v]. Meyers 2015 validation: sensitivity 80%, specificity 99% [v]. Barcelona algorithm (2020) [k] adds discordant ST deviation ≥1 mm in leads with R/S amplitude ≤6 mm.
- **de Winter** [k]: upsloping STD ≥1 mm at J-point V1–V6 with tall, symmetric T waves, no STE (± ≤1 mm aVR STE); ~2% of anterior LAD occlusions (de Winter, NEJM 2008). Treat as STEMI-equivalent.
- **Wellens** [k]: pain-free state, biphasic (type A, ~25%) or deep symmetric inverted (type B, ~75%) T waves V2–V3 (± V1–V4), minimal STE, preserved R; ~75% proceed to anterior MI without revascularisation (de Zwaan 1982). Critical proximal LAD stenosis.
- **Posterior MI** [k]: STD ≥0.5 mm V1–V3 with upright T/tall R (R/S >1 in V2); confirm V7–V9 STE ≥0.5 mm.
- **aVR** [k]: STE ≥1 mm in aVR with diffuse STD (≥6–8 leads) → left main/proximal LAD/3-vessel disease or severe demand ischaemia; not a STEMI-equivalent by itself (ACC 2022 chest-pain guideline).
- **Troponin** [k]: 99th-percentile URL — Elecsys hs-cTnT 14 ng/L; Architect hs-cTnI 26.2 ng/L (women 15.6, men 34.2). Delta criteria per ESC table above; for older contemporary assays, ≥20% change when baseline >URL. Chronic elevation (CKD, HF) → rely on delta.
- **D-dimer**: 500 ng/mL FEU; age × 10 if >50 (ADJUST-PE) [v]; YEARS 1000/500 [v]; for dissection, <500 ng/mL in ADD-RS ≤1 [v].

### E. Imaging (ACR Appropriateness Criteria) [k except as noted]
- Suspected acute aortic syndrome (ACR 2021): CTA chest (± abdomen/pelvis) with IV contrast — Usually Appropriate; TEE, MRA, CT chest with contrast also Usually Appropriate; CTA coronary May Be Appropriate [v].
- Suspected PE (ACR): CTPA with IV contrast — Usually Appropriate; V/Q if contrast contraindicated/pregnancy consideration; CXR first; lower-extremity US as adjunct [k].
- Acute chest pain, suspected ACS, low-intermediate risk (ACR): CXR Usually Appropriate; CCTA Usually Appropriate for low-intermediate risk with negative/indeterminate biomarkers [k]. Bedside echo for tamponade/wall motion; CXR for pneumothorax (POCUS more sensitive) [k].

---

## 2. DYSPNEA

### A. Can't-miss
PE; ACS; acute decompensated HF/flash pulmonary oedema; tension pneumothorax; cardiac tamponade; anaphylaxis/upper-airway obstruction; severe asthma/COPD with impending failure; pneumonia with sepsis; DKA/metabolic acidosis (Kussmaul); CO/cyanide poisoning. [k]

### B. Decision rules
- PE rules: Wells, Geneva, PERC, YEARS, age-adjusted DD — see §1B.
- **CURB-65** (Lim, Thorax 2003) [v]: Confusion (new); Urea >7 mmol/L (BUN >19 mg/dL); RR ≥30; BP SBP <90 or DBP ≤60; Age ≥65 — 1 point each. 30-day mortality derivation: 0: 0.7%; 1: 3.2%; 2: 13.0% [k — one extracted snippet read "3%", almost certainly truncated]; 3: 17%; 4: 41.5%; 5: 57% [v]. Grouped: 0–1 low (≈1.5%) outpatient; 2 (≈9.2%) consider admission; ≥3 (≈22%) severe/ICU consideration [v]. Use: prognosis/disposition, not diagnosis. CRB-65 for no labs.
- **NEWS2** (RCP 2017) [k]: RR, SpO2 (scale 2 for hypercapnic COPD), supplemental O2 (+2), SBP, HR, consciousness (ACVPU; new confusion scores 3), temperature. Aggregate 0–4 low; 3 in any single parameter low-medium (urgent review); 5–6 medium (urgent clinical response); ≥7 high (emergency response). SSC 2021 prefers NEWS/MEWS/SIRS over qSOFA alone for screening [k].
- qSOFA/SIRS: see §8.

### C. Likelihood ratios
**Heart failure — Wang, JAMA 2005;294:1944** (ED dyspnea) 
- History of HF LR+ 5.8 [v]; S3 LR+ 11 (4.9–25) [v]; CXR pulmonary venous congestion LR+ 12 [v]; interstitial oedema 12; cardiomegaly 3.3; JVD 5.1; hepatojugular reflux 6.4; rales 2.8; leg oedema 2.3; AF on ECG 3.8; any ECG abnormality LR− 0.64 [k except where marked].
- BNP <100 pg/mL LR− 0.11 (0.07–0.16) [v]; absence of prior HF, DOE, rales, cardiomegaly, any ECG abnormality LR− 0.33–0.64 [v]. Clinical gestalt LR+ 4.4, LR− 0.45 [k].

**Pneumonia — Metlay, JAMA 1997;278:1440** 
- Egophony LR+ 2.0–8.6 across studies (one summary 5.3) [v: 5.3; range k]; bronchial breath sounds LR+ 3.5; dullness 2.2–4.3; crackles 1.6–2.7 [v]; rhonchi, decreased breath sounds 1.5–3.5 range [v]; fever/tachycardia/tachypnoea LR+ 1.5–2.4 [v]; absence of any vital-sign abnormality LR− 0.18 [v]; absence of all vital-sign + auscultatory abnormalities substantially lowers probability (authors: may obviate CXR) [v]. Heckerling rule (T >37.8, HR >100, crackles, ↓breath sounds, no asthma): 0–1 → ~1%; all 5 → ~50% at 5% prevalence [v].
- Ebell 2020 meta-analysis (Acad Emerg Med): egophony LR+ 6.17 (1.34–18); dullness 2.62; no vital-sign abnormality LR− 0.25 [v].

### D. Test thresholds
- **BNP** (Maisel, NEJM 2002, 1,586 pts): 100 pg/mL — sensitivity 90%, specificity 76%; <100 rule-out, >400 likely HF, 100–400 grey zone [k]. Obesity lowers BNP; renal failure, AF, age raise it.
- **NT-proBNP** (ICON, Januzzi Eur Heart J 2006; ICON-RELOADED, JACC 2018): rule-out <300 pg/mL (sens 93.9%, NPV 98.0%) [v]; rule-in age-stratified 450 (<50 y), 900 (50–75 y), 1,800 (>75 y): sensitivity 85.7/79.3/75.9%, specificity 93.9/84.0/75.0% [v]. FDA-labelled outpatient cut-offs 125 (<75 y) / 450 (≥75 y) are different [v].
- Lactate, PCT, CRP — see §8. SpO2 <90–92% / PaO2 <60 mmHg = hypoxaemia; PaCO2 >45 with pH <7.35 = acute hypercapnic failure; PEF <50% predicted severe asthma [k].

### E. Imaging [k]
- ACR Acute Respiratory Illness (immunocompetent): CXR Usually Appropriate when ≥1 of age ≥40, dementia, abnormal vitals/exam, haemoptysis, immunocompromise, comorbidity; CT chest May Be Appropriate for complicated/unresolving. Dyspnea–suspected cardiac origin: CXR + TTE Usually Appropriate. Lung POCUS (B-lines) for pulmonary oedema and pneumothorax has high accuracy (B-lines sens ~85–94%, spec ~92%) [k].

---

## 3. ACUTE ABDOMINAL PAIN

### A. Can't-miss
Ruptured/symptomatic AAA; acute mesenteric ischaemia; perforated viscus; bowel obstruction with strangulation/volvulus; ectopic pregnancy; appendicitis; acute cholangitis; severe acute pancreatitis; testicular/ovarian torsion; inferior MI; aortic dissection; DKA; incarcerated hernia; toxic megacolon. [k]

### B. Decision rules
**Alvarado (MANTRELS)** (Alvarado 1986) [v/k]: Migration 1, Anorexia 1, Nausea/vomiting 1, RLQ Tenderness 2, Rebound 1, Elevated temp (≥37.3) 1, Leukocytosis (>10) 2, Shift left 1. Max 10. Ohle 2011 (BMC Med, 42 studies): cut-off <5 rules out — sensitivity 99% overall (96% men, 99% women, 99% children) [v]; cut-off ≥7 performs poorly for rule-in — specificity 81% overall (men 57%, women 73%, children 76%) [v]; over-predicts in women and children [v]. Specificity at cut-off 5 ≈ 43% [k, not confirmed].

**Adult Appendicitis Score (AAS)** (Sammalkorpi, BMC Gastroenterol 2014; 829 pts, 47% appendicitis) [v: structure/bands; point table k]
- Pain in RLQ 2; pain relocation 2; RLQ tenderness: women 16–49 y 1, all others 3; guarding: mild 2, moderate/severe 4; WBC (×10⁹/L): ≥7.2 <10.9: 1; ≥10.9 <14: 2; ≥14: 3; neutrophils %: ≥62 <75: 2; ≥75 <83: 3; ≥83: 4; CRP (mg/L) symptoms <24 h: ≥4 <11: 2; ≥11 <25: 3; ≥25 <83: 5; ≥83: 1; symptoms >24 h: ≥12 <53: 2; ≥53 <152: 2; ≥152: 1. Max 23. [k]
- Bands: ≤10 low, 11–15 intermediate, ≥16 high [v]. 2014: high group specificity 93% [v]; AUC 0.882 [k]; implementation study 2017: 7% appendicitis in low-risk group [v]. External validation (Tahir): >11 sens 100%/spec 55.6%; >16 sens 79.1%/spec 77.8% [v].

**AIR score** (Andersson, World J Surg 2008) [k; bands v]: vomiting 1; RIF pain 1; rebound/muscular defence light 1 / medium 2 / strong 3; temp ≥38.5 1; PMN 70–84% 1, ≥85% 2; WBC 10–14.9 1, ≥15 2; CRP 10–49 1, ≥50 2. Max 12. 0–4 low, 5–8 indeterminate, 9–12 high. Derivation AUC 0.97 vs Alvarado 0.92 [k]; AIR >4 vs Alvarado: sensitivity 89.9 vs 78.6%, specificity 63.6 vs 54.5% in one comparison [v]; validation AUC 0.836 [v].

**Ranson** (1974) [k]: admission — age >55, WBC >16k, glucose >200 mg/dL, LDH >350 IU/L, AST >250 IU/L; 48 h — Hct fall >10%, BUN rise >5 mg/dL, Ca <8 mg/dL, PaO2 <60, base deficit >4, fluid sequestration >6 L. Mortality 0–2: ~1–3%; 3–4: ~15%; 5–6: ~40%; ≥7: near 100%. Requires 48 h.
**BISAP** (Wu, Gut 2008; 17,992 derivation/18,256 validation) [v: items; mortality k]: BUN >25 mg/dL, impaired mental status, SIRS ≥2, age >60, pleural effusion — 1 each, within 24 h. Mortality <1% at 0–1, ~2% at 2, >20% at highest scores [v]; commonly tabulated 3: 5–8%, 4: 13–19%, 5: 22% [k, not confirmed]. BISAP ≥3 for mortality: pooled sensitivity 56%, specificity 91% [v].

**Kocher criteria** (paediatric septic hip; JBJS 1999) [k]: non-weight-bearing, ESR ≥40 mm/h, fever >38.5 °C, WBC >12,000. Predicted probability 0: <0.2%; 1: 3%; 2: 40%; 3: 93.1%; 4: 99.6%. Validation 2004: 2.0/9.5/35/72.8/93%. Caird 2006 adds CRP >2.0 mg/dL (strongest single predictor).

### C. Likelihood ratios
**Appendicitis — Wagner, JAMA 1996;276:1589** [v where marked]
- RLQ pain LR+ 7.31–8.46, LR− 0–0.28 [v]; rigidity LR+ 3.76 (AAFP table 3.8) [v]; migration LR+ 3.18 (2.41–4.21), LR− 0.50 (0.42–0.59) [v]; pain before vomiting LR+ 2.76 [k]; psoas sign 2.38 [k]; fever 1.94 [k]; rebound 1.1–6.3 [k]; guarding 1.65–1.78 [k]; rectal tenderness 0.83–5.34 [k]; anorexia 1.27 [k]; nausea 0.69–1.2 [k]; vomiting 0.92 [k]. No fever LR− 0.32; no guarding 0–0.54; no migration 0.5 [k]. Caveat: a JAMA letter notes internal inconsistencies between the paper's Table 3 sens/spec and its LRs; a 2008 AAFP table gives rigidity LR+ 1.59 [v]. Children (Bundy, JAMA 2007): migration LR 1.9–3.1; RLQ pain 1.2; rebound 3.0 [v].

**Cholecystitis — Trowbridge, JAMA 2003;289:80** [v]: Murphy sign LR+ 2.8 (0.8–8.6); RUQ tenderness LR− 0.4 (0.2–1.1); no finding or lab (WBC, LFTs) establishes or excludes; → RUQ US. Sonographic Murphy + stones: LR+ ≈ 2.7–4 [k].

**Small-bowel obstruction** (McGee, Evidence-Based Physical Diagnosis; Böhner, Eur J Surg 1998) [k]: visible peristalsis LR+ 18.8; abdominal distension LR+ 5.6–9.6, LR− 0.4; hyperactive bowel sounds LR+ 5.0; prior abdominal surgery LR+ ~3; constipation 2.5–8.8; vomiting ~1.5. Taylor & Lalani 2013 (Acad Emerg Med): CT LR+ 3.6, LR− 0.18; US (bedside) LR+ 9.5, LR− 0.04 [k]. Gottlieb 2018 US meta-analysis: sens 92.4%, spec 96.6%, LR+ 27.5, LR− 0.08 [v].

**AAA — Lederle & Simel, JAMA 1999** [k]: palpation sensitivity 68% overall (29% for 3.0–3.9 cm, 50% 4.0–4.9, 76% ≥5 cm), specificity 75%; LR+ for ≥4 cm 15.6, LR− 0.51. Absence of palpable mass does not exclude. POCUS for AAA sens ~99%, spec ~98%.

**Mesenteric ischaemia** (Cudnik, Acad Emerg Med 2013 meta-analysis) [k]: lactate sens 86%, spec 44%; D-dimer sens 96%, spec 40% (LR− ~0.1); CTA sens 94%, spec 95%.

### D. Test thresholds [k]
- Lipase ≥3× ULN (revised Atlanta 2012: 2 of 3 — typical pain, lipase/amylase ≥3× ULN, imaging). Degree of elevation ≠ severity. 
- Lactate >2 mmol/L concerning; >4 high mortality; normal lactate does not exclude early mesenteric ischaemia.
- WBC: LR+ ~1.5–2 for >10–12k in appendicitis; CRP + WBC both normal → appendicitis unlikely (LR− ~0.1 combined in some series).
- Urine/serum hCG in all women of reproductive age; discriminatory zone β-hCG ~1,500–3,500 mIU/mL for TVUS.
- TG18 cholangitis: systemic inflammation (fever/WBC/CRP) + cholestasis (bili ≥2 mg/dL or ALP/GGT/AST/ALT >1.5× ULN) + imaging (dilatation/stone); TG18 cholecystitis: local signs + systemic signs + imaging.
- ALT >150 U/L (3× ULN) LR+ ~10 for choledocholithiasis.

### E. Imaging (ACR) 
- RLQ pain/suspected appendicitis (ACR 2018): CT abdomen/pelvis with IV contrast Usually Appropriate; CT without contrast and US May Be Appropriate; pregnancy: US Usually Appropriate, then MRI without contrast [v]. Children: US first (graded compression), MRI/CT if equivocal [k].
- RUQ pain (ACR 2018): US abdomen Usually Appropriate first; HIDA if US equivocal; CT/MRCP for complications [k].
- Acute nonlocalised abdominal pain (ACR): CT abdomen/pelvis with IV contrast Usually Appropriate; non-contrast May Be Appropriate; US for RUQ/pelvic or pregnancy [k].
- Suspected SBO (ACR 2019): CT abdomen/pelvis with IV contrast Usually Appropriate; radiographs May Be Appropriate (low sensitivity) [k].
- LLQ/suspected diverticulitis: CT with IV contrast [k]. Suspected AAA rupture: POCUS → CTA abdomen/pelvis [k]. Suspected mesenteric ischaemia: CTA abdomen/pelvis [k]. Pancreatitis: CT not needed in first 48–72 h unless diagnosis unclear/deterioration; US for gallstones [k].

---

## 4. HEADACHE

### A. Can't-miss
Subarachnoid haemorrhage; bacterial meningitis/encephalitis; cerebral venous sinus thrombosis; cervical artery dissection; intracerebral/subdural haemorrhage; giant cell arteritis; acute angle-closure glaucoma; CO poisoning; hypertensive emergency/PRES; pituitary apoplexy; idiopathic intracranial hypertension with vision threat; mass with herniation; pre-eclampsia. [k]

### B. Decision rules
**Ottawa SAH Rule** (Perry, JAMA 2013 derivation; CMAJ 2017 validation) 
- Apply to alert (GCS 15) patients >15 y with new severe non-traumatic headache peaking within 1 h, presenting ≤14 days; exclude new neuro deficit, prior aneurysm/SAH/tumour, recurrent similar headaches (≥3 over ≥6 months) [k].
- Investigate if ANY: age ≥40; neck pain or stiffness; witnessed LOC; onset during exertion [v]; thunderclap (instantly peaking) headache; limited neck flexion on exam [k].
- Derivation (2,131 pts, 132 SAH): sensitivity 100%, specificity 15.3% [k]. Validation 2017 (1,153 pts, 67 SAH, 6 EDs): sensitivity 100% (94–100), specificity 13.6% (13.1–15.8), NPV 100% [v]. Use: rule-out only; very low specificity.
- SNNOOP10 red-flag list (Do 2019) for secondary headache screening [k].

### C. Likelihood ratios
**SAH — Carpenter, Acad Emerg Med 2016;23:963** (22 studies, prevalence 7.5%) [v]: neck pain (history) LR+ 4.1 (2.2–7.6); neck stiffness (exam) LR+ 6.6 (4.0–11.0); onset over >1 h LR− 0.06 (0–0.95); no physical finding has a useful LR−; non-contrast CT ≤6 h LR+ 230, LR− 0.01 (0–0.04); CT >6 h LR− 0.07 (0.01–0.61); Ottawa rule LR− 0.02, LR+ 1.17 [v]. Perry 2011 (BMJ): CT within 6 h on modern scanner read by neuroradiologist sensitivity 100% (97–100) [k].
**Meningitis — Attia, JAMA 1999;282:175** [v]: fever, neck stiffness, altered mental status — ≥1 present in 99–100% (absence of all three essentially excludes); jolt accentuation sensitivity 100%, specificity 54%, LR+ 2.2, LR− 0 (single study; later studies found much lower sensitivity, ~21–64%) [v/k]; Kernig/Brudzinski: sensitivity ~5%, specificity ~95% (Thomas 2002) — not useful for exclusion [v].
**Temporal arteritis — Smetana & Shmerling, JAMA 2002;287:92** [v]: jaw claudication LR+ 4.2 (2.8–6.2); diplopia 3.4 (1.3–8.6); beaded temporal artery 4.6 (1.1–18.4); prominent/enlarged TA 4.3 (2.1–8.9); tender TA 2.6 (1.9–3.7); absent TA pulse 2.7 [v]; scalp tenderness 1.6; synovitis LR 0.41 [v]; any TA abnormality ~2.0 [v]; ESR >100 LR+ 2.5 (0.7–8.3), sensitivity 39% [v]; normal ESR LR 0.2 [k, not confirmed]. Verification bias (biopsy-referred cohorts).

### D. Test thresholds [k]
- CT head non-contrast within 6 h of onset → SAH excluded (see LRs); >6 h → LP or CTA.
- LP (Perry, BMJ 2015): RBC <2,000 ×10⁶/L AND no xanthochromia excludes aneurysmal SAH (sensitivity 100%); xanthochromia reliable ≥12 h.
- Bacterial meningitis CSF: opening pressure >20 cmH2O; WBC >1,000/µL neutrophilic (bacterial likely if >500 with >80% PMN); protein >100 mg/dL; glucose <40 mg/dL or CSF:serum <0.4; CSF lactate ≥3.5 mmol/L (LR+ high); PCT serum >0.5 ng/mL favours bacterial.
- GCA: ESR ≥50 mm/h (ACR 1990 criterion); CRP >2.45 mg/dL sensitivity 86% (Kermani 2012); both normal → GCA unlikely (~1–4%); start steroids before biopsy.
- Angle closure: IOP >21 mmHg (typically >40). CO: COHb >3% non-smoker / >10% smoker.

### E. Imaging (ACR Headache 2019) [k]
- Sudden severe (thunderclap) headache: CT head without contrast Usually Appropriate; CTA head (± neck) Usually Appropriate as next step/with CT; MRI/MRA alternatives.
- New headache with red flags (immunocompromise, cancer, pregnancy, age >50, focal deficit, papilloedema): MRI brain with and without contrast Usually Appropriate; CT if MRI unavailable.
- Suspected CVST: CT venography or MR venography. Suspected dissection: CTA neck. Chronic/primary headache with normal exam: no imaging.

---

## 5. SYNCOPE

### A. Can't-miss
Arrhythmia (VT, high-grade AV block/sick sinus, long/short QT, Brugada, WPW, ARVC, HCM); structural (aortic stenosis, HCM, tamponade, myxoma); PE; aortic dissection; ruptured AAA; ectopic pregnancy; occult GI bleed/haemorrhage; SAH; ACS; severe hyperkalaemia/drug toxicity. [k]

### B. Decision rules
**San Francisco Syncope Rule (CHESS)** (Quinn, Ann Emerg Med 2004/2006) [v]: CHF history; Hct <30%; ECG abnormal (any new change or non-sinus rhythm); SOB; SBP <90 at triage. Any → high risk for 7-day serious outcome. Derivation (684 pts): sens 96% (92–100), spec 62% [v]; validation 2006 (760–791 pts, same centre): sens 98% (89–100), spec 56–58% [v]. Independent meta-analysis (Saccilotto, CMAJ 2011, 18 studies): sens 86% (83–89), spec 49% [v] — external performance notably worse; ECG interpretation variability. Use: rule-out, with caution.

**Canadian Syncope Risk Score** (Thiruganasambandamoorthy, CMAJ 2016 derivation 4,030 pts; JAMA Intern Med 2020 validation 3,819 pts) 
- Items: predisposition to vasovagal symptoms −1; history of heart disease +1; SBP <90 or >180 (any ED reading) +2; troponin >99th percentile +2; abnormal QRS axis (<−30° or >100°) +1; QRS >130 ms +1; QTc >480 ms +2; ED diagnosis vasovagal −2; ED diagnosis cardiac syncope +2. Range −3 to +11. [v]
- Categories (derivation 30-day serious outcome): very low −3 to −2: 0.4%; low −1 to 0: 1.2%; medium 1–3: 3.2%; high 4–5: 8.1%; very high 6–11: 25.7% [k; 0.4% and 1.2% confirmed, bands partly disputed by secondary sources that use −3 to 0 as very low]. Validation 2020: ≤1% in very-low/low; ~20% high; ~50% very high [v].
- Use: risk stratification for 30-day SAE; very-low/low → discharge; requires ED physician diagnosis input.
- Also EGSYS (cardiac syncope; ≥3 → high), OESIL [k].

### C. Likelihood ratios (Albassam, JAMA 2019 "Did this patient have cardiac syncope?") [k, not verified]: age >35 LR+ 3.3 (2.3–4.9); history of AF/flutter LR+ 7.3; known severe structural heart disease LR+ 3.3; syncope while supine LR+ ~2.6? (uncertain); prodrome of nausea/warmth/diaphoresis and triggers (pain, prolonged standing) reduce cardiac probability (LR ~0.2–0.4); CSRS very-low/low and EGSYS <3 had the best LR− (~0.1). Treat as placeholders until checked.

### D. Test thresholds [k]
- ECG red flags: QTc >480–500 ms (or <340); Brugada type 1 (coved STE ≥2 mm V1–V2); WPW (PR <120 ms + delta); Mobitz II or 3rd-degree block; bifascicular block + 1st-degree AV block; sinus brady <40 awake; pauses >3 s; VT/NSVT; LVH with HCM pattern; epsilon waves/T inversion V1–V3 (ARVC); S1Q3T3/RV strain (PE); ischaemia.
- Orthostatic hypotension: drop SBP ≥20 or DBP ≥10 mmHg within 3 min standing (or SBP <90).
- Troponin >99th percentile; Hb; glucose; hCG; lactate; D-dimer only if PE suspected (PESIT: 17% PE among first-syncope admissions — contested).

### E. Imaging (ACR Syncope 2020) [k]: no imaging routinely; CT head Usually Not Appropriate without focal deficit/trauma/headache; TTE Usually Appropriate when cardiac cause suspected or murmur/abnormal ECG; CTA/V-Q for suspected PE; CTA chest for suspected dissection.

---

## 6. ACUTE NEUROLOGICAL DEFICIT / ALTERED MENTAL STATUS

### A. Can't-miss
Ischaemic stroke (incl. basilar occlusion, LVO); intracerebral haemorrhage; SAH; hypoglycaemia; status epilepticus incl. non-convulsive; meningitis/encephalitis (HSV); Wernicke; hypertensive encephalopathy/PRES; toxic (opioids, anticholinergic, serotonin, NMS, CO); sepsis-associated encephalopathy; hyponatraemia/hypercalcaemia; hepatic/uraemic encephalopathy; cervical artery dissection; CVST; epidural/subdural haematoma; Todd paralysis; hypothyroid/myxoedema; thyroid storm. [k]

### B. Rules/scales
- **NIHSS** (Brott 1989) [k]: 15 items, 0–42 (LOC ×3, gaze, visual fields, facial palsy, motor arm ×2, motor leg ×2, ataxia, sensory, language, dysarthria, extinction). 0 none; 1–4 minor; 5–15 moderate; 16–20 moderate-severe; 21–42 severe. NIHSS ≥6 typical threshold for thrombectomy eligibility; underestimates posterior-circulation stroke.
- **BE-FAST** (Aroor, Stroke 2017) [v]: Balance, Eyes (vision loss/diplopia), Face, Arm, Speech, Time. FAST missed 14.1% of 736 ischaemic strokes; BE-FAST missed 4.4% (P<0.0001); retrospective single centre.
- Cincinnati (facial droop, arm drift, speech): any 1 → see Goldstein LRs below [k]. LVO prehospital scales: RACE ≥5, LAMS ≥4, VAN positive, FAST-ED ≥4 (sens ~0.7–0.85, spec ~0.7–0.9) [k].
- **ABCD²** (Johnston, Lancet 2007) [k]: Age ≥60 1; BP ≥140/90 1; Clinical: unilateral weakness 2, speech disturbance 1; Duration ≥60 min 2, 10–59 min 1; Diabetes 1. 2-day stroke risk 0–3: 1.0%; 4–5: 4.1%; 6–7: 8.1%. Superseded for disposition by rapid imaging pathways.
- GCS (E4 V5 M6); FOUR score for intubated [k].

### C. Likelihood ratios
**Stroke — Goldstein & Simel, JAMA 2005;293:2391** [v]: in patients with neurologically relevant symptoms (prior ~10%), presence of ≥1 of facial paresis, arm drift, abnormal speech LR+ 5.5 (3.3–9.1); absence of all three LR 0.39 (0.25–0.61). Early-mortality predictors: impaired consciousness, hemiplegia, conjugate gaze palsy ≥1 LR 1.8 (1.2–2.8) [v].
**Meningitis** — Attia 1999 (see §4C).
**Stroke mimic predictors** [k]: seizure at onset, glucose <50, known cognitive impairment, migraine history; FABS score.

### D. Test thresholds [k]
- Point-of-care glucose first (hypoglycaemia <70 mg/dL; treat if <50–60 with symptoms).
- IV thrombolysis window ≤4.5 h from last-known-well; BP must be <185/110 before and <180/105 after; glucose 50–400 mg/dL; INR ≤1.7; platelets ≥100k; no DOAC within 48 h (unless specific assays normal). Thrombectomy: LVO (ICA/M1 ± M2, basilar) up to 6 h with ASPECTS ≥6; 6–24 h with DAWN/DEFUSE-3 perfusion criteria (core <70 mL, mismatch ratio ≥1.8, mismatch volume ≥15 mL).
- ICH: BP target SBP 140 (not <130) (INTERACT/ATACH-2); reverse anticoagulation (PCC + vitamin K for warfarin, idarucizumab/andexanet).
- Sodium <120 mmol/L or rapid fall → symptomatic; correct ≤8–10 mmol/L/24 h. Ammonia elevated but poorly correlated with grade. CO: COHb. Thiamine 500 mg IV before glucose if Wernicke risk. NCSE: EEG; after convulsive status consider if no recovery at 20–30 min.

### E. Imaging (ACR Cerebrovascular Disease–Stroke and Stroke-Related Conditions 2021; ACR Altered Mental Status) [k]
- Acute neuro deficit/suspected stroke: non-contrast CT head immediately (Usually Appropriate) PLUS CTA head and neck (Usually Appropriate) for LVO; CT perfusion or MRI-DWI/perfusion for 6–24 h window; MRI brain without contrast (DWI) Usually Appropriate for TIA/resolved deficit.
- Acute AMS with no identified metabolic/toxic cause, focal deficit, trauma, anticoagulation, or age >65: CT head without contrast Usually Appropriate; MRI with/without contrast if encephalitis/CVST suspected (MRV/CTV).

---

## 7. MINOR HEAD AND CERVICAL TRAUMA

### A. Can't-miss
Epidural/subdural/subarachnoid haemorrhage and contusion requiring neurosurgery; depressed or basilar skull fracture; delayed bleeding in anticoagulated/antiplatelet patients; unstable cervical-spine fracture or ligamentous injury; spinal cord injury (central cord); blunt cerebrovascular injury (carotid/vertebral dissection); occult cause of fall (syncope, seizure). [k]

### B. Decision rules
**Canadian CT Head Rule** (Stiell, Lancet 2001; validation JAMA 2005) 
- Inclusion: GCS 13–15, witnessed LOC, definite amnesia or disorientation, injury <24 h; excludes age <16, anticoagulation/bleeding disorder, seizure, obvious open/depressed skull fracture, focal deficit, unstable vitals [k].
- High risk (need for neurosurgery): GCS <15 at 2 h; suspected open/depressed skull fracture; any sign of basal skull fracture (haemotympanum, raccoon eyes, Battle sign, CSF oto/rhinorrhoea); ≥2 episodes of vomiting; age ≥65. Medium risk (clinically important brain injury): amnesia before impact ≥30 min; dangerous mechanism (pedestrian struck, ejected, fall ≥3 ft/5 stairs). [v — note source wording varies: "vomiting ≥2 episodes", "age ≥65"]
- 3,121 pts: high-risk factors sensitivity 100% (92–100) for neurosurgical intervention, specificity 68.7%, CT in 32%; all 7 factors sensitivity 98.4% (96–99) for clinically important injury, specificity 49.6% [v].
- **New Orleans Criteria** (Haydel, NEJM 2000) for GCS 15: headache, vomiting, age >60, intoxication, persistent anterograde amnesia, visible trauma above clavicles, seizure; sensitivity 100% for CT abnormality, specificity ~25%; head-to-head CCHR 100%/50.6% vs NOC 100%/12.7% (Stiell 2005) [k].
- Easter 2015 RCE: all CCHR features absent → 0.31% probability of severe injury; all NOC absent → 0.61% [v].

**PECARN** (Kuppermann, Lancet 2009; 42,412 children, GCS 14–15, <24 h) [v]
- <2 y: GCS ≤14, palpable skull fracture, or altered mental status → CT (ciTBI 4.4%); occipital/parietal/temporal scalp haematoma, LOC ≥5 s, severe mechanism, or not acting normally per parent → observation vs CT (0.9%); none → ciTBI 0.02% [k for the rates; criteria v].
- ≥2 y: GCS ≤14, signs of basilar skull fracture, or AMS → CT (4.3%); any LOC, vomiting, severe headache, severe mechanism → obs vs CT (0.9%); none → <0.05% [k rates].
- Validation: <2 y sensitivity 100% (86.3–100), NPV 100% (99.7–100); ≥2 y sensitivity 96.8% (89.0–99.6), specificity 58.2%, NPV 99.95% (99.81–99.99) [v].

**NEXUS** (Hoffman, NEJM 2000; 34,069 pts, 21 centres) [v]: no imaging if ALL — no midline cervical tenderness; no focal neuro deficit; normal alertness; no intoxication; no painful distracting injury. Sensitivity 99.6% (98.6–100), specificity 12.9%, NPV 99.9% [v]. Lower sensitivity in elderly in later series [k].

**Canadian C-Spine Rule** (Stiell, JAMA 2001; 8,924 pts; NEJM 2003 comparison) 
- Alert (GCS 15), stable trauma. (1) Any high-risk factor → image: age ≥65, dangerous mechanism (fall ≥3 ft/5 stairs, axial load, MVC >100 km/h/rollover/ejection, motorised recreational vehicle, bicycle collision), paraesthesias in extremities. (2) Any low-risk factor allowing safe ROM assessment? simple rear-end MVC, sitting in ED, ambulatory at any time, delayed-onset neck pain, absence of midline tenderness — if none → image. (3) Able to actively rotate 45° left and right → no imaging. [k]
- 2001: sensitivity 100% (98–100), specificity 42.5% [v]; 2003 head-to-head (8,283 pts): CCR 99.4% vs NEXUS 90.7% sensitivity; specificity 45.1% vs 36.8% [v].

**Ottawa Ankle/Foot Rules** (Stiell 1992–1995; Bachmann, BMJ 2003 meta-analysis) [v]: ankle radiograph if malleolar-zone pain AND (bone tenderness posterior edge/tip distal 6 cm lateral or medial malleolus OR inability to bear weight 4 steps immediately and in ED); foot series if midfoot pain AND (tenderness base of 5th metatarsal or navicular OR inability to bear weight). 27 studies/15,581 pts: pooled LR− 0.08 ankle, 0.08 midfoot, 0.07 children; sensitivity ≈ 100% (often quoted 97.6–99.4%), reduces radiographs 30–40% [v]. 
**Ottawa Knee Rule** (Stiell, JAMA 1996; Bachmann, Ann Emerg Med 2004) [k]: radiograph if age ≥55, isolated patellar tenderness, fibular-head tenderness, inability to flex to 90°, or inability to bear weight 4 steps immediately and in ED. Pooled (6 studies, 4,249 adults): sensitivity 98.5% (93–100), specificity 48.6%, LR− 0.05.

### C. Likelihood ratios — Easter, JAMA 2015;314:2672 (adult minor head trauma, GCS 13–15; 23,079 pts; prevalence severe injury 7.1%, death/neurosurgery 0.9%) [v]: signs of skull fracture LR+ 16 (3.1–59); GCS 13 LR+ 4.9 (2.8–8.5); any GCS decline LR 3.4–16; ≥2 vomiting episodes LR+ 3.6 (3.1–4.1); pedestrian struck LR 3.0–4.3. Age, headache, LOC alone have LRs near 1 [k].

### D. Test thresholds [k]
- GCS ≤13 = moderate TBI (not "minor"); repeat GCS at 2 h is a CCHR criterion.
- Anticoagulated/antiplatelet patients: CT regardless of rules (ACEP 2023, NICE CG176 recommends CT within 8 h for warfarin); delayed-bleed rate ~0.5–1% → consider observation/repeat CT only if symptoms.
- S100B <0.10 µg/L within 6 h of injury (Scandinavian guideline 2013; Undén): sensitivity ~97–99% for CT abnormality; can avoid CT in low-risk adults.
- Cervical CT negative + persistent neuro deficit or obtunded → MRI; BCVI screening (Denver criteria: seatbelt sign/neck haematoma, LeFort II/III, C-spine fracture C1–C3/foramen transversarium/subluxation, GCS <8 with mechanism) → CTA neck.

### E. Imaging (ACR Head Trauma 2020; ACR Suspected Spine Trauma 2018) [k]
- Minor head trauma meeting CCHR/NOC/PECARN risk criteria: CT head without contrast Usually Appropriate; skull radiographs Usually Not Appropriate; MRI for persistent symptoms/suspected DAI later.
- Adult cervical trauma meeting NEXUS/CCR imaging criteria: CT cervical spine without contrast Usually Appropriate; plain radiographs Usually Not Appropriate (adults); MRI for neuro deficit/obtunded with negative CT; CTA neck for BCVI criteria. Children <14: radiographs often first; CT selective.

---

## 8. FEVER AND SUSPECTED SEPSIS

### A. Can't-miss
Sepsis/septic shock (any source); bacterial meningitis/encephalitis; necrotising soft-tissue infection; infective endocarditis; spinal epidural abscess; febrile neutropenia; toxic shock syndrome; acute cholangitis; malaria/travel infections; thyroid storm; NMS/serotonin syndrome/heat stroke; peritonsillar/retropharyngeal/epiglottitis airway infections; toxic megacolon. [k]

### B. Decision rules
- **qSOFA** (Seymour, JAMA 2016) [v]: RR ≥22; altered mentation (GCS <15); SBP ≤100 — ≥2 = positive. Outside ICU (~66,500–148,907 encounters, in-hospital mortality ~3%): AUROC 0.81 vs SOFA 0.79 vs SIRS 0.76 [v]; ED cohort AUROC 0.80 vs SIRS 0.65 [v]; ICU: SOFA 0.753 vs qSOFA 0.607 vs SIRS 0.589 [v]. Pooled (Fernando, Ann Intern Med 2018): qSOFA sensitivity 60.8%, specificity 72.0%; SIRS sensitivity 88.1%, specificity 25.8% [k]. SSC 2021: recommend AGAINST qSOFA as the sole screening tool (prognostic, low sensitivity) [k].
- **SIRS** (1992) [k]: temp >38 or <36 °C; HR >90; RR >20 or PaCO2 <32 mmHg; WBC >12k or <4k or >10% bands. ≥2 = SIRS. Sensitive, non-specific (~1 in 8 ICU sepsis patients SIRS-negative — Kaukonen NEJM 2015).
- **Sepsis-3** [k]: sepsis = suspected infection + acute SOFA rise ≥2; septic shock = vasopressors to keep MAP ≥65 AND lactate >2 mmol/L despite adequate fluids (mortality ~40%).
- **NEWS2** — see §2B. ≥5 triggers sepsis screen (NHS). [k]
- **CURB-65** — §2B. **PSI/PORT** for CAP (class I–II outpatient) [k].
- **Centor / McIsaac** [k]: tonsillar exudate; tender anterior cervical nodes; fever history; absence of cough (1 each); McIsaac age 3–14 +1, ≥45 −1. GAS probability: 0: 1–2.5%; 1: 5–10%; 2: 11–17%; 3: 28–35%; 4–5: 51–53%. 0–1 no test; 2–3 RADT/culture; ≥4 test or treat (IDSA: test). Fine 2012 (JAMA Intern Med, 206,870 pts) similar.
- **LRINEC** (necrotising fasciitis; Wong 2004) [k]: CRP ≥150 (4), WBC 15–25 (1) >25 (2), Hb 11–13.5 (1) <11 (2), Na <135 (2), Cr >1.6 mg/dL (2), glucose >180 mg/dL (1); ≥6 intermediate, ≥8 high; sensitivity only ~68% in meta-analysis — do not rule out.
- **MASCC** for febrile neutropenia (≥21 low risk) [k]. **Kocher** — §3B.

### C. Likelihood ratios — Metlay 1997 (§2C); Attia 1999 (§4C). Bacterial vs viral: no exam finding reliable; chills/rigors LR+ ~1.5–2 for bacteraemia; hypotension LR+ ~2; SIRS ≥2 LR+ ~1.3 for bacteraemia (Coburn, JAMA 2012 "Does this adult patient with suspected bacteremia require blood cultures?": Shapiro rule) [k].

### D. Test thresholds
- **Lactate**: >2 mmol/L = hypoperfusion/sepsis-3 shock criterion; ≥4 mmol/L → 30 mL/kg crystalloid within 3 h (SSC 2021), remeasure within 2–4 h; mortality by initial lactate 0–2.4: ~5%, 2.5–3.9: ~9%, ≥4: ~28% (Shapiro 2005) [k]. Lactate clearance ≥10–20% = resuscitation target [k].
- **Procalcitonin** [k]: ProHOSP (Schuetz, JAMA 2009) LRTI algorithm: <0.1 µg/L antibiotics strongly discouraged; <0.25 discouraged; ≥0.25 encouraged; ≥0.5 strongly encouraged; >2 high risk of sepsis/bacteraemia; serum PCT >0.5 ng/mL favours bacterial meningitis (sens ~95%). Rises 3–6 h after insult; falsely low early; raised in surgery, burns, cardiogenic shock. SSC 2021: do not use PCT to decide initiation of antibiotics.
- **CRP**: nonspecific; <10 mg/L normal; >100 mg/L supports serious bacterial infection; peaks 36–50 h; in children fever without source CRP >40 mg/L and PCT >0.5 ng/mL raise SBI risk [k].
- **WBC**: >12k or <4k; bands >10%; neutropenia ANC <500 (febrile neutropenia = T ≥38.3 once or ≥38.0 for 1 h + ANC <500 or expected) [k].
- Blood cultures ×2 before antibiotics (SSC); antibiotics within 1 h for shock/probable sepsis; MAP ≥65 target; urine output ≥0.5 mL/kg/h [k].

### E. Imaging [k]
- CXR for all with respiratory symptoms/sepsis without clear source (ACR Acute Respiratory Illness). CT abdomen/pelvis with IV contrast for sepsis of unknown abdominal source; CT head + LP for meningitis suspicion (CT before LP only if immunocompromise, CNS disease history, new seizure, papilloedema, abnormal consciousness, focal deficit — IDSA). MRI spine with contrast for suspected epidural abscess. Echo (TTE then TEE) for endocarditis. POCUS for abscess, cholecystitis, hydronephrosis, effusions. Imaging should not delay antibiotics.

---

## 9. UPPER GI BLEEDING

### A. Can't-miss
Variceal haemorrhage (cirrhosis); peptic ulcer with high-risk stigmata (spurting/visible vessel); aortoenteric fistula (prior aortic graft — "herald bleed"); Dieulafoy lesion; Boerhaave/Mallory-Weiss with instability; haemorrhagic shock; malignancy; anticoagulant-associated bleeding. [k]

### B. Decision rules
**Glasgow-Blatchford Score** (Blatchford, Lancet 2000; derivation 1,748, validation 197 [k]) [components k, performance v]
- BUN mg/dL (mmol/L): 18.2–22.4 (6.5–7.9) 2; 22.4–28 (8–9.9) 3; 28–70 (10–24.9) 4; ≥70 (≥25) 6. Hb g/dL men: 12–12.9 1; 10–11.9 3; <10 6; women: 10–11.9 1; <10 6. SBP 100–109 1; 90–99 2; <90 3. Pulse ≥100 1. Melaena 1. Syncope 2. Hepatic disease 2. Cardiac failure 2. Max 23.
- Stanley 2009 (Lancet): GBS 0 — 123 pts (16%) managed as outpatients, no interventions/deaths [k]. Stanley 2017 (BMJ, 3,012 pts international): GBS ≤1 optimum for survival without intervention — sensitivity 98.6%, specificity 34.6%, PPV 96.6%; 3.4% of GBS ≤1 needed intervention or died; GBS ≥7 best for endoscopic treatment (sens 80%, spec 57%); AUROC for intervention 0.86 (GBS) vs 0.62 AIMS65 vs 0.61 admission Rockall; PNED/AIMS65 best for mortality (0.77) [v]. Use: GBS 0–1 → outpatient; rule-out of need for intervention.

**Rockall** (Rockall, Gut 1996; 4,185 derivation, 1,625 validation) [v for mortality; components k]
- Age <60 0; 60–79 1; ≥80 2. Shock: HR >100 (SBP ≥100) 1; SBP <100 2. Comorbidity: none 0; CHF/IHD/major 2; renal/liver failure/disseminated malignancy 3. (Pre-endoscopy max 7.) Endoscopic diagnosis: Mallory-Weiss/no lesion 0; all other 1; upper-GI malignancy 2. Stigmata: none/dark spot 0; blood/adherent clot/visible or spurting vessel 2. Full max 11.
- Mortality by pre-endoscopy score 0–7: 0.2, 2.4, 5.6, 11, 24.6, 39.6, 48.9, 50% [v]. Full score ≤2 → mortality ~0.1%, rebleed ~4% [k]. Use: prognosis (mortality), not triage for discharge (GBS better).
- **AIMS65** [k]: Albumin <3 g/dL, INR >1.5, altered Mental status, SBP ≤90, age ≥65; mortality 0: 0.3% → ≥4: ~25–32%.

### C. Likelihood ratios — Srygley, JAMA 2012 ("Does this patient have a severe upper GI bleed?") [k, not verified]: melaena on exam LR+ 25 (4–174); melaena history 5.1–5.9; NG aspirate with blood/coffee grounds LR+ 9.6; BUN:creatinine >30 LR+ 7.5 (2.8–12); clots in stool LR+ 0.05 for upper source. For severe bleed: NG aspirate red blood LR+ 3.1; tachycardia LR+ 4.9 (3.2–7.6); Hb <8 g/dL LR+ 4.5–6.2; GBS 0 LR− 0.02. Syncope/orthostasis non-discriminatory.

### D. Test thresholds [k]
- Transfuse at Hb <7 g/dL (restrictive; Villanueva NEJM 2013 improved survival), <8 if ACS/CAD; massive transfusion for haemodynamic instability. INR >1.5 reverse if bleeding on warfarin; platelets <50k transfuse. BUN/Cr ratio >30 (or urea/Cr >100 in SI) suggests upper source. Lactate >2–4 for occult shock. Shock index >1. Endoscopy within 24 h (≤12 h for variceal/unstable after resuscitation). Cirrhosis: antibiotics (ceftriaxone), terlipressin/octreotide. PPI infusion pre-endoscopy reduces high-risk stigmata but not mortality.

### E. Imaging [k] — ACR Nonvariceal UGIB 2020: endoscopy is first-line; CTA abdomen/pelvis Usually Appropriate for haemodynamically significant bleeding when endoscopy negative/unavailable or for suspected aortoenteric fistula (detects ≥0.3–0.5 mL/min); catheter angiography for embolisation after positive CTA; tagged RBC scan for intermittent lower bleeding. Plain films not useful; CXR/upright for suspected perforation.

---

## 10. ACUTE LOW BACK PAIN

### A. Can't-miss
Cauda equina syndrome; spinal epidural abscess; vertebral osteomyelitis/discitis; spinal cord compression (metastasis, haematoma); ruptured/leaking AAA; vertebral fracture (osteoporotic/traumatic, especially on steroids); malignancy; retroperitoneal haemorrhage (anticoagulated); aortic dissection; pyelonephritis/renal colic with obstruction + infection; pancreatitis. [k]

### B. Decision rules — no validated ED decision rule; red-flag frameworks (ACP/APS 2007; NICE NG59; Henschke 2009 fracture rule) [k]:
- Henschke 2009 (Arthritis Rheum, primary care, 1,172 pts): prolonged corticosteroid use, age >70, significant trauma, contusion/abrasion — ≥1 feature LR+ 3.1 (?), ≥3 features LR+ 218 (vertebral fracture) [k].
- Cancer (Deyo & Diehl 1988; Jarvik & Deyo 2002): history of cancer, age >50, unexplained weight loss, failure to improve after 1 month — if all absent, cancer ≈ 0.0% in primary-care series.
- Cauda equina: bilateral sciatica, saddle anaesthesia, urinary retention/overflow incontinence, faecal incontinence, reduced anal tone; post-void residual >200 mL (sens ~90%, spec ~95%) [k].
- STarT Back / Oswestry are not ED tools; Sciatica: SLR, crossed SLR.

### C. Likelihood ratios (Deyo, JAMA 1992 RCE "What can the history and physical examination tell us about low back pain?"; Jarvik & Deyo, Ann Intern Med 2002) [k, not verified]
- Cancer: history of cancer LR+ 14.7; unexplained weight loss 2.7; failure to improve after 1 month 3.0; age >50 2.7; no relief with bed rest 1.7; ESR ≥20 sensitivity 78%; plain film sensitivity 60%.
- Compression fracture: age >70 LR+ ~5–12 (spec 0.96); corticosteroid use LR+ 12 (spec 0.99); significant trauma. 
- Infection (epidural abscess/osteomyelitis): fever sensitivity 50% (TB 27%, pyogenic 50%, epidural abscess 83%); IVDU, recent infection/instrumentation, immunosuppression; ESR >20 sensitivity ~95% for epidural abscess (Davis 2004); classic triad (fever, back pain, neuro deficit) present in only ~13%.
- Cauda equina: urinary retention sensitivity 90%, specificity 95% (LR+ ~18, LR− ~0.1); saddle anaesthesia sensitivity ~75%; anal tone decreased 60–80%.
- Disc herniation: SLR sensitivity 91%, specificity 26%; crossed SLR sensitivity 29%, specificity 88%; great-toe extensor weakness/ankle reflex loss for L5/S1.
- AAA: see §3C (Lederle 1999).

### D. Test thresholds [k]
- ESR >20 mm/h and/or CRP >10 mg/L in suspected infection/malignancy (ESR/CRP both normal → epidural abscess very unlikely; NPV ~99% in ED series (Davis 2011 pathway)); WBC often normal in SEA (sens ~60%). Blood cultures if SEA suspected (positive ~60%). Urinalysis for pyelonephritis/stone; POCUS aorta ≥3 cm = aneurysm; post-void residual >200 mL; calcium/alk phos for malignancy. Glucose/HbA1c in SEA risk (diabetes).

### E. Imaging (ACR Low Back Pain 2021) [k]
- Acute/subacute uncomplicated LBP (<6 wk, no red flags): imaging Usually Not Appropriate.
- Red flags for cancer, infection, immunosuppression, or progressive/severe neuro deficit/suspected cauda equina: MRI lumbar spine without contrast Usually Appropriate (with and without contrast if infection/malignancy suspected); CT if MRI contraindicated; emergent MRI (whole spine if SEA suspected — skip lesions ~15%).
- Suspected fracture (osteoporosis, steroids, trauma, age >70): radiographs or CT lumbar spine Usually Appropriate; MRI for neurological compromise or age of fracture.
- Suspected AAA: POCUS then CTA. Suspected renal colic: low-dose CT without contrast.

---

## Cross-cutting source disagreements worth encoding
1. **Klompas 2002 vs Ohle 2018** on pulse deficit (LR+ 5.7 vs 2.7) and widened mediastinum (2.0 vs 3.4) — use the pooled 2018 values if you want one number; both are wide-CI [v].
2. **CURB-65 score 2 mortality**: 13% (derivation) vs 9.2% (combined cohorts) — store both with cohort labels [v/k].
3. **Sgarbossa original specificity**: 90% (derivation) / 96% (validation) / 98% (2008 meta-analysis) [v].
4. **SFSR**: 96–98% sensitivity (originators) vs 86% (independent meta-analysis) [v].
5. **CSRS bands**: −3 to −2 very low vs −3 to 0 very low, depending on secondary source; use the CMAJ 2016 table [v].
6. **Jolt accentuation**: 100% sensitivity in Attia 1999 vs ~21–64% in later studies [k].
7. **NEXUS NPV**: 99.8% vs 99.9% between summaries [v].
8. **BISAP per-score mortality**: original paper's rates are lower than the commonly tabulated 5–8/13–19/22% figures [v].
9. **Alvarado cut-off 7 "82%"**: is specificity in one source and sensitivity in another; Ohle's abstract says specificity 81% [v].
10. **Canadian CT Head "vomiting" threshold**: ≥2 episodes in the Lancet abstract; some summaries write ">1" or "2" [v].

---

## Sources (URLs consulted this session)
- ESC 2020 NSTE-ACS guideline (Table 5): https://academic.oup.com/eurheartj/article/42/14/1289/5898842
- Rev Esp Cardiol ESC 0/1h implementation (assay table): https://www.revespcardiol.org/en-implementation-of-the-esc--h-h-high-sens-articulo-S1885585723000270
- JACC 2018 prospective validation 0/1h: https://www.jacc.org/doi/10.1016/j.jacc.2018.05.040
- HEART validation (Backus 2013) summary: https://wikem.org/wiki/EBQ:A_prospective_validation_of_the_HEART_score_for_chest_pain_patients_at_the_emergency_department ; https://journalfeed.org/?p=185 ; https://www.emdocs.net/heart-matter/ ; Six 2008 derivation summary: https://www.tomwademd.net/?p=117978
- ADvISED (Nazerian 2018): https://fis.uke.de/portal/en/publications/diagnostic-accuracy-of-the-aortic-dissection-detection-risk-score-plus-ddimer-for-acute-aortic-syndromes-the-advised-prospective-multicenter-study(7b2715fd-2c78-4fa2-b765-fafe2927b74f).html ; https://emottawablog.com/2018/06/diagnostic-accuracy-of-the-aortic-dissection-detection-risk-score-plus-d-dimer-for-acute-aortic-syndromes-the-advised-prospective-multicenter-study/
- Ottawa SAH validation (Perry 2017): https://www.cmaj.ca/content/189/45/E1379/T3 ; https://emottawablog.com/2017/11/validation-ottawa-sah-rule/
- CSRS validation (2020): https://jamanetwork.com/journals/jamainternalmedicine/fullarticle/2763181 ; AAFP summary: https://www.aafp.org/pubs/afp/issues/2021/0315/p375.html ; derivation CMAJ: https://www.cmaj.ca/content/188/12/e289
- Swap & Nagurney 2005: https://pubmed.ncbi.nlm.nih.gov/16304077/ ; https://jamanetwork.com/journals/jama/fullarticle/201900 ; https://www.aliem.com/chest-pain-value-of-good-history/ ; Fanaroff 2015: https://pubmed.ncbi.nlm.nih.gov/26547467/
- Klompas 2002: https://read.qxmd.com/read/11980527/does-this-patient-have-an-acute-thoracic-aortic-dissection ; https://www.ncbi.nlm.nih.gov/books/NBK69165/ ; Ohle 2018 meta-analysis: https://pubmed.ncbi.nlm.nih.gov/29265487/ ; https://www.thennt.com/cms/lr/aortic-dissection/
- Wang 2005 HF: https://www.qxmd.com/r/16234501 ; https://www.aliem.com/paucis-verbis-chf-likelihood-ratios/
- Attia 1999 meningitis: https://www.aafp.org/afp/2000/0115/p493 ; https://canadiem.org/boring-question-useful-physical-examination-manoeuvres-patient-suspected-meningitis-adults/
- Wagner 1996 appendicitis: https://pubmed.ncbi.nlm.nih.gov/8918857/ ; https://www.aafp.org/afp/2018/0701/p25 ; https://www.aafp.org/pubs/afp/issues/2008/0315/p828.html ; JAMA clarification letter: https://jamanetwork.com/journals/jama/article-abstract/1725121
- Trowbridge 2003 cholecystitis: https://read.qxmd.com/read/12503981/does-this-patient-have-acute-cholecystitis ; https://www.aliem.com/paucis-verbis-strength-of-diagnostic-tests-for-cholecystitis/
- Metlay 1997 pneumonia: https://www.ncbi.nlm.nih.gov/books/NBK67086/ ; https://community.the-hospitalist.org/content/how-accurate-clinical-diagnosis-pneumonia ; Ebell 2020: https://onlinelibrary.wiley.com/doi/full/10.1111/acem.13965
- Easter 2015 head trauma: https://www.aafp.org/afp/2016/0401/p594a.html ; https://www.scinapse.io/papers/2212683164
- Smetana & Shmerling 2002 GCA: https://pubmed.ncbi.nlm.nih.gov/11754714/ ; https://thennt.com/lr/temporal-arteritis/ ; https://www.mdedge.com/familymedicine/article/63031/which-clinical-features-and-lab-findings-increase-likelihood-temporal
- Anand 1998 DVT: https://experts.mcmaster.ca/scholarly-works/190483 ; https://www.aafp.org/pubs/afp/issues/1998/1001/p1207.html ; 2006 update: https://pubmed.ncbi.nlm.nih.gov/16403932/
- Goldstein & Simel 2005 stroke: https://scholars.duke.edu/publication/681088 ; https://elentra.healthsci.queensu.ca/assets/modules/LR-module/the_rational_clinical_examination_continued.html
- Carpenter 2016 SAH: https://onlinelibrary.wiley.com/doi/full/10.1111/acem.12984 ; https://first10em.com/subarachnoid-hemorrhage-lp/
- Chunilal 2003 PE: https://scholars.duke.edu/publication/681091 ; Kohn 2017 D-dimer interval LRs: https://pure.amsterdamumc.nl/ws/files/159146332/D-dimer-interval-likelihood-ratios-for-pulmonary-embolism.pdf
- SBO ultrasound (Gottlieb 2018): https://thennt.com/lr/pocus-atlas-small-bowel-obstruction/
- SFSR: https://wikem.org/wiki/San_Francisco_Syncope_Rule ; https://pmc.ncbi.nlm.nih.gov/articles/PMC2946941 ; https://www.ebmedicine.net/topics/cardiovascular/syncope/calculators
- NEXUS / CCR: https://www.aafp.org/afp/2004/0515/p2449 ; https://reliasmedia.com/articles/2691-nexus-vs-the-canadian-c-spine-rule-let-the-battle-begin ; https://www.bestbets.org/bets/bet.php?id=126 ; https://www.tamingthesru.com/blog/diagnostics/c-spine-rules
- Canadian CT Head Rule: https://www.qxmd.com/r/11356436 ; https://www.wikijournalclub.org/wiki/Canadian_CT_Head_Rule ; https://www.aafp.org/afp/2001/1201/p1886a.html
- PECARN: https://wikem.org/wiki/EBQ:PECARN_Head_Trauma ; https://pmc.ncbi.nlm.nih.gov/articles/PMC5769508/table/Tab1 ; https://www.2minutemedicine.com/pecarn-prediction-rules-for-children-at-a-low-risk-of-clinically-important-traumatic-brain-injury
- GBS (Stanley 2017): https://eprints.gla.ac.uk/187156 ; https://journalfeed.org/?p=448 ; https://bestbets.org/bets/bet.php?id=1942
- Rockall 1996: https://www.rcemlearning.co.uk/modules/upper-gastrointestinal-haemorrhage/lessons/risk-stratification-2/topic/nonvariceal-bleed/ ; https://www.2minutemedicine.com/the-rockall-score-risk-assessment-after-acute-upper-gastrointestinal-haemorrhage-classics-series
- qSOFA/SIRS (Seymour 2016 and others): https://www.hksccm.org/?p=4779 ; https://journalclub.wustl.edu/2017/01/24/prognostic-accuracy-of-sepsis-3-criteria-for-in-hospital-mortality-among-patients-with-suspected-infection-presenting-to-the-emergency-department/ ; https://ahro.austin.org.au/austinjspui/handle/1/16610?mode=full
- CURB-65 (Lim 2003): https://pmc.ncbi.nlm.nih.gov/articles/PMC1746657 ; https://wikem.org/wiki/EBQ:Pneumonia_curb_65
- Alvarado (Ohle 2011): https://bmcmedicine.biomedcentral.com/articles/10.1186/1741-7015-9-139 ; https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3299622/
- AAS (Sammalkorpi 2014/2017; validations): https://link.springer.com/article/10.1186/1471-230X-14-114 ; https://journals.sagepub.com/doi/10.1177/1457496916683099 ; https://www.sciencedirect.com/science/article/pii/S2589845023000489 ; AIR: https://en.wikipedia.org/wiki/Appendicitis_Inflammatory_Response_score ; https://pmc.ncbi.nlm.nih.gov/articles/PMC8154764/
- PERC (Kline 2008): https://wikem.org/wiki/EBQ:PERC_Rule_Validation ; https://www.wikijournalclub.org/wiki/PERC ; https://sinaiem.org/wp-content/uploads/2016/11/Kline-Prospective-multicenter-evaluation-of-PERC.pdf
- ADJUST-PE: https://wikem.org/wiki/EBQ:ADJUST-PE_Trial ; https://journalclub.wustl.edu/2014/03/25/age-adjusted-d-dimer-cutoff-levels-to-rule-out-pulmonary-embolism-the-adjust-pe-study/
- YEARS: https://rebelem.com/the-years-study-simplified-diagnostic-approach-to-pe/ ; https://emergencymedicine.wustl.edu/items/the-years-algorithm-for-evaluation-of-pe/ ; external validation: https://pubmed.ncbi.nlm.nih.gov/32869501/ ; meta-analysis 2024: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11614012/
- Sgarbossa / modified Sgarbossa: https://www.aliem.com/2013/12/modified-sgarbossa-criteria-ready-primetime/ ; https://www.tamingthesru.com/blog/diagnostics/miinlbbb ; https://journalfeed.org/?p=324 ; https://www.emdocs.net/ecg-pointers-the-barcelona-criteria/
- Ottawa ankle (Bachmann 2003): https://pubmed.ncbi.nlm.nih.gov/12595378/ ; https://pmc.ncbi.nlm.nih.gov/articles/PMC149439/
- NT-proBNP (ICON-RELOADED 2018; ICON 2006): https://reliasmedia.com/articles/142406-age-stratified-nt-probnp-thresholds-identify-acute-heart-failure ; https://acutecaretesting.org/en/articles/choosing-cut-offs-for-nt-probnp
- BISAP: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4474919/ ; https://pubmed.ncbi.nlm.nih.gov/18519429/ ; https://www.mdcalc.com/calc/1735/bisap-score-pancreatitis-mortality
- BE-FAST (Aroor 2017): https://pubmed.ncbi.nlm.nih.gov/28082668/
- ACR Appropriateness Criteria — Suspected Acute Aortic Syndrome: https://acsearch.acr.org/docs/69402/Narrative ; Right Lower Quadrant Pain–Suspected Appendicitis: https://acsearch.acr.org/docs/69357/Narrative/ ; AAFP summary: https://www.aafp.org/pubs/afp/issues/2020/1001/p403.html ; ACR search portal for the remaining topics (headache, head trauma, spine trauma, low back pain, syncope, stroke, AMS, SBO, RUQ, nonlocalised abdominal pain, acute respiratory illness, nonvariceal UGIB): https://acsearch.acr.org/list

**Items I could not web-verify this session and recommend checking first:** ESC Architect hs-cTnI cut-offs and all non-Elecsys assay rows; Wagner 1996 minor-finding LRs; Panju 1998 exam LRs; Fanaroff 2015 LRs; SBO physical-exam LRs (McGee/Böhner); Albassam 2019 syncope LRs; Srygley 2012 UGIB LRs; Deyo/Jarvik low-back-pain LRs; Kocher probabilities; Ottawa knee pooled numbers; CSRS category rates beyond very-low/low; the full ACR rating tables for the scenarios other than AAS and RLQ pain.