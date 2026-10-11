# Göğüs ağrısı · EKARTE klinik protokolü (taslak v0.1, uzman incelemesi için)

Durum: Taslak. Her satır uzman onayı bekler. Sayısal değerler kaynaklı ve kaynağı yanında yazılıdır; kaynak yazmayan satırlar ders kitabı düzeyinde nitel bilgidir ve "nitel" diye işaretlidir. Bu dosya, sistemin bir ana şikâyet için taşıması gereken derinliğin örneğidir. Aynı yapı on ana şikâyetin her biri için üretilecektir.

Kapsam: 18 yaş üstü, travma dışı, akut (≤7 gün) göğüs ağrısı veya göğüste rahatsızlık ile acil servise başvuran hasta.

---

## 0. Önce yapılacaklar (sistem tetikler, hekim uygular)

| Zaman | Eylem | Dayanak |
|---|---|---|
| 0 dk | Triyaj: kırmızı alan ölçütleri (SKB <90, SpO₂ <90, bilinç değişikliği, devam eden şiddetli ağrı, aritmi) | Bakanlık triyaj tebliği |
| ≤10 dk | 12 derivasyon EKG, hekim yorumu | ESC 2020 NSTE-AKS, ESC 2023 AKS |
| 0 dk | Damar yolu, monitör, SpO₂; oksijen yalnızca SpO₂ <90 ise | ESC 2023 AKS |
| 0 dk | Her iki koldan tansiyon | Diseksiyon taraması (nitel, ADD-RS bileşeni) |
| İlk 15 dk | hs-troponin 0. saat örneği alınır (sonuç beklenmeden sorgu sürer) | ESC 0/1 saat algoritması |

Sistem bu adımları "yapıldı" işaretlenene kadar her turda en üstte tutar.

---

## 1. Kaçırılmaması gereken tanılar ve kapanma eşikleri

Her tanı için sistem bir "açık / zayıfladı / kapalı" durumu değil, bir **sonsal olasılık** ve bir **kapanma eşiği** tutar. Eşik, tanının kaçırılma maliyetine göre belirlenir. Tanı, sonsal olasılık eşiğin altına inince VE o tanı için tanımlı dışlama yolu tamamlanınca kapanır.

| Tanı | ICD-10 | Acilde ön olasılık (kaba) | Kapanma eşiği | Dışlama yolu (tamamlanması gereken) |
|---|---|---|---|---|
| Akut koroner sendrom (STEMI, NSTEMI, kararsız angina) | I20.0, I21 | %10–15 (göğüs ağrısı başvurularında, merkeze göre değişir) | <%1 MACE 30 gün | İskemik olmayan EKG + ESC 0/1 saat "rule-out" + HEART ≤3 |
| Pulmoner emboli | I26 | %2–5 | <%2 | PERC negatif (düşük ön olasılıkta) veya Wells ≤4 / YEARS + D-dimer eşik altı veya BTPA negatif |
| Aort diseksiyonu | I71.0 | %0,2–0,5 | <%0,5 | ADD-RS ≤1 + D-dimer <500 ng/mL (ADvISED) veya BT anjiyografi negatif |
| Tansiyon pnömotoraks / pnömotoraks | J93 | %1–2 | <%1 | Akciğer grafisi veya USG'de lung sliding mevcut, bilateral |
| Kardiyak tamponad | I31.9 | <%1 | <%0,5 | Yatak başı eko: efüzyon yok |
| Özofagus rüptürü (Boerhaave) | K22.3 | <%0,5 | <%0,5 | Kusma sonrası ani ağrı yok + mediastinal amfizem yok (grafi) |
| Perikardit / miyokardit | I30, I40 | %1–5 | kapalı sayılmaz, "aktif değil" | EKG tipik değil + troponin normal + sürtünme sesi yok |
| Pnömoni / plevral efüzyon | J18, J90 | %2–5 | aktif değil | Grafi temiz + ateş yok |

Ön olasılıklar literatür aralığıdır; ortak hastanenin kendi verisiyle kalibre edilir (Faz 1 çıktısı). Kaynak: Tintinalli 9. baskı "Chest Pain" bölümü ve Rosen's "Chest Pain" cardinal presentation; sayılar nitel aralıktır.

---

## 2. Yapılandırılmış sorgu bankası

Sistem soruları bu sırayla değil, **bilgi kazancına** göre seçer: açık kalan en maliyetli tanıyı en çok hareket ettiren soru önce gelir. Her sorunun etkilediği tanı ve varsa olabilirlik oranı (LR) yazılıdır. LR+ bulgunun varlığının tanı olasılığını kaç kat artırdığını, LR− yokluğunun kaç kat azalttığını söyler.

### 2.1 Zaman ve başlangıç

