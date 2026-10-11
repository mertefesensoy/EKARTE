# Literature review: AI-guided emergency differential diagnosis

Date: 2026-10-11. Scope: web search of peer-reviewed papers, preprints, registered trials and benchmarks on AI systems that take a patient's complaints and physical-exam findings, narrow the differential by exclusion, recommend tests and imaging, and interpret the results. This is the workflow the expert described (şikayet + fizik muayene bulguları → dışlayarak ana tanıya ulaşma → tetkik isteme ve değerlendirme).

## 1. Short answer

Yes, there is a substantial and fast-growing body of research, but it is fragmented. No single published system does the full loop (exam findings in → iterative exclusion → test ordering → result interpretation) in a live emergency department. Each step has been studied separately:

| Step in the expert's workflow | Research maturity | Representative work |
|---|---|---|
| Complaints + exam findings → differential list | Many retrospective and vignette studies, 2023–2026 | ten Berg 2023, Hoppe 2024, Shah-Mohammadi 2024, Niset 2025, Zhejiang 2025, Marmara trial 2026 |
| Iterative questioning and exclusion | Benchmarks and research prototypes, not clinical trials | Microsoft SDBench / MAI-DxO 2025, MediQ, MSDiagnosis, AgentClinic, Google AMIE |
| Recommending labs and imaging | Small simulated-case studies, mixed results | ACR-criteria alignment work, CCLM 2025 lab-test study, AJR 2024 |
| Interpreting results, updating the differential | Mostly embedded in the above; separate evidence is thin | Mass General Brigham JAMA Netw Open, Nature Medicine 2024 abdominal study |
| Effect on real ED outcomes | Almost none; RCT meta-analysis shows near-zero effect in EM | MDPI Appl Sci 2026 meta-analysis, Karolinska trial NCT07766863 |

## 2. Closest match to the expert's description: sequential diagnosis

**Sequential Diagnosis with Language Models (Microsoft AI, arXiv 2506.22405, June 2025).**
SDBench turns 304 NEJM clinicopathological conference cases into stepwise encounters. The model starts with a short presentation and must ask questions or order tests one at a time. A "gatekeeper" model releases a finding only when the request is specific. Scoring covers diagnostic accuracy and the cost of the tests ordered. MAI-DxO is an orchestrator that makes a general LLM behave like a panel (hypothesis keeper, test chooser, challenger, cost checker). With o3 it reported roughly 80 to 85 percent accuracy versus about 20 percent for 21 physicians working without references, at lower cost per case. Caveat: NEJM puzzle cases, physicians were denied internet and colleagues, not an ED population, Microsoft-reported figures. This is the most direct academic precedent for an "exclude, then order the next test" engine.

**Google AMIE, Nature 2025 ("Towards conversational diagnostic artificial intelligence").** Randomized, double-blind crossover OSCE-style study with patient actors, 20 primary care physicians, about 150 scenarios. AMIE beat physicians on diagnostic accuracy and on most history-taking and communication axes. Text-chat only, primary care rather than emergency, and the authors state more research is needed before real-world use.

**Interactive-reasoning benchmarks.** MediQ (question-asking before deciding), MSDiagnosis (multi-step diagnosis), AgentClinic (doctor agent requests simulated exams and imaging from a measurement agent), MedAgentBench (FHIR-based virtual EHR). AgentClinic found that converting standard MedQA questions into a sequential format cut accuracy to below a tenth of the original in some models. MediQ reported that naive prompting to ask clarifying questions can degrade reasoning. Lesson: the iterative format is much harder than one-shot vignettes and needs explicit state tracking.

## 3. Emergency-department specific diagnostic studies

- **ten Berg et al., Annals of Emergency Medicine 2023 (Jeroen Bosch Hospital, NL).** 30 real undifferentiated ED patients. With lab data included, correct diagnosis in top five: physicians 87 percent, GPT-3.5 97 percent, GPT-4 87 percent. Small sample.
- **Hoppe et al., JMIR 2024.** 100-patient retrospective cohort; GPT-4 outperformed ED physicians on diagnostic accuracy.
- **Shah-Mohammadi and Finkelstein, Diagnostics 2024.** Differential lists from first-24-hour EHR notes versus discharge diagnoses. Good at body-system level, inconsistent at fine-grained level; GPT-4 better than GPT-3.5.
- **Niset et al., JAMIA Open 2025.** Retrieval-grounded LLM pipelines on real ED cases. Diagnostic match 62 to 72 percent. Much higher for specific diagnoses (86 percent) than unspecific ones (31 percent) and for surgical versus medical cases. Accuracy depended more on the case than on the model.
- **Zhejiang University, 2025 retrospective (PMC13195009).** 154 emergency internal-medicine patients, five LLMs versus 15 emergency physicians. DeepSeek-V3 90 percent, GPT-4o 86 percent, versus physicians 77.5 percent on primary diagnosis; LLMs also scored higher on differential diagnosis.
- **Brodeur et al. (Harvard / BIDMC), arXiv 2412.10849, later in Science 2026.** o1-preview on real ED triage records: correct diagnosis 67 percent versus 55 and 50 percent for two attending physicians; also strong on management reasoning. Secondary-source figures.
- **International Journal of Emergency Medicine 2026, vignette study.** LLMs 74 percent versus EM physicians 57 percent; physicians dropped sharply on differential (45 percent) versus definitive diagnosis (69 percent).
- **Nature npj-family benchmarking, 2026.** Twelve simulated ED cases, five models; GPT-5 best.
- **Counter-evidence: Nature Medicine 2024 abdominal study.** 2,400 real cases across appendicitis, pancreatitis, cholecystitis, diverticulitis. LLMs performed significantly worse than clinicians when given all information, with errors in guideline adherence and result interpretation.
- **Turkey: Marmara University Pendik, NCT07632859 (2026).** Retrospective, 600 Turkish ED anamnesis notes, GPT-4o versus Claude 4.6 Sonnet against a three-specialist ICD-10 consensus. Listed as completed, no results published yet. First Turkish-language ED LLM diagnostic study. Sister trial NCT07626060 on HEART score and 30-day MACE. No other Turkish clinical evaluation was found; Turkish literature consists of book chapters and reviews.

