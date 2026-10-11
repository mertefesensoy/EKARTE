# Computable-knowledge infrastructure: terminologies, logic standards, DDx engines, datasets

Date: 2026-10-11. Research note compiled for the EKARTE knowledge model (`knowledge-model.md`). Direct fetches of snomed.org, skrs.saglik.gov.tr and hpo.jax.org were blocked from the research sandbox, so licence details for those come from search snippets and secondary sources; items marked **[verify]** must be confirmed against the primary page before any contract.

## 1. Terminologies and ontologies

| Terminology | What it codes in EKARTE | Licence / access | Turkish availability |
|---|---|---|---|
| SNOMED CT | Findings, symptoms, disorders, procedures; the only terminology that represents "finding absent" with context and links findings to disorders | Affiliate licence. Türkiye is not a SNOMED International member, so production use falls under Non-Member Territory fees; free for qualifying research. A UMLS licence still makes you an Affiliate with annual usage reporting. **[verify member list]** | No Turkish translation, no National Release Centre |
| ICD-10, Turkish MoH list | Output diagnosis layer expected by HBYS, e-Nabız, MEDULA | Distributed through SKRS. A published study found 320 spelling and 11 semantic discrepancies between the MoH list and one hospital's copy, so sync from SKRS, never hard-code | Official Turkish |
| ICD-11 | Future diagnosis layer | WHO licence, free; REST API | Turkish is a browser language in the 2025 and 2026 releases; no MoH transition date |
| SKRS (Sağlık Kodlama Referans Sunucusu) | ICD-10, SUT procedures, branches, drugs with ATC, institutions and dozens of other lists; mandatory for valid USS submissions | MoH web service `GetSkrsList` returns active lists as JSON; XML services too. No fee known **[verify registration]** | Native |
| LOINC | Lab tests, vitals, ECG and imaging observations | Free, attribution, commercial use allowed | Official Turkish linguistic variant (LNC-TR-TR v2.77, Feb 2024, in UMLS) maintained with two MoH departments |
| HPO | Symptom and finding coding where SNOMED is unavailable; disease–phenotype frequencies usable as priors | Free, JAX licence, cite HPO, no third-party modification **[verify]** | No Turkish layer; community translation possible |
| UMLS | Crosswalks ICD-10, SNOMED, LOINC, HPO, Orphanet | Free NLM licence, annual report | Partial (LOINC-TR) |
| ATC/DDD | Drug classes for medication-history questions | WHOCC: free non-commercial, commercial needs permission **[verify]** | Turkey codes all drugs by ATC in the SKRS drug list |
| Orphanet / ORDO | Rare-disease tail | CC BY 4.0 | No Turkish layer, ICD-10 aligned |
| RxNorm | US drug names | Free | Not applicable to Turkish drugs |

Practical reading: the mandatory Turkish vocabularies are ICD-10, SUT and ATC, all via SKRS. SNOMED CT is the only one with a licence cost and no Turkish lexicon; LOINC, HPO, Orphanet and ICD are free.

## 2. Standards for computable clinical logic

| Standard | Fit for a question-asking, exclusion-driven engine | Real deployments |
|---|---|---|
| FHIR Clinical Reasoning (PlanDefinition, ActivityDefinition, Library; CPG-on-FHIR) | Good for "what to order next" and "apply exclusion rule"; actions can reference Questionnaires | WHO SMART Guidelines (run in OpenMRS), CMS eCQMs, AHRQ CDS Connect |
| CQL (Clinical Quality Language) | Natural encoding for rule-out criteria and result interpretation; open Java and JS engines (Apache 2.0) | All CMS eCQMs since 2019; AHRQ CDS Connect; WHO SMART Guidelines |
| CDS Hooks | Optional outer façade; Turkish HBYS vendors generally do not support it, so the MCP server stays the integration layer | Epic, Oracle Health (partial) |
| FHIR Questionnaire + SDC, adaptive `$next-question` | Best fit for the structured-history front end: the server decides the next item from prior answers; `$extract` writes answers back as coded Observations | NLM LHC-Forms, Android FHIR SDK, Aidbox |
| Arden Syntax | Legacy alerting; no questionnaire or probabilistic constructs. Not recommended | Historic |
| openEHR GDL2 | Reasonable only on an openEHR stack, which Turkey's HIS is not | Cambio CDS in Swedish regions |
| BPM+ Health (BPMN/CMMN/DMN) | Useful as an authoring view for pathways and decision tables; essentially no live production deployments | Pilots only |
| PROforma / OpenClinical | Alternative authoring formalism, small community | Demonstrators |

