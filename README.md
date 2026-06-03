# Kā Latvijas uzņēmums parādās ChatGPT, Perplexity un Google AI atbildēs

Praktisks ceļvedis par AI un LLM redzamību latviešu valodā. Balstīts reālā darbā ar Latvijas mājaslapām — ne teorija, bet soļi, kas strādā.

Autors: **Modris Šķēls** — 30 gadu mārketinga pieredze, [skels.lv](https://skels.lv). Pirmais Latvijā prezentēja Google reklāmu 2007. gadā.

> Vajag pārbaudīt, vai ChatGPT zina tieši tavu uzņēmumu? Bezmaksas AI redzamības audits: **[skels.lv](https://skels.lv)**

---

## 1. Galvenais — AI meklētāji neizmanto Google tāpat kā parastā meklēšana

Lielākā daļa uzņēmumu domā, ka pietiek ar Google SEO. Tā nav taisnība AI meklēšanā — katram dzinējam ir savs ceļš, kā atrod lapas.

| Platforma | Kā atrod lapas |
|---|---|
| ChatGPT (search) | Savs robots + indekss; daļēji Bing |
| Perplexity | Savs indekss + robots; daļēji Bing |
| Microsoft Copilot | Bing |
| Google Gemini / AI Overviews | Google |

Tradicionāls Google SEO sedz tikai vienu no tiem (Gemini). Pilna AI redzamība prasa trīs lietas paralēli: (1) atļaut visiem AI robotiem lasīt lapu, (2) būt gan Bing, gan Google indeksā, (3) strukturēti dati. Vairums Latvijas uzņēmumu neko no tā nav sakārtojuši — tāpēc AI meklētāji tos vienkārši neredz.

---

## 2. 7 soļu kontrolsaraksts

| # | Solis | Laiks | Ko dod |
|---|---|---|---|
| 1 | `robots.txt` ar `Allow` rindām GPTBot, ClaudeBot, PerplexityBot, Google-Extended | 1 min | Pamats — bez tā AI roboti lapu neredz |
| 2 | Schema.org JSON-LD (Person, Organization, Service, FAQPage, Article) | 2–4 h | Strukturēti fakti, ko AI citē |
| 3 | `llms.txt` un `llms-full.txt` lapas saknē | 30 min | AI robotiem domāts lapas teksta kopsavilkums |
| 4 | Bing Webmaster + IndexNow ar automātisku ping pēc katras publicēšanas | 30 min | Sedz Copilot + stiprina Bing pusi |
| 5 | Google Business / Bing Places profils ar vietnes lauku | 30 min + verifikācija | Zināšanu paneļa savienojums vārds → lapa |
| 6 | Ārējās atsauces (`sameAs`) — LinkedIn, Google profils, GitHub, Crunchbase | 1–3 h | Stiprina entītes datus |
| 7 | Sitemap iesniegts + Google Search Console "Request Indexing" | 5 min | Paātrina indeksāciju no nedēļām uz dienām |

---

## 3. Bing — neaizmirstamais solis

Uzņēmums ar aktīvu Google SEO bieži pieņem, ka viss ir kārtībā. Bet Microsoft Copilot balstās uz Bing, un, ja tava lapa Bing indeksā nav, tad tur tevi neredz. Bing nav vienīgais (ChatGPT un Perplexity lieto pašu indeksus), bet to sakārtot ir ātri un to bieži aizmirst.

Soļi:

1. Atver [bing.com/webmasters](https://www.bing.com/webmasters)
2. Pievieno un verificē savu lapu
3. Iesniedz sitemap (vai apakš-sitemap tieši — sk. 6. sadaļu)
4. Uzliec IndexNow atslēgas failu (32 simbolu virkne) lapas saknē
5. Iestati automātisku IndexNow ping pēc katras publicēšanas (piem. caur deploy skriptu vai CI workflow)

IndexNow paziņo Bing par jaunajām un atjaunotajām lapām dažu minūšu laikā, nevis gaida, kamēr robots pats atnāks.

---

## 4. Biznesa profili 3 vidēs — savienojums vārds ↔ lapa

Biznesa profils ar **vietnes lauku** ir vienīgā vieta, kur meklētāji strukturēti pieraksta savienojumu "persona vai uzņēmums → mājaslapa". Tas ir pamats zināšanu panelim, ko AI izmanto kā ground truth.

| Platforma | Adrese | Ko sasniedz | Laiks |
|---|---|---|---|
| Google Business Profile | [business.google.com](https://business.google.com) | Gemini + Google meklēšana | 30 min + verifikācija |
| Bing Places for Business | [bingplaces.com](https://www.bingplaces.com) | Microsoft Copilot + Bing rezultāti | 5 min ar "Import from Google" |
| Apple Maps Connect | [mapsconnect.apple.com](https://mapsconnect.apple.com) | Siri + Apple Maps + Spotlight | 15 min |

Praktisks triks: **Bing Places automātiski pārņem Google profila datus** ar funkciju "Import from Google". Tāpēc nav jāveic uzstādīšana trīs reizes — Google profils ir pamats, pārējos divus tikai pievieno.

Yandex Business der tikai tad, ja mērķē uz krievvalodīgo auditoriju (zem 2% no Latvijas tirgus).

---

## 5. Kā izmērīt sākuma stāvokli

Pirms un pēc darba pārbaudi 4 platformas ar vienādiem jautājumiem.

Vērtēšana:

- **0 — nezina:** atbild "es nezinu šādu uzņēmumu" vai dod nesaistītu info
- **1 — zina ar ārējiem avotiem:** citē LinkedIn vai ziņas, bet ne pašu lapu
- **2 — citē lapu tieši:** atbildē iekļauj URL vai precīzu strukturētu info

3 jautājumi katram uzņēmumam: (a) zīmola vārds, (b) "nozare + pilsēta", (c) konkurents vai niša. Testē visās 4 platformās, saglabā ekrānuzņēmumus, atkārto pēc 30/60/90 dienām. Tipiski sākumā rezultāts ir 0/4 — un tas pats par sevi parāda problēmu skaidri.

---

## 6. Biežākās kļūdas no prakses

**"Discovered – currently not indexed" Google Search Console.** Tas ir normāli aptuveni 1,5 nedēļu pēc lapas dzimšanas, ne kļūda. Paātrina ar GSC "URL Inspection → Request Indexing" (līdz 5 lapām dienā) — no nedēļām uz 24–72 stundām.

**Sitemap recursion + Bing.** Ja `sitemap-index.xml` satur tikai 1 norādi uz apakš-sitemap, Bing rāda "URLs discovered: 1". Iesniedz apakš-sitemap (`sitemap-0.xml`) tieši, lai paātrinātu, un paralēli izmanto IndexNow ar pilnu URL sarakstu.

**CI "Success" nenozīmē, ka strādā.** Workflow var atgriezt "Success", bet atsevišķi soļi klusi izgāžas. Vienmēr pārbaudi logus par katru kritisko soli atsevišķi — HTTP statusa kods ir definitīvais avots (200/202 = labi, 4xx/5xx = problēma).

**Neuzticies dokumentācijai bez pārbaudes.** URL kanoniskā forma (ar slīpsvītru vai bez) jāpārbauda pašā build izvadē un sitemap, ne tikai pieņēmumos. Nesakritība starp dokumentāciju un reālo build maitā indeksāciju.

---

## Kāpēc tas ir svarīgi tieši tagad

AI meklēšana Latvijas tirgū vēl ir agrīna. Latviešu valodā satura par šo tēmu ir maz, tāpēc tie uzņēmumi, kas savu redzamību sakārto tagad, iegūst priekšrocību, pirms konkurenti to pamana.

---

**Vajag praktisku palīdzību ar savu lapu?**

Es veidoju klientu mārketingu, kur AI dara operāciju, bet kvalitāti un lēmumus kontrolē cilvēks: Google reklāma, SEO, AI redzamība un skaidras mēneša atskaites.

- 🌐 [skels.lv](https://skels.lv) — bezmaksas AI redzamības audits
- 💼 [LinkedIn: in/modris-skels](https://www.linkedin.com/in/modris-skels)