## 4. Physical examination findings as input

No study was found that evaluates structured physical-exam input (throat, abdomen, thorax findings) as a distinct variable in ED diagnosis. Closest evidence:

- **Mass General Brigham, JAMA Network Open.** Data given stepwise (basics, then exam, then labs). Final diagnosis correct over 90 percent with full data, but differential diagnosis was inappropriate in most cases; accuracy rose when labs and imaging were added.
- **Mass General Brigham exam-guidance study.** GPT-4 prompted to recommend which physical-exam maneuvers to perform given symptoms. This matches the expert's "boğazına bak, karnını muayene et" step.
- **Pediatric 2026 study.** Both LLMs and clinicians improved with extended clinical information.

Gap worth noting for the project: structured exam-finding capture and its marginal value to the differential is an open research question.

## 5. Recommending and interpreting tests

- **Imaging.** "Evidence Is All You Need" (arXiv 2409.19177) and its follow-up (PMC12322208) align LLM imaging orders with ACR Appropriateness Criteria and release the RadCases dataset. AJR 2024 found GPT-3.5 and GPT-4 8 to 24 percent less accurate than residents on binary "image or not" decisions, with a false-positive tendency; other work shows good ACR adherence with careful prompting.
- **Laboratory tests.** CCLM 2025 evaluated GPT-4o as a lab-test recommender on 15 simulated primary-care and ED cases; variability concentrated on conditional tests. Machine-learning models predict ED lab ordering from structured plus free-text EHR data (PMC13268631).
- **Registered trial NCT06902675** measures whether AI decision support changes imaging and lab orders per ED visit.

## 6. Does it help clinicians in practice?

- **Meta-analysis of five RCTs, about 12,657 participants (Appl Sci 2026).** AI decision support gave a small overall gain in clinician diagnostic accuracy (SMD 0.18). Emergency-medicine subgroup effect was essentially zero (SMD 0.01) versus 0.38 in radiology.
- **Implementation-gap review (Int J Emerg Med 2026).** Algorithmic performance does not translate reliably to bedside integration.
- **Triage.** Vilnius University conference data showed AI behind doctors and nurses on ED triage.
- **Karolinska trial NCT07766863** is studying how generative AI changes physicians' differentials in emergency care and notes the lack of large clinical studies.
- **Harms.** "Dr. GPT Will See You Now, but Should It?" (arXiv 2506.13805) catalogs benefits and harms on crowdsourced cases.

## 7. Older rule-based differential generators

