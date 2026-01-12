# Fraktály, časticové systémy, virtuálna realita a XR (otázky 78 - 80)

_[Zdroj: PG_2021_Otazky_z_predmetu.pdf, skuska2023.pdf, prednasky.pdf]_

---

## 78. Fraktály a časticové systémy

### Fraktály

#### Základná charakteristika
- Pôvod slova: *lat. frangere* – „zlomiť“ (*to break*).
- Fraktál je **množina, ktorej Hausdorffova dimenzia je väčšia než dimenzia topologická**:
  - dimenzia je **neceločíselná**,
  - vyjadruje „mieru členitosti“ (ako veľmi je útvar detailný/členitý na rôznych mierkach).
- Kľúčový pojem fraktálnej geometrie: **sebepodobnosť** (invariancia voči zmene mierky) – malé časti môžu pripomínať celok.

#### Typy fraktálov (podľa podkladov)
- **L-systémy**
- **IFS (Iterated Function Systems)**
- **Dynamické množiny / dynamické systémy (dynamic sets)**

---

### 78.1 L-systémy (Lindenmayerove systémy)
- Patria medzi **najjednoduchšie fraktály**.
- Vhodné pre **popis objektov prírody** (rastliny, stromy, listy) – v **2D aj 3D**.
- Pracujú na princípe **aplikácie pravidiel nezávisle na poradí**.
- Systém je definovaný:
  - **stavom** (poloha a orientácia L-systému),
  - **tabuľkou akcií** (pravidlá).

**Grafická interpretácia:**
- najčastejšie **korytnačia grafika** (turtle graphics), historicky spájaná s jazykom **LOGO**.

**Základné pravidlá pohybu (podľa podkladov):**
- presunutie vpred **s kreslením**,
- presunutie vpred **bez kreslenia**,
- otočenie **vľavo**,
- otočenie **vpravo**.

**Príklad použitia:**
- generovanie vetvených štruktúr podobných rastlinám (strom, konár, list).

---

### 78.2 IFS (Iterated Function Systems)
- **Generatívny typ fraktálov**: systém iterovaných funkcií.
- V podkladoch sa uvádza použitie napr. pri **fraktálnej komprimácii údajov**.
- Realizácia: na obrazovke sa **iteratívne kreslia body**.

**Príklady fraktálov uvedené v materiáloch:**
- Pascalov trojuholník, Sierpinského trojuholník, Sierpinského koberček,
- Kochova vločka, Dračia krivka, C krivka,
- Mengeleho/Mengerova huba (v podkladoch uvádzané ako „Mengeleho huba“).

---

### 78.3 Dynamické množiny / dynamické systémy
- V podkladoch: „zvizuálnenie niektorých funkcií komplexných čísel“, pričom vizuálny efekt sa prejaví v **špecifickom intervale**.
- Často ide o **rovinné obrazy 3D objektov**, kde:
  - „3. rozmer“ je vyjadrený **farbou** (farba predstavuje „výšku“ v danom bode).
- Založené na **komplexných číslach**.

**Pojmy a príklady z podkladov:**
- **Juliova množina** – sebepodobná, pozostáva z kópií samej seba pomocou nelineárnych transformácií; ohraničená kružnicou.
- **Mandelbrotova množina** – známy komplikovaný tvar.
- **Plazma** – využitie dynamických fraktálov pri simulácii **oblakov** a **ohňa**.

**Príklad použitia (podľa podkladov):**
- generovanie povrchov (napr. „hory“) a abstraktných podkladov; plazma pre oheň/oblaky.

---

### Časticové systémy (particle systems)

#### Základná idea
- **Častica** je objekt v scéne, ktorý má **vlastný životný cyklus**:
  - niekde sa „narodí“,
  - počas života sa vyvíja podľa prideleného kódu,
  - na konci „umiera“.
- To, čo častica robí a ako sa vyvíja, je **v réžii programátora**.
- Podľa podkladov sa časticové systémy pre niektoré prírodné javy používajú **častejšie ako fraktály**.

#### Použitie (príklady z podkladov)
- simulácia správania častíc: **mraky, dym, oheň**, prípadne aj ďalšie prírodné javy.

#### Prečo to funguje
- využívajú efekt **veľkého množstva malých častíc**, ktoré ako celok pôsobia realisticky.

#### Typy správania častíc (podľa podkladov)
- **usporiadané**: pohyb, rotácia, zmena farby,
- **chaotické**: výbuch, chemická reakcia, vietor.

---

## 79. Virtuálna realita: základné pojmy, kategorizácia, podsystémy VR systémov

### Základná definícia VR (podľa podkladov)
- Virtuálno-realitný systém je **interaktívny počítačový systém**, ktorý vytvára **ilúziu fyzickej prítomnosti** v priestore, ktorý reálne neexistuje (je syntetizovaný).
- Podklady zdôrazňujú tesne viazanú interakciu človek – výpočtový systém (**HCI, Human Computer Interaction**).
- Proces spracovania vstupov, modelovania, vizualizácie a virtualizácie v rámci komplexného VR systému sa nazýva **virtualizačný reťazec**.

### Kategorizácia VR systémov (podľa úrovne techniky)

#### 79.1 Vstupná VR
- v podstate „inteligentnejšie“ 3D modely a ich zobrazenie na obrazovke,
- spravidla podporené zvukom,
- interakcia na úrovni 2D ovládačov,
- môže ísť o niektoré dobre spracované hry.

#### 79.2 Základná (nízka) VR
- 3D efekt pomocou monitorov a **anaglyfických okuliarov** (napr. červený + azúrový/tyrkysový filter),
- nevýhoda: menšie „vtiahnutie“ používateľa,
- interakcia stále cez 2D ovládače (myš, joystick).

