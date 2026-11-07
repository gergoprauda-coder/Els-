# Claude Code B2B marketingre – gyakorlati tananyag

Ez a repó egy kiinduló „munkaállomás” B2B marketing munkához Claude Code-dal.
Nem kell programozni tudni: a Claude Code itt egy olyan asszisztens, ami
**fájlokkal, mappákkal és összekötött eszközökkel (Drive, Gmail, Sheets,
Supermetrics, Canva, Trello, Naptár) dolgozik helyetted**, és amit
egyszer betanítasz, azt minden alkalommal ugyanúgy csinálja.

---

## 0. A legfontosabb gondolat

A chat-alapú AI-t minden alkalommal újra kell tanítani. A Claude Code-ban a
tudás **fájlokban** él:

| Mit akarsz, hogy „tudjon”? | Hova kerül? |
|---|---|
| Ki az ügyfél, mi a hangja, mik a tilalmak | `CLAUDE.md` (projekt-memória, minden indításkor betöltődik) |
| Az ügyfél nyersanyagai (interjúk, cikkek, számok) | `ugyfelek/<ugyfel>/forras/` mappa vagy Drive |
| Egy ismétlődő munkafolyamat (pl. „interjúból poszt”) | **skill** (`.claude/skills/<nev>/SKILL.md`) |
| Külső rendszerek (Drive, HubSpot, Ads adatok) | **connector / MCP szerver** |
| Rendszeresen futó feladat (pl. heti riport) | **routine / ütemezett feladat** |

Ha ezt a négy réteget felépíted, a Claude Code nem „szövegíró”, hanem egy
betanított junior marketinges lesz.

---

## 1. modul – Az első 15 perc

1. Indítsd el a Claude Code-ot ebben a mappában (web: claude.ai/code, vagy
   terminálban `claude`).
2. Írd be magyarul, amit szeretnél. Nincs speciális szintaxis.
3. Hasznos alapok:
   - `@fajlnev` – egy fájlt a beszélgetéshez csatolsz (`@ugyfelek/acme/forras/interju.md`)
   - **Plan mode** (Shift+Tab kétszer) – előbb tervet kérsz, csak jóváhagyás után dolgozik. Nagyobb anyagnál mindig ezzel kezdj.
   - `/` – a slash-parancsok és skillek listája
   - `/init` – a mappa alapján megírja a `CLAUDE.md` első változatát
   - `Esc` – megállítod, ha rossz irányba megy

**Első gyakorló prompt:**
> Olvasd el a CLAUDE.md-t, és kérdezz tőlem 10 kérdést, amitől jobban
> megérted az ügyfelet. A válaszaim alapján frissítsd a fájlt.

---

## 2. modul – Ügyfél-memória: a `CLAUDE.md`

A `CLAUDE.md` a legnagyobb hatású fájl. Minden munkamenet elején betöltődik,
ezért ide jön minden, amit nem akarsz minden alkalommal elmondani:

- ICP (ideális ügyfélprofil), döntéshozói szerepek, fájdalompontok
- pozicionálás, 3–4 üzenetpillér, bizonyítékok (számok, esettanulmányok)
- hang: 3 jó és 1 rossz példaposzt, *indoklással*
- tiltólista (szavak, fordulatok, állítások, amiket nem tehetünk)
- mappa-struktúra: hol vannak a források, hova mentse a kimenetet

Sablon: [`CLAUDE.md`](CLAUDE.md). Több ügyfélnél ügyfelenként egy almappa,
saját `CLAUDE.md`-vel (`ugyfelek/acme/CLAUDE.md`) – az almappában dolgozva az
is betöltődik.

**Szabály:** ha Claude kétszer ugyanazt a hibát elköveti, ne a promptot
javítsd, hanem írd bele a `CLAUDE.md`-be („Soha ne használd: …”).

---

## 3. modul – Tipikus B2B feladatok promptokkal

A te környezetedben már telepítve van a **marketing plugin** és több saját
skill. Ezek automatikusan bekapcsolnak, ha a kérés illik rájuk, de név szerint
is hívhatók (`/marketing:campaign-plan`).

| Feladat | Skill | Példa prompt |
|---|---|---|
| Tudásbázis az ügyfél anyagaiból | `knowledge-center` | „Építs Knowledge Centert az Acme Drive-mappájából.” |
| Hangminták, tartalmi mix | `tartalom-alap` | „Készítsd el az Acme hangmintáit a 10 legjobb posztjából.” |
| Interjúból LinkedIn poszt / hírlevél | `storytelling` | „@interju.md – ebből 3 posztötlet, aztán a legerősebbet írd meg.” |
| AI-citálható LinkedIn cikk | `linkedin-article-audit` → `-iro` → `-kiertekeles` | „Futtass AI-láthatósági auditot az Acme-nak.” |
| Infografika / carousel | `infografika` | „Ebből a cikkből 6 diás carouselt kérek.” |
| Funnel / vásárlói út | `funnel-terv` | „Készíts funnel tervet az Acme-nak.” |
| Kampányterv | `marketing:campaign-plan` | „Q1 lead-gen kampány CFO-knak, 8 hét, LinkedIn + email.” |
| Versenytárs-elemzés, battlecard | `marketing:competitive-brief` | „Hasonlítsd össze az Acme-t X-szel és Y-nal.” |
| Nurture email-sorozat | `marketing:email-sequence` | „5 lépéses nurture webinar-regisztrálóknak.” |
| SEO audit | `marketing:seo-audit` | „SEO audit: acme.hu, fókusz: ERP bevezetés.” |
| Teljesítmény-riport | `marketing:performance-report` + Supermetrics | „Múlt havi LinkedIn Ads + GA4 riport, javaslatokkal.” |
| Végső ellenőrzés | `tartalom-qa`, `marketing:brand-review` | „Nézd át, AI-szagú-e ez a szöveg.” |