Isabel and DXplain are the established non-LLM differential generators. Isabel was integrated into ED EHRs (T-System 2011, St. Louis Children's 2012) and flags "don't miss" diagnoses. Independent accuracy data date from 2000–2001 paediatrics (91 to 95 percent of expected diagnoses displayed). No modern independent ED outcome study was found. Useful as a design reference for the "must-exclude dangerous diagnoses first" pattern.

## 8. MCP and agentic architectures in healthcare

- **MCP-FHIR framework (arXiv 2506.13800).** Open-source MCP agent fetching FHIR resources for an LLM to summarize.
- **MCP-AI (arXiv 2512.05365).** Protocol-driven, auditable reasoning state stored per case; validated on two non-emergency use cases.
- **Springer 2026 perspective (s44250-026-00343-w).** MCP as the interface layer between multimodal LLMs and EHR, imaging, medication and lab systems.
- **FDB press release, Oct 2025.** First commercial MCP server for medication decision support.
- **awesome-healthcare-mcp-servers (GitHub).** Catalog of healthcare MCP servers with HIPAA and clinical-validity notes.
- No MCP server dedicated to emergency differential diagnosis was found. This project would be novel on that axis.

## 9. Design implications for Emergiency-Health-MCP

1. Model the state explicitly: current differential with probabilities, excluded diagnoses with the finding that excluded them, pending tests. Benchmarks show that free-form multi-turn prompting degrades reasoning.
2. Separate "what to ask or examine next" from "what to order next". MAI-DxO's panel pattern (hypothesis keeper, test chooser, challenger, cost checker) is the best-documented approach.
3. Put "can't-miss" emergency diagnoses first (Isabel pattern), then narrow by exclusion.
4. Ground test recommendations in published criteria (ACR Appropriateness Criteria for imaging, local lab protocols) rather than model memory; the AJR data show unguided models over-order.
5. Treat result interpretation as a separate tool with guideline grounding; the Nature Medicine abdominal study showed that this is where LLMs fail most.
6. Plan evaluation on real de-identified ED notes, ideally Turkish, with a specialist consensus reference. The Marmara protocol (NCT07632859) is a ready-made template.
7. Regulatory status is open. The tool is decision support for clinicians, not a device, and should be framed and logged as such.

## 10. Sources

- https://arxiv.org/abs/2506.22405 (Sequential Diagnosis with Language Models, SDBench / MAI-DxO)
- https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12158756/ (AMIE, Nature)
- https://arxiv.org/abs/2405.07960 (AgentClinic)
- https://arxiv.org/html/2501.14654v2 (MedAgentBench)
- https://arxiv.org/html/2408.10039v3 (MSDiagnosis)
- https://www.researchgate.net/publication/397195934_MediQ_Question-Asking_LLMs_and_a_Benchmark_for_Reliable_Interactive_Clinical_Reasoning (MediQ)
- https://www.eusem.org/news/904-press-release-chatgpt-performs-as-well-as-doctors-for-suggesting-the-most-likely-diagnoses-in-the-emergency-medicine-department (ten Berg 2023)
- https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11263899/ (Hoppe, JMIR 2024)
- https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11354035/ (Shah-Mohammadi, Diagnostics 2024)
- https://academic.oup.com/jamiaopen/article/8/5/ooaf119/8294036 (Niset, JAMIA Open 2025)
- https://pmc.ncbi.nlm.nih.gov/articles/PMC13195009/ (Zhejiang emergency internal medicine 2025)
- https://arxiv.org/pdf/2412.10849 (Brodeur, o1-preview physician reasoning)
- https://link.springer.com/article/10.1186/s12245-026-01324-9 (EM physicians vs LLMs, vignettes 2026)
- https://www.nature.com/articles/s44387-026-00078-2 (ED benchmarking 2026)
- https://clinicaltrials.gov/study/NCT07632859 (Marmara Turkish ED anamnesis trial)
- https://clinicaltrials.gov/study/NCT07766863 (Karolinska AI support in EM)
- https://clinicaltrials.gov/study/NCT06902675 (AI decision tool, ED ordering rates)
- https://www.mdpi.com/2076-3417/16/10/5146 (RCT meta-analysis, AI CDS diagnostic accuracy)
- https://link.springer.com/article/10.1186/s12245-026-01333-8 (implementation gap review)
- https://arxiv.org/pdf/2409.19177 (imaging orders aligned with ACR criteria)
- https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12322208/ (acute image ordering, RadCases)
- https://ajronline.org/doi/10.2214/AJR.24.32465 (AJR, LLM radiology decisions in ED)
- https://doi.org/10.1515/cclm-2025-0647 (LLMs as lab-test recommenders)
- https://pmc.ncbi.nlm.nih.gov/articles/PMC13268631/ (ML prediction of ED lab ordering)
- https://www.techtarget.com/healthtechanalytics/feature/LLMs-struggle-with-clinical-reasoning-study-finds (Nature Medicine 2024 abdominal study coverage)
- https://mobihealthnews.com/news/study-gpt-4-helps-clinicians-physical-exam-guidance (GPT-4 physical exam guidance)
- https://arxiv.org/pdf/2506.13805 (benefits and harms of LLM diagnosis)
- https://arxiv.org/pdf/2506.13800 (MCP-FHIR framework)
- https://arxiv.org/html/2512.05365 (MCP-AI)
- https://link.springer.com/article/10.1007/s44250-026-00343-w (MCP perspective, Springer 2026)
- https://www.fdbhealth.com/about-us/press-releases/2025-10-15-fdb-announces-first-mcp-server-for-ai-clinical-decision-support (FDB MCP server)
- https://github.com/rdmgator12/awesome-healthcare-mcp-servers (healthcare MCP catalog)
- https://about.ebsco.com/health-care/products/isabel.md (Isabel)
- https://tr.euronews.com/2026/05/05/arastirma-yapay-zeka-hekimleri-karmasik-tibbi-karar-gorevlerinde-geride-birakti (Turkish coverage of Harvard study)
- https://tr.euronews.com/health/2025/10/01/yapay-zeka-acil-servis-onceliklendirmesinde-doktor-ve-hemsirelerin-gerisinde (Vilnius triage study)