#### 79.3 Stredná VR
- zlepšenie zobrazovania aj vstupných prvkov,
- 3D efekt cez okuliare s **polarizačnými filtrami** alebo **LCD okuliare** (umožnia farebný pohľad),
- interakcia cez ovládače s viacerými stupňami voľnosti (Spacepilot, spaceball, 3D joystick…),
- spomína sa aj dátová rukavica, snímanie na báze tenzie svalov, bezkontaktné snímanie (napr. MS Kinect),
- typická črta: možnosť prevádzky aj na PC s výkonnou grafickou kartou.

#### 79.4 Úplné (immersive) VR
- kvalitatívne iná interakcia najmä vizuálne, zvukovo a pohybovo,
- 3D efekt cez **dátovú prilbu / HMD (Head Mounted Display)** so vstavanými displejmi,
- často doplnené o audio systém a snímače polohy hlavy, rúk či nôh,
- môžu existovať simulátory fyzického odporu/dotyku a ďalšie zariadenia pôsobiace na receptory (čuch, chuť…).

### Podsystémy VR (podľa zmyslov, ktoré ovplyvňujú)
- **Vizualizačný podsystém**
- **Akustický podsystém**
- **Kinetický a statokinetický podsystém**
- **Podsystém dotyku a kontaktu**
- ďalšie zmysly (napr. čuch, chuť, …)

Poznámka z podkladov:
- niektoré zmysly nemá veľký zmysel implementovať (ako príklad sa uvádza chuť).

---

## 80. XR (eXtended Reality) a jej zložky, kolaboratívna VR, interakcia a používateľské rozhrania na báze XR

### XR a jeho zložky (podľa podkladov)
V materiáloch sa uvádzajú tri základné technologické bázy:
- **VR (Virtual Reality)** – plne pohlcujúce virtuálne prostredie; pohltenie najmä na úrovni vizuálnej, zvukovej a dotykovo-hmatovej.
- **MR (Mixed Reality, zmiešaná realita)** – syntetizácia virtuálnych objektov do fyzického priestoru používateľa; ovládanie často gestami a snímaním rúk; rozšírené o priestorové rozpoznávanie.
- **AR (Augmented Reality, augmentovaná realita)** – viazaná k obrazovej informácii; využíva rozpoznávanie informácií v obraze za účelom dosadenia 3D objektov; dôležitá je konzistentnosť a rozpoznateľnosť vizuálneho vstupu.

**XR (eXtended Reality)**:
- v podkladoch ako zlučovanie VR, MR a AR pod spoločnú oblasť,
- „X“ referuje na variabilné použitie ktoréhokoľvek z nich,
- cieľom je zjednocovanie softvérovej kompatibility a aplikačných platforiem na úroveň XR.

### Kolaboratívna VR / kolaboratívna XR
- Vzniká potreba zdieľania používateľskej interakcie a spoločného virtuálneho priestoru.
- Kolaboratívne systémy sprostredkujú **zdieľané prostredie viacerým používateľom v reálnom čase** a zabezpečujú zdieľanie interakcie a komunikácie.

**Vlastnosti kolaboratívneho prostredia (podľa podkladov):**
- integrácia skupiny používateľov a podpora skupinových aktivít,
- zdieľanie virtuálneho/zmiešaného priestoru,
- dosahovanie spoločného cieľa,
- kombinácia viacerých vstupov v reálnom čase,
- interaktívna komunikácia a operovanie v zdieľanom prostredí.

### Systémy interakcie a používateľské rozhrania na báze XR
Podklady zdôrazňujú, že VR/XR je úzko spätá s efektívnou komunikáciou človek – počítač (HCI) a s rozvojom pokročilých rozhraní.
- V praxi sa používajú rôzne vstupné a výstupné zariadenia (od klasických 2D ovládačov až po snímače pohybu, gestá, HMD a haptické prvky).
- Používateľské rozhrania v XR sú viazané na vizualizačný reťazec a jeho real-time spracovanie (vizualizácia, spätná väzba, interakcia).

---

## Rýchle skúškové zhrnutie (čo vedieť povedať)
- Fraktál: Hausdorffova dimenzia > topologická dimenzia; neceločíselná dimenzia = miera členitosti; sebepodobnosť.
- Typy fraktálov: L-systémy, IFS, dynamické množiny (komplexné čísla).
- L-systémy: stav + tabuľka akcií; korytnačia grafika; pravidlá pohybu vpred (s/bez kreslenia) + otočenia vľavo/vpravo; použitie na rastliny.
- IFS: iterované funkcie; iteratívne kreslenie bodov; príklady (Sierpinski, Koch, dračia krivka…); použitie aj pri fraktálnej komprimácii.
- Dynamické množiny: komplexné čísla; Julia (sebepodobná), Mandelbrot; „plazma“ pre oblaky/oheň; farba ako „výška“.
- Časticové systémy: častica = životný cyklus (narodí sa → vyvíja sa podľa kódu → umiera); použitie (dym, oheň, mraky); usporiadané vs chaotické správanie.
- VR definícia: interaktívny systém s ilúziou prítomnosti v syntetizovanom priestore; virtualizačný reťazec.
- Kategorizácia VR: vstupná → základná (anaglyf) → stredná (polarizačné/LCD okuliare, 3D ovládače, rukavica/Kinect) → úplná/immersive (HMD, snímače, haptika).
- Podsystémy VR: vizualizačný, akustický, kinetický/statokinetický, dotyk/kontakt + ďalšie zmysly.
- XR: zlučuje VR/MR/AR; cieľom je zjednotiť platformy a kompatibilitu.
- Kolaboratívna VR/XR: zdieľaný priestor a interakcia viacerých používateľov v reálnom čase (komunikácia, spoločný cieľ, kombinácia vstupov).
