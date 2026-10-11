# What an MCP-style emergency decision-support system can do in Turkish emergency services

Date: 2026-10-11. Companion to `literature-review.md`. This note maps the expert's workflow (complaints + physical exam → exclusion-driven differential → test ordering → result interpretation) onto the Turkish emergency-care system and proposes how an MCP (Model Context Protocol) server could fit into it. Facts are from a web search on the date above; items marked "unverified" could not be confirmed against a primary source.

## 1. Why Turkey is a strong setting for this

- **Volume.** About 150 million emergency department (ED) visits in 2023, roughly 177 per 100 people per year, versus an OECD average near 27. Figures for 2024 and 2025 were requested in parliament but not published.
- **Case mix.** An ED professor quoted in the press estimates about 70 percent of visits are green-zone (low acuity), with red-zone cases at 1 to 2 percent. Unverified and undated, but consistent with the volume data.
- **Staffing.** Many state-hospital EDs are run by general practitioners and residents rather than emergency medicine specialists, with reports of one physician seeing 300 patients a day. Decision support that helps a non-specialist exclude dangerous diagnoses quickly is where the value is.
- **Digital infrastructure already exists.** Every hospital runs an HBYS (hospital information system) that must integrate with USS/e-Nabız (national health data), MEDULA (SGK reimbursement), and SKRS (national code lists). Decision support services called from HBYS through e-Nabız already exist for transfusion. This is the integration pattern to reuse.
- **Ministry direction.** TÜSEB hosts a Türkiye Sağlık Veri Araştırmaları ve Yapay Zekâ Uygulamaları Enstitüsü with clinical decision support in its remit. The Ministry has announced RADİS, a guideline-based imaging decision support system developed with ASELSAN (press report, no technical source found, unverified).
- **A ready evaluation template.** Marmara University Pendik registered a 600-case retrospective study of GPT-4o and Claude Sonnet on Turkish ED anamnesis notes (NCT07632859), using a three-specialist ICD-10 consensus as the reference. Listed as completed, no results yet.

## 2. Where the tool sits in the patient flow

```
112 / ASOS (prehospital)  ─┐
Walk-in registration       ├─► Triage (red / yellow / green, before registration per 2018 tebliğ)
                           │
                           ▼
              Physician encounter in HBYS
   ┌──────────────────────────────────────────────┐
   │  MCP server: emergency differential engine   │
   │  1. intake: complaints, vitals, exam findings │
   │  2. differential + can't-miss list            │
   │  3. next question / next exam maneuver        │
   │  4. test and imaging recommendation           │
   │  5. result interpretation, differential update│
   │  6. disposition suggestion + audit log        │
   └──────────────────────────────────────────────┘
                           │
                           ▼
    Orders → LIS / PACS → results back → HBYS → USS/e-Nabız, MEDULA
```

The clinician stays in HBYS. The MCP server is an assistant that an HBYS vendor's AI client (or a standalone clinician client) calls. It never writes orders itself in phase 1; it proposes, the physician approves in HBYS.

## 3. Proposed MCP tool surface

| Tool | Input | Output | Turkish-specific grounding |
|---|---|---|---|
| `start_encounter` | age, sex, triage colour, chief complaint (Turkish free text) | encounter id, initial differential with can't-miss diagnoses flagged | Turkish complaint vocabulary, SKRS code lists |
| `add_findings` | structured physical exam findings by system (boğaz, toraks, batın, nöro, cilt), vitals | updated differential, list of diagnoses excluded and the finding that excluded each | Finding schema mapped to USVS (national data dictionary) elements |
| `next_step` | encounter id | ranked suggestions: ask this question, examine this, or order this test; each with the hypothesis it discriminates and estimated cost | SUT (Sağlık Uygulama Tebliği) test codes and prices, Ministry rational test-request interval rules |
| `recommend_tests` | encounter id | lab panel and imaging with justification | ACR Appropriateness Criteria plus Turkish radiology society guidance; RADİS alignment if an API exists |
| `interpret_results` | lab values, imaging report text, ECG description | updated differential, red flags, suggested consults | Turkish lab reference ranges, Turkish radiology report language |
| `disposition` | encounter id | discharge, observe, admit, consult, transfer, with required exclusions satisfied | Ministry ED tebliğ categories, ASOS transfer workflow |
| `explain` | any step | reasoning trace in Turkish for the chart and for audit | Required for liability under Turkish malpractice rules |

Every tool returns its reasoning in Turkish and logs inputs and outputs to an append-only audit store, because Turkish law assigns final responsibility to the physician and the institution.

## 4. Integration surfaces in the Turkish stack