Fit summary: SDC adaptive Questionnaire (asking) + CQL Libraries (exclusion and interpretation rules) + PlanDefinition/ActivityDefinition (test recommendations) is the only combination that is standard, free, has open engines and documented production use.

## 3. Machine-readable differential-diagnosis engines and APIs

| Product | Representation | Licence / API | Accuracy evidence | Turkish |
|---|---|---|---|---|
| Isabel DDx API | Proprietary text-mined knowledge base, NLP matching | Commercial headless API; EHR integrations | German-version study 2023: correct dx present 82 percent (Pro), top-3 37 percent | Vendor claims any language; no Turkish evidence |
| DXplain (MGH) | Curated finding–disease weights (~2,400 diseases, ~5,000 findings); suggests discriminating findings | Institutional licence; no public API | NEJM 1994; JAMA Netw Open 2024/25: with labs 72 percent vs ChatGPT 64 percent | English only |
| Infermedica Engine API | Bayesian network over ~1,500 conditions; `/diagnosis` returns next question and ranked conditions | Commercial, usage-based; other languages under custom plans | BMJ Open 2020: below GPs but competitive | Symptomate app lists Turkish, so content may be localised **[verify]** |
| Ada Health | Bayesian engine, curated | Enterprise contract | BMJ Open 2020: top-3 70.5 percent vs GPs 82.1 percent | No Turkish |
| VisualDx | Findings-based, dermatology strength | Commercial API | Dermatology | No |
| Babylon | Counterfactual diagnosis (Nat Commun 2020) | Defunct since 2023; partial code on GitHub | 72.5 vs 77.3 percent on vignettes | No |
| Symptoma | Literature-mined ranking, ~20k diseases | Commercial API | ED RCT 2024 | Claims 36 languages; Turkish unconfirmed |
| Mediktor | ML question engine | Commercial SDK, 16 languages | Barcelona ED study 2017 | Unconfirmed |
| WikEM / OpenEM | Open EM wiki, DDx lists, algorithms | Open access, wikitext only | Reference, not engine | No |
| Open DDx knowledge base (BMC MIDM 2019) | >2,000 ICD-10 diseases, 8,000 SNOMED/LOINC-coded observations | Open access | 117 cases, comparable to Isabel/DXplain | No |
| BMJ Best Practice, UpToDate Connect | Monographs with differential tables; APIs | Institutional / partner licence | Not engines | No |

Takeaway: no vendor offers a licensable, Turkish-ready ED DDx engine, and all are black boxes, which conflicts with an exclusion engine that must explain why a diagnosis is closed. Build the knowledge base (findings × diseases × likelihood ratios) in-house; use vendor APIs at most as benchmark comparators.

## 4. Open datasets