**Jó prompt receptje (B2B):**
1. *Kinek* (szerep, iparág, cégméret, buying stage)
2. *Mit érjen el* (egy konkrét cselekvés)
3. *Miből dolgozzon* (`@forrás`, Drive-mappa, URL)
4. *Formátum és korlát* (hossz, csatorna, hány változat)
5. *Hova mentse* (`ugyfelek/acme/kimenet/2026-11/`)

---

## 4. modul – Láncolt munkafolyamat (ahol a Claude Code igazán erős)

Egy chatbot egy szöveget ír. A Claude Code egy **teljes folyamatot** végig tud
vinni egyetlen kérésre:

> Olvasd be az Acme Drive „Interjúk” mappájának új átiratait, frissítsd a
> Knowledge Centert, válaszd ki a 3 legerősebb történetet, írj belőlük
> LinkedIn posztot a hangminták alapján, futtasd rajtuk a tartalom-qa-t,
> a legjobbhoz készíts carouselt, és tegyél egy Trello kártyát a
> „Jóváhagyásra vár” listába mindhárommal.

Tippek:
- Ilyen hosszú feladatnál kapcsold be a **Plan mode**-ot.
- Kérj **köztes ellenőrzőpontot**: „A 3 történet kiválasztása után állj meg és mutasd meg.”
- Független részfeladatokhoz kérhetsz **subagenteket** („3 versenytársat párhuzamosan elemezz, külön agentekkel”).

---

## 5. modul – Adatok és eszközök (connectorok)

Jelenleg csatlakoztatva: **Gmail, Google Drive, Google Sheets, Google Naptár,
Supermetrics, Canva, Trello**. Példák:

- „Supermetricsből húzd le az elmúlt 90 nap LinkedIn Ads kampányait, és
  mondd meg, melyik hirdetésnek a legrosszabb a CPL-je.”
- „Írd be egy új Google Sheetbe a hónap lead-forrásait csatornánként.”
- „Keresd meg a Gmailben az Acme-tól jött utolsó 5 visszajelzést, és foglald
  össze, mit kérnek másként.”
- „Készíts Canva tervet a márka-sablonból ehhez a webinar-meghívóhoz.”

A marketing plugin HubSpot, Ahrefs, Similarweb, Notion, Slack, Klaviyo,
Amplitude és Figma connectorokat is hoz – ezek ebben a felhős munkamenetben
most **nem tudtak csatlakozni** (a hálózati proxy blokkolta). Ha CRM- vagy
SEO-adatokkal is dolgoznál, a környezet hálózati beállításaiban kell
engedélyezni a hosztjaikat, vagy helyi (asztali) Claude Code-ból használni.

---

## 6. modul – Saját skill írása (ismétlődő munkára)

Ha valamit hetente háromszor elmagyarázol, abból skill legyen. Egy skill csak
egy mappa egy `SKILL.md` fájllal:

```
.claude/skills/webinar-promo/SKILL.md
```

Minta: [`.claude/skills/webinar-promo/SKILL.md`](.claude/skills/webinar-promo/SKILL.md).
Legegyszerűbb, ha Claude-dal íratod meg:

> Az előbb csinált webinar-promóciós folyamatból csinálj skillt, hogy
> legközelebb egy mondatból is így csináld.

(Erre a `skill-creator` skill is be van kapcsolva.)

---

## 7. modul – Automatizálás

- **Ütemezett feladat:** „Minden hétfő reggel 8-kor készíts heti
  teljesítmény-összefoglalót Supermetricsből és küldd el nekem Gmail
  piszkozatként.” (Claude routine-t állít be.)
- **Hookok:** pl. minden mentett szövegen automatikusan fusson egy ellenőrzés
  – ehhez az `update-config` skillt kérd.

---

## 8. modul – Biztonsági és minőségi szabályok

1. **Számokat soha ne találjon ki.** Írd a `CLAUDE.md`-be: „Minden szám
   forrással, ha nincs forrás, jelöld [FORRÁS KELL]-lel.”
2. **Küldés előtt jóváhagyás.** Kérj Gmail *piszkozatot*, ne közvetlen küldést.
3. **Ügyféladat elkülönítése.** Ügyfelenként külön mappa / külön `CLAUDE.md`.
4. **Ember a végén.** A `tartalom-qa` szűr, de a végső szó a tiéd.
5. **Verziókövetés.** A git minden változatot megőriz – kérd: „commitold a mai
   anyagokat”, és bármikor visszanézhető, mi változott.

---

## Gyakorló terv (1 hét)

| Nap | Feladat |
|---|---|
| 1 | Töltsd ki a `CLAUDE.md`-t egy valós ügyfélre (Claude kérdezzen téged). |
| 2 | Knowledge Center építése az ügyfél Drive-anyagaiból. |
| 3 | Hangminták + 3 LinkedIn poszt egy interjúból, QA-val. |
| 4 | Kampányterv + 5 lépéses email-sorozat ugyanarra az ICP-re. |
| 5 | Supermetrics-riport az elmúlt hónapról, javaslatokkal. |
| 6 | Írj saját skillt a leggyakoribb feladatodra. |
| 7 | Állíts be egy heti ütemezett riportot. |