1. **HBYS.** There is no single HBYS. Target the SBYS registry requirements and offer a thin client that any vendor can embed. HL7 v3 and XML web services are the Ministry-accepted standards; FHIR R4 is claimed by some integrators for e-Nabız but adoption is partial (unverified). Plan for both: a FHIR R4 facade for new systems and an XML adapter for legacy ones.
2. **USS / e-Nabız.** The hospital sends data to USS, not directly to e-Nabız. A decision service pattern already exists where HBYS calls an e-Nabız service and receives a report (used for transfusion decision support). If the Ministry agrees, the MCP server could be exposed the same way, which solves distribution to all hospitals at once.
3. **SKRS.** National code lists for ICD-10, procedures, drugs and lab tests. The server must speak SKRS codes so that its outputs drop straight into HBYS order and diagnosis screens.
4. **MEDULA / SUT.** Reimbursement rules define which tests are payable in the ED and at what interval. Encoding these turns "which test" into "which payable test", which clinicians and administrators both need.
5. **112 / ASOS.** Prehospital case data (vitals, ECG, complaint) can pre-populate the encounter so the differential is already running when the ambulance arrives. HBYS–ASOS integration is on the Ministry's agenda but its status per hospital is unclear.
6. **LIS / PACS.** Results return through HBYS; the server reads them via the same adapter. Imaging reports are free text in Turkish, so the interpretation tool needs Turkish radiology language.

## 5. Turkish-specific model and data requirements

- **Language.** Anamnesis is written in Turkish with heavy abbreviation and local idiom. Evaluate Turkish-note performance explicitly; the Marmara protocol is the only such study and its results are pending. Prompting in Turkish with Turkish clinical vocabulary, not translation, should be the default.
- **Case mix.** Weight the differential toward Turkish ED epidemiology: very high green-zone volume, so the tool must be fast at safe discharge, not only at rare diagnoses.
- **Triage colours.** Use the Ministry's red, yellow, green and "Yeşil Alan 1" categories as the acuity input, since every ED already assigns them before registration.
- **Can't-miss first.** Follow the Isabel pattern: for each chief complaint, enumerate dangerous diagnoses that must be excluded before green-zone discharge, and show which exclusions are still open.
- **Local references.** Turkish lab reference ranges, Turkish drug names, local antibiotic resistance patterns, and Ministry clinical protocols.

## 6. Regulatory and legal frame

- **KVKK (data protection).** Health data is special-category data. The 2024 amendment (8th judicial package, effective 1 June 2024) allows processing without explicit consent on specific legal bases, including protection of life when the person cannot consent, and eases cross-border transfer subject to adequacy decisions that were still pending at the time of the sources. Practical consequence: host inference inside Turkey or de-identify before any foreign API call; keep the raw note inside the hospital network.
- **TİTCK (medical device regulation).** TİTCK follows the EU MDR definition of medical device software and the MDCG 2019-11 decision flow. Software that produces information used for diagnosis or treatment decisions for an individual patient is likely a medical device, probably class IIa or higher. A pure information-retrieval tool is not. Plan from the start for medical device qualification, which means a quality management system, clinical evaluation, and post-market surveillance. Confirm the exact class with a regulatory consultant; no AI-specific TİTCK guidance was found.
- **Liability.** No AI-specific law exists. Responsibility stays with the physician and institution, which is why the explanation and audit tools above are mandatory, not optional.
- **Ministry approval.** Any connection to USS or e-Nabız requires Ministry agreement. Approach through TÜSEB's AI institute or SBSGM (Sağlık Bilgi Sistemleri Genel Müdürlüğü).

## 7. Evidence plan, Turkish context

1. **Retrospective, silent.** Replicate the Marmara design on your partner hospital's de-identified ED notes: 500 to 1,000 cases, specialist consensus reference, report chapter-level and top-3 accuracy, and separately score can't-miss sensitivity. Add exam findings as a controlled variable, since no published study has done so.
2. **Sequential simulation.** Build a Turkish SDBench-style set: 100 to 200 real ED cases converted to stepwise scripts where the server must ask or order one thing at a time. Score accuracy and test cost in SUT prices. This is the only way to validate the exclusion loop the expert described.
3. **Shadow mode in one ED.** Run alongside physicians without showing output; compare recommendations with actual orders and discharge diagnoses. This also produces the data needed for TİTCK clinical evaluation.
4. **Prospective, physician-in-the-loop.** Randomize shifts or physicians; outcomes are time to disposition, test count per visit, missed-diagnosis return visits within 72 hours. Register the trial; the Karolinska and Marmara registrations show the format.

## 8. Phased roadmap

| Phase | Deliverable | Depends on |
|---|---|---|
| 0, now | MCP server with the seven tools, Turkish prompts, SKRS and SUT code tables, audit log, synthetic cases | Nothing external |
| 1 | Retrospective validation on partner hospital notes; Turkish sequential benchmark | Hospital ethics approval, de-identified data |
| 2 | HBYS adapter (FHIR facade + XML), read-only shadow mode in one ED | One HBYS vendor, hospital IT |
| 3 | TİTCK qualification file, KVKK impact assessment, on-premise or Turkish-cloud inference | Regulatory consultant |
| 4 | Ministry integration via e-Nabız decision-service pattern; 112/ASOS pre-population | Ministry, TÜSEB institute |

## 9. Main risks