| # | Soru (hekime gösterilen Türkçe) | Yanıt tipi | Etkilediği tanı ve ağırlık | Kaynak |
|---|---|---|---|---|
| S1 | Ağrı ne zaman başladı? (saat:dakika) | zaman | Troponin zamanlaması: <3 saat ise "çok düşük" rule-out kullanılamaz; STEMI'de reperfüzyon penceresi | ESC 2020 |
| S2 | Ağrı aniden mi başladı, saniyeler içinde en şiddetli haline mi ulaştı? | evet/hayır | Diseksiyon: ani başlangıç LR+ 1,6; ani başlangıç **yokluğu** LR− 0,3. ADD-RS ağrı bileşeni | Klompas JAMA 2002 |
| S3 | Ağrı şu anda devam ediyor mu? | evet/hayır | Devam eden ağrı + nondiagnostik EKG → 15–30 dk'da EKG tekrarı | ESC 2023 |
| S4 | Ağrı aralıklı mı, sürekli mi? Her atak ne kadar sürüyor? | seçenek + süre | Saniyeler süren: AKS için atipik (nitel). >20 dk istirahat ağrısı: kararsız angina ölçütü | Tintinalli |

### 2.2 Karakter

| # | Soru | Yanıt | Etki | Kaynak |
|---|---|---|---|---|
| S5 | Ağrıyı nasıl tarif edersiniz: baskı/sıkışma, yırtılma/parçalanma, bıçak gibi keskin, yanma? | çoklu seçim | Baskı: AMI LR+ 1,3. Yırtılma/parçalanma: diseksiyon LR+ 10,8. Keskin: AMI LR− 0,3. | Swap & Nagurney JAMA 2005; Klompas 2002 |
| S6 | Nefes alırken veya öksürürken artıyor mu (plöretik)? | evet/hayır | AMI LR 0,2 (plöretik ise). Pnömotoraks, PE, perikardit, pnömoni lehine (nitel) | Swap 2005 |
| S7 | Pozisyonla değişiyor mu (öne eğilince azalıyor, sırtüstü artıyor)? | evet/hayır | AMI LR 0,3. Perikardit lehine (nitel, klasik bulgu) | Swap 2005 |
| S8 | Ağrı yerini değiştirdi mi (göğüsten sırta veya karna indi)? | evet/hayır | Diseksiyon: göç eden ağrı LR+ 1,1–7,6 (çalışmalar arası geniş aralık) | Klompas 2002 |
| S9 | Ağrı nereye yayılıyor? | çoklu: sol kol, sağ kol, her iki kol, çene, sırt, epigastrium, boyun | Sağ kol/omuz: AMI LR+ 4,7 (GA 1,9–12). Her iki kol: LR+ 4,1 (Swap 2005); Fanaroff 2015 güncellemesinde 2,6 (1,8–3,7). Sol kol: LR+ 2,3. Sırta, kürek kemikleri arasına: diseksiyon (nitel) | Swap 2005; Fanaroff JAMA 2015 |
| S10 | Şiddeti 0–10 arası kaç? Hayatınızın en şiddetli ağrısı mı? | sayı + evet/hayır | ADD-RS ağrı bileşeni ("şiddetli") | Rogers Circulation 2011 (ADD-RS) |

### 2.3 Tetikleyici ve eşlik eden

| # | Soru | Yanıt | Etki | Kaynak |
|---|---|---|---|---|
| S11 | Efor, yürüme veya merdivenle başladı mı ya da arttı mı? | evet/hayır | AMI LR+ 2,4; efor ilişkisi yoksa LR 0,8 | Swap 2005 |
| S12 | Göğüs duvarına bastırınca aynı ağrı oluyor mu? (muayenede doğrulanır) | evet/hayır | AMI LR 0,3 (palpasyonla tekrarlanıyorsa). Dikkat: tek başına AKS'yi dışlamaz | Swap 2005 |
| S13 | Terleme oldu mu? | evet/hayır | AMI LR+ 2,0 | Swap 2005 |
| S14 | Bulantı veya kusma oldu mu? Kusma ağrıdan **önce** mi başladı? | evet/hayır + sıra | Bulantı/kusma: AMI LR+ 1,9. Şiddetli kusma **sonrası** ani ağrı: Boerhaave uyarısı (nitel, kırmızı bayrak) | Swap 2005; Tintinalli |
| S15 | Nefes darlığı var mı? İstirahatte mi? | evet/hayır | PE, pnömotoraks, kalp yetersizliği, AKS eşdeğeri (nitel). Wells/PERC girdisi değil ama öncelik artırır | Tintinalli |
| S16 | Bayıldınız veya bayılacak gibi oldunuz mu? | evet/hayır | PE (senkop ile gelen PE mortalitesi yüksek), diseksiyon, aritmi, tamponad (nitel kırmızı bayrak) | ESC 2019 PE |
| S17 | Kan tükürdünüz mü? | evet/hayır | Wells PE +1; YEARS maddesi; PERC maddesi | Wells 2000; van der Hulle 2017; Kline 2004 |
| S18 | Çarpıntı var mı? | evet/hayır | Aritmi, PE (nitel) | — |
| S19 | Ateş, öksürük, balgam var mı? Kaç gündür? | evet/hayır + süre | Pnömoni, perikardit (viral prodrom), miyokardit (nitel) | Tintinalli |
| S20 | Son 2 haftada üst solunum yolu enfeksiyonu veya ishal geçirdiniz mi? | evet/hayır | Perikardit/miyokardit (nitel) | — |
| S21 | Bir bacakta şişlik, ağrı veya kızarıklık var mı? | evet/hayır | Wells PE "DVT klinik bulgusu" +3; YEARS maddesi; PERC maddesi | Wells 2000 |