| Dataset | Content | Access | Use here |
|---|---|---|---|
| MIMIC-IV-ED v2.2 | ~425k ED stays with triage chief complaint, vitals, acuity, ICD diagnoses | PhysioNet credentialed DUA | Priors per complaint, rule firing at scale; US case mix, engine behaviour only |
| MIMIC-IV-Ext-CDS, MIETIC | Pain, chief complaint, labs; 9,629 triage cases | PhysioNet | Triage and complaint parsing tests |
| eICU-CRD | 200k ICU admissions | Credentialed | Downstream outcomes for high-acuity branches |
| PTB-XL | 21,799 12-lead ECGs with SCP statements | CC BY 4.0 | ECG interpretation step |
| DDXPlus (NeurIPS 2022) | 1.3M synthetic patients, 49 pathologies, 223 evidences with hierarchical answers, ground-truth differential with probabilities | CC BY | Closest public analogue of EKARTE's data model; mechanical test of question selection |
| MedQA, MedMCQA | Exam MCQs | MIT-like **[verify]**, Apache 2.0 | Regression tests |
| MedDialog | Doctor–patient dialogues | Licence unknown | Legally fragile; phrasing only |
| NEJM Healer | Staged clinical-reasoning cases | Commercial | Gold-standard reasoning evaluation if licensed |
| AgentClinic | Simulated patient, doctor, measurement agents | Open | End-to-end loop harness |
| SDBench | 304 NEJM CPC cases as sequential encounters with test costs | Paper public; case release to confirm | Cost-aware metric to copy |
| Turkish clinical NLP | Synthetic Turkish radiology NER set; BioBERTurk | Mostly closed | Building blocks only; Turkish ED data must come from partner hospitals under KVKK |

## 5. Structured history-taking and probabilistic engines

- **CLEOS (Karolinska)**: expert-system history taker whose question bank is driven by a working differential; CLEOS-derived HEART/EDACS/T-MACS reached sensitivity 0.91 to 0.97 for 30-day MACE (JMIR 2026). Proprietary, but the papers describe item design. Closest published precedent for EKARTE's question engine.
- **HEART, EDACS, T-MACS**: structured chest-pain items; the HEART "History" item has only fair inter-rater agreement, which argues for granular questions rather than a single gestalt score.
- **OPQRST / SOCRATES**: canonical item skeleton for pain complaints.
- **Rational Clinical Examination (JAMA series, JAMAevidence book)**: over 50 systematic reviews with likelihood ratios per history and exam item; subscription; no structured database, so LRs are transcribed by hand.
- **Symptom-checker evidence**: Semigran 2015 (correct dx first 34 percent, top-20 58 percent); Wallace 2022 (primary-dx accuracy 19 to 38 percent). Consumer checkers are not the bar.
- **Bayesian engines**: de Dombal 1972 naive Bayes on acute abdomen, 91.8 percent in 304 patients; a Hacettepe study reached 78.6 percent on Turkish non-traumatic acute abdomen with naive Bayes; Iliad, QMR, Meditel, DXplain (Berner NEJM 1994: 0.52 to 0.71, no winner); Babylon counterfactual ranking.
- **DDXPlus baselines**: AARLC, BASD, CASANDE (adds exploration, confirmation and severity rewards), DDxT.
- **Information-gain question selection**: BALAR (mutual-information question choice), MedClarify, MedKGI, SDBench/MAI-DxO cost-aware test selection.

## 6. Recommended stack

**Terminologies.** Internal canonical concept IDs mapped to ICD-10 (SKRS list) for every output diagnosis, LOINC with the Turkish variant for every test and result, ATC via the SKRS drug list for medication history, HPO for findings, Orphanet for the rare tail. SNOMED CT only for internal modelling under a research licence, never a hard dependency for Turkish deployment. Sync SKRS lists at startup.

**Logic.** Each chief-complaint interview as a FHIR SDC adaptive Questionnaire served through `$next-question`, items coded and `$extract`-able into Observations. Rule-out and interpretation logic as CQL Libraries referenced by PlanDefinition/ActivityDefinition actions. Everything exposed as MCP tools; CDS Hooks adapter only when a vendor supports it. DMN tables at most as an authoring view that compiles to CQL.