- **Over-ordering.** Imaging studies show unguided models order more than residents. Guideline grounding and SUT cost display are the mitigation.
- **Performance on Turkish text.** Unknown until Marmara reports; test early.
- **Automation bias in a high-volume, junior-staffed ED.** Present exclusions and open questions, never a single answer; require explicit physician acknowledgement for discharge of patients with open can't-miss items.
- **Regulatory delay.** Medical device qualification can take longer than the software build. Start the file in phase 1.
- **Vendor fragmentation.** Dozens of HBYS products. A Ministry-level service (e-Nabız pattern) is the only route that avoids per-vendor integration.

## 10. Sources

- https://www.cnnturk.com/turkiye/turkiyede-acil-servislere-yilda-100-milyon-basvuru-yapiliyor-598894 (ED volume, green-zone share)
- https://www.birgun.net/haber/saglikta-acil-alarm-583484 (2023 visits, per-capita vs OECD)
- https://www.cumhuriyet.com.tr/turkiye/nufustan-fazla-basvuru-acil-servislere-150-milyonu-askin-hasta-kaydi-2163322 (2023 visits)
- https://cdn.tbmm.gov.tr/KKBSPublicFile/D28/Y3/T7/WebOnergeMetni/9b0acca2-ed83-4fba-8dba-5e9f803ab38b.pdf (parliamentary question, visit figures)
- https://bianet.org/haber/saglikta-donusum-manzarasi-gunde-300-hastaya-bakan-acil-hekimi-265965 (ED workload)
- https://www.cumhuriyet.com.tr/saglik/saglikta-kriz-derinlesiyor-uzman-doktor-bulunamiyor-2106059 (specialist shortage)
- https://www.trthaber.com/haber/saglik/turkiye-acil-tipta-ileri-seviyede-924230.html (emergency medicine workforce)
- https://www.aa.com.tr/tr/saglik/saglik-bakani-memisoglu-klinik-alanda-yapay-zeka-uygulamalari-ile-bircok-surecte-yeni-yontemleri-hayata-geciriyoruz/3755362 (Ministry AI projects, RADİS)
- https://www.lexpera.com.tr/resmi-gazete/metin/turkiye-saglik-veri-arastirmalari-ve-yapay-zeka-uygulamalari-enstitusunun-yapilanmasi-ve-1 (TÜSEB AI institute regulation)
- https://www.hanyaloglu-acar.av.tr/malpraktis-tazminat/saglikta-yapay-zeka-hukuki-cerceve (legal frame, liability)
- https://ininia.com/blog/hbys-nedir-hastane-bilgi-yonetim-sistemi-uss-entegrasyonu (HBYS, USS, MEDULA, SKRS architecture)
- https://ininia.com/blog/e-nabiz-entegrasyonu-teknik-rehber (e-Nabız FHIR R4 claim, unverified)
- https://afyonluoglu.org/PublicWebFiles/Reports-TR/Veri%20Sozlugu/2014-USVS%20Ulusal%20Sa%C4%9Fl%C4%B1k%20Veri%20S%C3%B6zl%C3%BC%C4%9F%C3%BC%20v2_2.pdf (USVS data dictionary, HL7 v3)
- https://webupload.gazi.edu.tr/upload/289/2024/2/26/8a3c06a2-3101-436d-afa3-48e02ef04384-hky_kullanici_klavuzu_v3.pdf (e-Nabız decision-service pattern, transfusion)
- https://www.saglikaktuel.com/d/file/15140,akilci-laboratuvar-kullanimi-aek42422915pdf.pdf (rational test-request rules)
- https://www.alomaliye.com/2018/02/20/yatakli-saglik-tesisleri-acil-servis-hizmetleri/ (triage colour rules, 2018 amendment)
- https://www.lexpera.com.tr/mevzuat/tebligler/yatakli-saglik-tesislerinde-acil-servis-hizmetlerinin-uygulama-usul-ve-esaslari-hakkinda-teblig (ED communiqué, 2022)
- https://www.medikalakademi.com.tr/netas-turkiyede-hastane-oncesi-saglik-sistemini-asos-ile-dijitallestiriyor/ (ASOS scope)
- https://www.urfanatik.com/sanliurfa-8-bolge-18-askom-toplantisina-ev-sahipligi-yapti (HBYS–ASOS integration on agenda)
- https://cottgroup.com/tr/blog/kvkk-gdpr/item/8-yargi-paketi-kapsaminda-6698-sayili-kisisel-verilerin-korunmasi-kanununda-yapilan-degisiklikler-ve-yansimalari (KVKK 2024 amendment)
- https://www.sozcu.com.tr/yurt-disina-veri-aktariminin-onu-acildi-1-haziran-da-yururluge-girecek-p34084 (KVKK cross-border transfer)
- https://titck.gov.tr/storage/Archive/2024/contentFile/infographic_TR_d4007cb7-8023-4629-8474-67da81aa1cf5.pdf (TİTCK software-as-medical-device decision flow)
- https://clinicaltrials.gov/study/NCT07632859 (Marmara Turkish ED LLM study)
- https://avesis.akdeniz.edu.tr/yayin/ab5ac682-9eb3-4897-b847-8d20f4891946/radyolojik-tetkik-seciminde-klinisyenler-icin-bir-karar-destek-sistemi-ornegi (Turkish ACR-based imaging decision support, RADDES)