### 2.4 Özgeçmiş ve risk

| # | Soru | Yanıt | Etki | Kaynak |
|---|---|---|---|---|
| S22 | Daha önce kalp krizi, stent, baypas veya bilinen koroner hastalık? | evet/hayır | HEART risk faktörü = 2 (aterosklerotik hastalık öyküsü); "önceki MI'a benziyor" LR+ 1,8 | Six 2008 HEART; Swap 2005 |
| S23 | Şeker hastalığı, yüksek tansiyon, kolesterol yüksekliği, sigara, obezite, ailede erken kalp hastalığı (erkek <55, kadın <65)? | çoklu | HEART risk faktörü: 1–2 faktör = 1, ≥3 = 2 | Six 2008 |
| S24 | Daha önce bacakta pıhtı veya akciğer embolisi? | evet/hayır | Wells +1,5; PERC maddesi | Wells 2000; Kline 2004 |
| S25 | Son 4 haftada ameliyat, alçı, 3 günden uzun yatak istirahati, 6 saatten uzun yolculuk? | evet/hayır | Wells +1,5 (immobilizasyon/cerrahi); PERC maddesi (cerrahi/travma) | Wells 2000 |
| S26 | Aktif kanser (tedavi altında veya son 6 ay)? | evet/hayır | Wells +1 | Wells 2000 |
| S27 | Östrojen içeren ilaç (doğum kontrol hapı, hormon tedavisi)? Gebelik veya 6 hafta içinde doğum? | evet/hayır | PERC maddesi (östrojen); gebelik/lohusalık PE riski (nitel); D-dimer yorumu gebelikte değişir | Kline 2004; ESC 2019 |
| S28 | Marfan, Ehlers-Danlos, biküspit aort, bilinen aort anevrizması, ailede aort hastalığı? Yakın zamanda aort/kalp girişimi? | çoklu | ADD-RS yüksek riskli durum bileşeni | Rogers 2011 |
| S29 | Kokain, amfetamin veya benzeri madde kullandınız mı (son 72 saat)? | evet/hayır | Vazospastik AKS, diseksiyon; beta bloker kaçınma uyarısı (nitel, kılavuz) | ACEP, Tintinalli |
| S30 | Kan sulandırıcı kullanıyor musunuz? | evet/hayır | Hemorajik komplikasyon, BT öncesi bilgi, antikoagülan kararı | — |
| S31 | Reflü, mide ülseri, yemekle ilişki, antasitle rahatlama? | evet/hayır | GÖRH/peptik (nitel). Dikkat: antasitle rahatlama AKS'yi dışlamaz (sık hata) | Tintinalli "pitfalls" |
| S32 | Son günlerde göğüs bölgesinde döküntü veya tek taraflı yanıcı ağrı? | evet/hayır | Herpes zoster (nitel) | — |

Toplam 32 soru; sistem tipik vakada 10–15'ini sorar, kalanı ya EKG/troponinden sonra gereksiz kalır ya da önceki yanıtlarla kapanır.

---

## 3. Fizik muayene maddeleri (hekim girer, sistem ağırlıklandırır)