**Question selection.** Bayesian model over findings × diagnoses with priors conditioned on complaint, age and sex (initially from MIMIC-IV-ED and literature, later partner-hospital data) and likelihood ratios from the Rational Clinical Examination and decision-rule literature. A diagnosis is closed when its posterior falls below a severity-weighted threshold, with the responsible findings listed. Next question or test by expected information gain weighted by severity and cost. The language model normalises Turkish free text to coded findings and phrases explanations; it never ranks. Validate structure on DDXPlus, accuracy on MIMIC-IV-ED, interview behaviour with AgentClinic-style simulation, and benchmark against Isabel or Infermedica on shared vignettes.

## Sources

- SNOMED: https://www.snomed.org/members ; https://www.nlm.nih.gov/healthit/snomedct/snomed_licensing.html
- SKRS / e-Nabız: https://skrs.saglik.gov.tr/doc/index.html ; https://rehber.enabiz.gov.tr/Home/UssIsleyis
- ICD-11 Turkish: https://icd.who.int/docs/browser/tr/Browser/
- LOINC Turkish: https://loinc.org/international/turkish/ ; https://nlm.nih.gov/research/umls/sourcereleasedocs/current/LNC-TR-TR/metadata.html
- HPO: https://hpo.jax.org/app/license ; Orphanet: https://www.orphadata.com/
- ATC in Turkey: https://titck.gov.tr/storage/announcement/v4ZzVOUI.pdf
- FHIR SDC adaptive: https://hl7.org/fhir/uv/sdc/OperationDefinition-Questionnaire-next-question.html ; https://build.fhir.org/ig/HL7/sdc/adaptive.html
- WHO SMART Guidelines / CQL: https://smart.who.int/ig-starter-kit/v1.0.0/l3_cql.html ; https://cql.hl7.org/ ; AHRQ CDS Connect: https://cds.ahrq.gov/cdsconnect
- CDS Hooks: https://cds-hooks.hl7.org/ ; openEHR GDL2: https://specifications.openehr.org/releases/CDS/latest/GDL2.html ; BPM+ Health: https://omg.org/hot-topics/healthcare-and-bpmn.htm
- Isabel: https://v4.isabelhealthcare.com/products/integration ; https://boris.unibe.ch/185000/
- DXplain: https://www.mghlcs.org/projects/dxplain/index.html ; Infermedica: https://developer.infermedica.com/docs/v3/basics ; Ada: https://ada.com/
- Babylon counterfactual: https://arxiv.org/abs/1910.06772 ; Symptoma: https://www.symptoma.com/ ; Mediktor: https://www.mediktor.com/
- WikEM: https://wikem.org/ ; Open DDx KB: https://pmc.ncbi.nlm.nih.gov/articles/PMC6486985/
- MIMIC-IV-ED: https://physionet.org/content/mimic-iv-ed/ ; PTB-XL: https://physionet.org/content/ptb-xl/ ; DDXPlus: https://figshare.com/articles/dataset/DDXPlus_Dataset/20043374 ; https://arxiv.org/abs/2205.09148
- AgentClinic: https://arxiv.org/abs/2405.07960 ; SDBench: https://arxiv.org/abs/2506.22405
- CLEOS: https://pmc.ncbi.nlm.nih.gov/articles/PMC8476015 ; https://www.jmir.org/2026/1/e76087
- Rational Clinical Examination: https://jamaevidence.mhmedical.com/
- Symptom checkers: https://www.bmj.com/content/351/bmj.h3480 ; https://www.jmir.org/2023/1/e43803/
- Bayesian DDx: https://www.aaai.org/Papers/KDD/1996/KDD96-010.pdf ; https://openaccess.hacettepe.edu.tr/handle/11655/18806
- Question selection: https://arxiv.org/abs/2605.05386 ; https://arxiv.org/abs/2602.17308 ; https://arxiv.org/abs/2512.24181 ; DDXPlus baselines: https://arxiv.org/abs/2210.07198 ; https://arxiv.org/abs/2312.01242