| # | Bulgu | Nasıl girilir | Etki | Kaynak |
|---|---|---|---|---|
| M1 | Vitaller: SKB, DKB, nabız, SS, SpO₂, ateş | sayı | SKB ≤80: AMI LR+ 3,1. Nabız >100: Wells +1,5; PERC (<100 koşulu). SpO₂ <%95: PERC koşulu bozulur. Şok: ADD-RS bileşeni | Panju JAMA 1998 (Swap 2005'te aktarılan); Wells; Kline |
| M2 | İki kol arasında SKB farkı >20 mmHg | sayı/evet-hayır | Diseksiyon: nabız/basınç farkı LR+ 5,7 (Klompas 2002); Ohle 2018 meta-analizinde 2,7 (GA 0,7–9,8). ADD-RS muayene bileşeni | Klompas 2002; Ohle 2018; Rogers 2011 |
| M3 | Nabız defisiti (radial, femoral, karotis asimetrisi) | evet/hayır | Diseksiyon LR+ 5,7 (Klompas) / 2,7 (Ohle 2018). İki kaynak da: muayene diseksiyonu dışlayamaz | Klompas 2002; Ohle 2018 |
| M4 | Yeni diyastolik üfürüm (aort yetersizliği) | evet/hayır | Diseksiyon LR+ 1,4; ADD-RS bileşeni | Klompas 2002 |
| M5 | Fokal nörolojik defisit (göğüs ağrısıyla birlikte) | evet/hayır | Diseksiyon LR+ 6,6–33; ADD-RS bileşeni | Klompas 2002 |
| M6 | S3 | evet/hayır | AMI LR+ 3,2; kalp yetersizliğinde (Wang 2005) LR+ 11 | Panju 1998; Wang JAMA 2005 |
| M7 | Akciğerde ral (bilateral bazal) | evet/hayır | AMI LR+ 2,1; kalp yetersizliği LR+ 2,8 | Panju 1998; Wang 2005 |
| M8 | Boyun venöz dolgunluğu | evet/hayır | Tamponad, sağ kalp yetersizliği, tansiyon pnömotoraks (nitel) | — |
| M9 | Pulsus paradoksus >10 mmHg | sayı | Tamponad (nitel klasik) | — |
| M10 | Perikardiyal sürtünme sesi | evet/hayır | Perikardit (nitel, özgül ama duyarlı değil) | — |
| M11 | Solunum sesleri asimetrik / tek tarafta azalmış | evet/hayır | Pnömotoraks, efüzyon (nitel; duyarlılık düşük, grafi veya USG gerekir) | — |
| M12 | Subkütan amfizem (boyun, göğüs) | evet/hayır | Pnömotoraks, özofagus rüptürü (kırmızı bayrak) | — |
| M13 | Göğüs duvarı palpasyonla ağrı, aynı ağrı tekrarlanıyor | evet/hayır | AMI LR 0,3 (0,2–0,4); kas-iskelet lehine. Tek başına AKS'yi kapatmaz | Swap 2005; Panju 1998 |
| M14 | Tek taraflı bacak şişliği, baldır hassasiyeti, çap farkı >3 cm | evet/hayır + cm | Wells "DVT klinik bulgusu" +3; PERC | Wells 2000 |
| M15 | Epigastrik hassasiyet, defans | evet/hayır | Pankreatit, perfore ülser, kolesistit ayırımı (nitel) | — |
| M16 | Dermatomal veziküler döküntü | evet/hayır | Zoster (nitel) | — |
| M17 | Yatak başı USG (hekim yapıyorsa): perikardiyal efüzyon, lung sliding her iki hemitoraks, sağ ventrikül dilatasyonu, aort kökü çapı, flap, B-çizgileri | yapılandırılmış | Tamponad, pnömotoraks (lung sliding varlığı pnömotoraksı o alanda dışlar), PE (RV yükü), diseksiyon (kök >4 cm, flap), ödem | Tintinalli; ACEP POCUS politikası |

---

## 4. EKG yorum şeması (hekim işaretler, sistem sınıflar)

Sistem EKG'yi okumaz; hekimin işaretlediği bulguları sınıflar ve eksik bakılan derivasyonu hatırlatır.

| Bulgu | Ölçüt | Sonuç |
|---|---|---|
| STEMI | J noktasında ≥1 mm ST yükselmesi, 2 komşu derivasyon. V2–V3 için: erkek ≥40 yaş ≥2 mm, erkek <40 yaş ≥2,5 mm, kadın ≥1,5 mm | AKS **doğrulandı**, reperfüzyon yolu açılır; kalan tanılar ikincil |
| Posterior MI | V1–V3'te ST çökmesi + dik T; V7–V9'da ≥0,5 mm yükselme (erkek <40: ≥1 mm) | Sistem V7–V9 çekilmesini ister |
| Sağ ventrikül | İnferior STEMI'de V3R–V4R ≥0,5 mm (erkek <30 yaş: ≥1 mm) | Sistem V4R ister; nitrat uyarısı |
| Sgarbossa (LBBB / paced) | Konkordan STE ≥1 mm: 5 puan; V1–V3 konkordan STD ≥1 mm: 3; diskordan STE ≥5 mm: 2. ≥3 puan özgül. Modifiye Sgarbossa: diskordan STE / S dalgası oranı ≤ −0,25 | AKS eşdeğeri |
| De Winter | V1–V6'da J noktasında ≥1 mm yukarı eğimli ST çökmesi + uzun simetrik T; aVR'de STE | Proksimal LAD tıkanıklığı eşdeğeri; STEMI gibi yönet |
| Wellens | Ağrısız dönemde V2–V3'te bifazik (A) veya derin simetrik negatif (B) T; R dalgaları korunmuş; troponin normal olabilir | Kritik proksimal LAD; stres testi **kontrendike**; kardiyoloji |
| aVR | aVR'de ≥1 mm STE + yaygın ST çökmesi (≥6 derivasyon) | Sol ana / üç damar / yaygın subendokardiyal iskemi |
| Perikardit | Yaygın konkav STE, PR çökmesi, aVR'de PR yükselmesi, resiprokal değişiklik yok | Perikardit lehine |
| PE | Sinüs taşikardisi, S1Q3T3, V1–V4 T negatifliği, yeni sağ dal bloğu | Duyarlı değil; PE'yi dışlamaz |
| Normal EKG | — | AMI LR 0,1–0,3; AKS'yi tek başına kapatmaz | Swap 2005 |

Kural: Devam eden ağrı ve nondiagnostik EKG → 15–30 dakikada tekrar; ağrı karakteri değişirse tekrar.

---

## 5. Tetkik algoritmaları

### 5.1 hs-Troponin, ESC 0/1 saat (ESC 2020 NSTE-AKS)

| Analizör | Çok düşük (0. saat, ağrı >3 saat) | Düşük (0. saat) ve 1. saat delta | Yüksek (0. saat) veya 1. saat delta |
|---|---|---|---|
| Roche Elecsys hs-cTnT | <5 ng/L | <12 ng/L ve Δ <3 ng/L | ≥52 ng/L veya Δ ≥5 ng/L |
| Abbott Architect hs-cTnI | <4 ng/L | <5 ng/L ve Δ <2 ng/L | ≥64 ng/L veya Δ ≥6 ng/L |
| Siemens Centaur / Atellica hs-cTnI | <3 ng/L | <6 ng/L ve Δ <3 ng/L | ≥120 ng/L veya Δ ≥12 ng/L |
| Beckman Access hs-cTnI | <4 ng/L | <5 ng/L ve Δ <4 ng/L | ≥50 ng/L veya Δ ≥15 ng/L |
| Diğerleri (ESC Tablo 5) | Clarity 1 · Vitros 1 · Pathfast 3 · TriageTrue 4 | Clarity <2/Δ<1 · Vitros <2/Δ<1 · Pathfast <4/Δ<3 · TriageTrue <5/Δ<3 | Clarity ≥30/Δ≥6 · Vitros ≥40/Δ≥4 · Pathfast ≥90/Δ≥20 · TriageTrue ≥60/Δ≥8 |

0/2 saat varyantı: Elecsys 5 / 14 ve Δ<4 / ≥52 veya Δ≥10; Architect 4 / 6 ve Δ<2 / ≥64 veya Δ≥15. 99. persentil üst sınırı: Elecsys hs-cTnT 14 ng/L; Architect hs-cTnI 26,2 ng/L (kadın 15,6, erkek 34,2). Performans (APACE, TRAPID, High-STEACS): rule-out NPV ≈ %99,5–99,9, duyarlılık ≈ %99, hastaların yaklaşık %55–60'ı rule-out koluna düşer; rule-in PPV ≈ %70–75. Rule-out miyokart enfarktüsü içindir, kararsız anginayı kapatmaz.

Çıkış: "rule-out" (AKS sonsal olasılığı eşik altına iner, HEART ≤3 ile birlikte taburculuk yolu açılır), "observe" (3. saat troponin, eko, kardiyoloji), "rule-in" (NSTEMI, yatış). Hastanenin kullandığı analizör sistem kurulumunda seçilir; eşikler ona göre yüklenir. Kaynak: ESC 2020 NSTE-ACS Guideline, Tablo "0/1 h algorithm cut-offs". Diğer analizörler için kılavuz tablosu eklenecek.

Dikkat: Troponin yükselten AKS dışı nedenler (diseksiyon, PE, miyokardit, böbrek yetmezliği, sepsis, taşiaritmi). Yüksek troponin diseksiyonu **kapatmaz**; ADD-RS yüksekse BT önce.

### 5.2 HEART skoru (Six 2008; Backus 2013 doğrulama)

| Bileşen | 0 | 1 | 2 |
|---|---|---|---|
| History (öykü) | az şüpheli | orta | yüksek şüpheli |
| EKG | normal | nonspesifik repolarizasyon | belirgin ST sapması |
| Age | <45 | 45–64 | ≥65 |
| Risk faktörleri | yok | 1–2 | ≥3 veya aterosklerotik hastalık öyküsü |
| Troponin | normal | 1–3× ÜSL | >3× ÜSL |

0–3: 6 haftalık MACE %1,7 (Backus 2013, 2.440 hasta, 10 Hollanda acili; c-istatistik 0,83); 4–6: %16,6; 7–10: %50,1. Havuzlanmış: düşük risk duyarlılığı ≈ %96,7, özgüllük ≈ %47 (Van Den Berg & Body 2018); HEART ≤3 LR 0,20 (Fanaroff 2015). Kullanım: negatif troponinle birlikte rule-out; rule-in aracı değildir. "History" maddesinin değerlendiriciler arası uyumu zayıftır; bu yüzden sistem puanı tek tek sorgu yanıtlarından önerir, hekim onaylar (CLEOS deneyimi: yapılandırılmış öyküden türetilen HEART/EDACS/T-MACS duyarlılığı 0,91–0,97).

### 5.3 Pulmoner emboli yolu

1. PERC (Kline 2004; doğrulama 2008, 8.138 hasta): yaş <50, nabız <100, SpO₂ ≥%95, hemoptizi yok, östrojen yok, önceki VTE yok, tek taraflı bacak şişliği yok, son 4 haftada hastaneye yatış gerektiren cerrahi/travma yok. Sekizi de sağlanıyor **ve** hekim ön olasılığı düşük (<%15) → PE kapanır, D-dimer istenmez. Doğrulamada 45 günlük VTE/ölüm %1,0; duyarlılık %97,4, özgüllük %21,9. PROPER (Freund JAMA 2018) randomize çalışmasında kaçırılan PE %0,1.
2. PERC başarısızsa Wells (2000): DVT klinik bulgusu 3; PE en olası tanı 3; nabız >100: 1,5; ≥3 gün immobilizasyon veya 4 hafta içinde cerrahi: 1,5; önceki VTE: 1,5; hemoptizi: 1; malignite (6 ay içinde tedavi veya palyatif): 1. ≤4 "PE olası değil" → D-dimer; olası değil + negatif D-dimer: 3 aylık VTE %0,5 (Christopher, JAMA 2006). >4 → doğrudan BTPA. Alternatif: Revize Geneva (Le Gal 2006) tamamen nesneldir, gestalt maddesi yoktur.
3. D-dimer eşiği: standart 500 ng/mL FEU; >50 yaş için yaş × 10 ng/mL (ADJUST-PE, Righini JAMA 2014; yaşa göre ayarlanmış eşikle dışlananlarda 3 aylık VTE %0,3). YEARS (van der Hulle Lancet 2017; 3.465 hasta): üç madde (DVT bulgusu, hemoptizi, PE en olası) sıfırsa eşik 1000 ng/mL, bir ve üstü ise 500; BTPA %48 azalır, 3 aylık VTE %0,61. Dış doğrulamada (JTH 2020) yalnızca D-dimer ile yönetilen grupta ilk testte PE %1,2; D-dimer yaş ayarlı eşiğin üstünde ama <1000 ise dikkat. Birim uyarısı: 500 ng/mL FEU ≈ 250 ng/mL DDU; hastane laboratuvarının birimi kurulumda seçilir.
4. D-dimer eşik üstü → BTPA. Kontrast kontrendike / gebe → V/Q veya alt ekstremite venöz USG + klinik karar.

### 5.4 Aort diseksiyonu yolu

ADD-RS (Rogers 2011): üç kategori, her biri 1 puan, toplam 0–3.
- Yüksek riskli durum: Marfan, ailede aort hastalığı, bilinen aort kapak hastalığı, yakın aort girişimi, bilinen torasik anevrizma.
- Yüksek riskli ağrı: ani başlangıç, şiddetli, yırtıcı/parçalayıcı.
- Yüksek riskli muayene: nabız defisiti / SKB farkı, fokal nörolojik defisit + ağrı, yeni AY üfürümü, hipotansiyon/şok.

ADvISED (Nazerian Circulation 2018; 1.850 hasta, 241 akut aort sendromu): ADD-RS ≤1 ve D-dimer <500 ng/mL → diseksiyon kapanır; duyarlılık %98,8, NPV %99,7, LR− 0,02, kaçırma oranı %0,3. Tek başına D-dimer <500: duyarlılık %96,7, özgüllük %64. Gözlemsel çalışma, randomize doğrulaması yok. ADD-RS ≥2 veya D-dimer ≥500 → EKG kapılı BT anjiyografi (toraks + abdomen). Rogers 2011 (IRAD, 2.538 hasta): ADD-RS ≥1 duyarlılığı %95,7; diseksiyonların %4,3'ü 0 puan alır. Mediasten genişliği grafide: LR+ 2,0 (Klompas) / 3,4 (Ohle 2018), yokluğu LR− 0,3; grafi normal olsa diseksiyon kapanmaz.

### 5.5 Diğer tetkikler ve ne zaman

| Tetkik | Ne zaman | Yorum kuralı |
|---|---|---|
| PA akciğer grafisi | Tüm göğüs ağrılarında ilk saat | Pnömotoraks, infiltrasyon, efüzyon, mediasten >8 cm, pnömomediastinum |
| Yatak başı eko | Hipotansiyon, JVD, nefes darlığı, troponin yüksek | Efüzyon/tamponad, duvar hareket bozukluğu, RV dilatasyonu, aort kökü |
| D-dimer | Yalnızca 5.3 ve 5.4 kapılarından geçince | Kapı dışı D-dimer isteme = gereksiz BT'nin ana kaynağı |
| BTPA | Wells >4 veya D-dimer eşik üstü | Kreatinin, kontrast alerjisi, gebelik kontrolü |
| BT aortografi (EKG kapılı) | ADD-RS ≥2 veya D-dimer ≥500 + ADD-RS 1 | Toraks + abdomen, flap, yalancı lümen |
| Lipaz | Epigastrik ağrı / sırta yayılan ağrı | >3× ÜSL pankreatit |
| Hemogram, kreatinin, elektrolit, glukoz | Troponin ile aynı örnekte | Kontrast öncesi kreatinin; anemi (iskemi tetikleyici) |
| BNP / NT-proBNP | Nefes darlığı, ral, ödem | NT-proBNP: <300 pg/mL dışlar (duyarlılık %93,9, NPV %98); rule-in yaşa göre <50 yaş >450, 50–75 >900, >75 >1800 pg/mL (ICON, ICON-RELOADED). BNP <100 pg/mL LR− 0,11 (Wang 2005) |
| Laktat | Şok, hipotansiyon | >2 mmol/L hipoperfüzyon, >4 ağır |
| Toksikoloji | Madde şüphesi | Kokain: beta bloker kaçın (nitel kılavuz) |

---

## 6. Dışlama mantığı, tanı tanı

| Tanı | Kapatır | Doğrular | Asla tek başına kapatmaz |
|---|---|---|---|
| AKS | İskemik olmayan EKG + 0/1 saat rule-out (ağrı >3 saat ise 0. saat çok düşük yeterli) + HEART ≤3 | STEMI ölçütleri; rule-in troponin; Wellens/de Winter | Normal tek EKG; antasitle rahatlama; palpasyonla ağrı; genç yaş |
| PE | PERC 8/8 + düşük ön olasılık; veya Wells ≤4 ve D-dimer eşik altı; veya BTPA negatif | BTPA pozitif; yüksek olasılık V/Q | Normal SpO₂; normal EKG; normal grafi |
| Diseksiyon | ADD-RS ≤1 + D-dimer <500; veya BT anjiyo negatif | BT'de flap | Normal grafi; normal troponin; simetrik nabız |
| Pnömotoraks | Grafi negatif veya bilateral lung sliding | Grafi / USG | Normal solunum sesleri |
| Tamponad | Eko'da efüzyon yok | Eko efüzyon + kollaps | Normal EKG |
| Boerhaave | Kusma sonrası ani ağrı yok + grafide pnömomediastinum/efüzyon yok | BT/özofagogram | — |

---

## 7. Karar ve taburculuk

| Durum | Öneri | Dayanak |
|---|---|---|
| STEMI / eşdeğeri | PKG merkezi: kapı-balon ≤90 dk; PKG yoksa ve nakil >120 dk: fibrinolitik ≤10 dk, sonra sevk. 112 ile koordinasyon | ESC 2023 AKS |
| NSTEMI (rule-in) | Yatış, antitrombotik tedavi kararı kardiyoloji ile; çok yüksek risk ölçütleri varsa <2 saat invaziv | ESC 2023 |
| Observe | 3. saat troponin, eko, HEART 4–6 → gözlem/yatış | ESC 2020 |
| AKS rule-out + HEART ≤3 + PE ve diseksiyon kapalı | Taburculuk; 72 saat içinde kardiyoloji/poliklinik; gerekirse ayaktan stres görüntüleme veya koroner BT | ESC 2020; HEART literatürü |
| Açık kritik tanı varken | Sistem taburculuk önermez; hekim onayı ve gerekçe zorunlu | EKARTE güvenlik kuralı |

Taburculuk gerekçesi otomatik üretilir (Türkçe): "EKG iskemik değil; hs-cTnT 0 saat 4 ng/L (ağrı 5 saat); HEART 2; PERC negatif; ADD-RS 0 ve D-dimer 310. AKS, PE, diseksiyon kapandı. 72 saat içinde kontrol."

---

## 8. Sık hatalar (sistem uyarı verir)

1. Antasit veya nitratla rahatlamayı tanısal saymak.
2. Palpasyonla ağrı tekrarlanınca AKS'yi kapatmak (LR 0,3, kapatmaz).
3. Tek normal EKG ile AKS'yi kapatmak.
4. Yüksek troponinde diseksiyonu düşünmeden antikoagülan başlamak.
5. Kapı dışı D-dimer istemek (yanlış pozitif BT zinciri).
6. Ağrı <3 saat iken tek troponinle taburcu etmek.
7. Wellens paternini "nonspesifik T değişikliği" diye geçmek.
8. Posterior derivasyon çekmeden V1–V3 ST çökmesini "iskemi" diye bırakmak.
9. Kokain kullanıcısında beta bloker.
10. Genç kadın ve diyabetikte atipik prezentasyonu küçümsemek.

---

## 9. Kaynaklar (bu protokolde kullanılan)

- Swap CJ, Nagurney JT. Value and limitations of chest pain history in the evaluation of patients with suspected acute coronary syndromes. JAMA 2005;294:2623–2629.
- Klompas M. Does this patient have an acute thoracic aortic dissection? JAMA 2002;287:2262–2272.
- Rogers AM et al. Sensitivity of the aortic dissection detection risk score. Circulation 2011;123:2213–2218.
- Nazerian P et al. Diagnostic accuracy of the ADD-RS plus D-dimer (ADvISED). Circulation 2018;137:250–258.
- Six AJ, Backus BE, Kelder JC. Chest pain in the emergency room: value of the HEART score. Neth Heart J 2008;16:191–196.
- Backus BE et al. A prospective validation of the HEART score. Int J Cardiol 2013;168:2153–2158.
- Collet JP et al. 2020 ESC Guidelines for NSTE-ACS. Eur Heart J 2021;42:1289–1367 (0/1 saat algoritması ve analizör eşikleri).
- Byrne RA et al. 2023 ESC Guidelines for acute coronary syndromes. Eur Heart J 2023;44:3720–3826.
- Thygesen K et al. Fourth universal definition of myocardial infarction. Eur Heart J 2019;40:237–269 (STEMI EKG ölçütleri).
- Wells PS et al. Derivation of a simple clinical model to categorize patients' probability of PE. Thromb Haemost 2000;83:416–420.
- Kline JA et al. Clinical criteria to prevent unnecessary diagnostic testing in ED patients with suspected PE (PERC). J Thromb Haemost 2004;2:1247–1255.
- Righini M et al. Age-adjusted D-dimer cutoff levels to rule out PE (ADJUST-PE). JAMA 2014;311:1117–1124.
- van der Hulle T et al. Simplified diagnostic management of suspected PE (YEARS). Lancet 2017;390:289–297.
- Konstantinides SV et al. 2019 ESC Guidelines on acute pulmonary embolism. Eur Heart J 2020;41:543–603.
- Sgarbossa EB et al. NEJM 1996;334:481–487; Smith SW et al. Ann Emerg Med 2012;60:766–776 (modifiye Sgarbossa).
- de Winter RJ et al. NEJM 2008;359:2071–2073.
- Rhee TM et al. / de Zwaan C et al. Am Heart J 1982;103:730–736 (Wellens).
- Januzzi JL et al. NT-proBNP in the ED (ICON). Eur Heart J 2006;27:330–337; ICON-RELOADED, JACC 2018.
- Panju AA et al. Is this patient having a myocardial infarction? JAMA 1998;280:1256–1263.
- Fanaroff AC et al. Does this patient with chest pain have acute coronary syndrome? JAMA 2015;314:1955–1965.
- Ohle R et al. Clinical examination for acute aortic dissection: a systematic review and meta-analysis. Acad Emerg Med 2018;25:397–412.
- Wang CS et al. Does this dyspneic patient in the ED have congestive heart failure? JAMA 2005;294:1944–1956.
- Kline JA et al. Prospective multicenter evaluation of the PERC rule. J Thromb Haemost 2008;6:772–780; Freund Y et al. PROPER trial. JAMA 2018;319:559–566.
- van Belle A et al. Christopher Study. JAMA 2006;295:172–179.
- Le Gal G et al. Revised Geneva score. Ann Intern Med 2006;144:165–171.
- Ayrıntılı derleme ve kaynak bağlantıları: `docs/clinical/decision-rules.md`.
- Tintinalli's Emergency Medicine, 9. baskı, "Chest Pain" ve "Acute Coronary Syndromes" bölümleri. Rosen's Emergency Medicine, 10. baskı, "Chest Pain" cardinal presentation.
- Bakanlık triyaj tebliği (13.05.2022, RG 31952).

Doğrulanması gerekenler (uzman): ön olasılık aralıkları, Siemens/Beckman eşikleri (ESC tablosundan aktarıldı, hastane analizörüyle eşleştirilecek), Türkiye'de kullanılan D-dimer birimi (FEU ng/mL mi, DDU mu; eşik birime göre yarıya iner).
