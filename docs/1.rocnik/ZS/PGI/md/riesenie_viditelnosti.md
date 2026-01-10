# Riešenie viditeľnosti v počítačovej grafike (otázky 50-60)

_[Zdroj: PG_2021_Otazky_z_predmetu.pdf, skuska2023.pdf, prednasky.pdf]_

---

## 50. Problém riešenia viditeľnosti a jeho kategorizácia v rámci počítačovej grafiky

### Podstata problému
Riešenie viditeľnosti spočíva v odstránení (resp. odlíšení) tých častí 3D objektov, ktoré **pri danom premietaní do 2D nie sú z miesta pozorovateľa viditeľné** (sú zakryté). Cieľom je, aby sa do výsledného obrazu dostal vždy „ten správny“ objekt/pixel – typicky ten, ktorý je ku kamere najbližšie.

Prakticky sa to často deje tak, že sa pre obrazové body uvažujú lúče/pohľadové úsečky zo smeru kamery a hľadajú sa priesečníky s objektmi.

### Kategorizácia (podľa materiálov)
- **Podľa priestoru, kde sa viditeľnosť rieši**
  - riešenie v **3D**
  - riešenie v **2D priemetni** (v obrazovom priestore)
- **Podľa reprezentácie (orientácie) algoritmu**
  - **objektovo orientované** – riešia „ktorá časť objektu je viditeľná“
  - **obrazovo orientované** – riešia spätne „ktorý objekt je viditeľný v danom obrazovom bode“
- **Podľa toho, či sa uvažuje osvetlenie**
  - bez osvetlenia (farby lokálne na objektoch)
  - s osvetlením (globálne metódy v scéne – napr. raytracing, radiosity)
- **Podľa vplyvu chyby**
  - s **lokálnym** vplyvom chyby
  - s **globálnym** vplyvom chyby (typicky globálne metódy)
- **Podľa času výpočtu**
  - mimo reálneho času
  - v reálnom čase (často HW podpora)

Poznámka: pri veľkých scénach často narastá „problém výberu čo kresliť“ skôr než samotné kreslenie.

---

## 51. Algoritmus plávajúceho horizontu

### Charakteristika
- Viditeľnosť rieši **až v priemete (2D)**, teda nie úplne „100 %“ všeobecne.
- Účinný hlavne pre **vykresľovanie grafov funkcií / plošných grafov** (plocha kreslená po rezoch).
- Jednoducho implementovateľný, typicky nie je používaný ako univerzálny real‑time algoritmus.

### Pointa postupu (horizonty)
- Plocha sa kreslí po **krivkových rezoch** (napr. podľa parametra `u` alebo `w` – zvolí sa dominantný smer kreslenia).
- Pre každý stĺpec `X` obrazovky sa udržiava:
  - **horný horizont H(X)** (maximálna už viditeľná hodnota)
  - **dolný horizont D(X)** (minimálna už viditeľná hodnota)
- Prvý rez vytvorí počiatočné horizonty (H=D podľa prvého rezu).
- Pri ďalšom reze:
  - body **nad H** alebo **pod D** sú viditeľné → kreslia sa a **aktualizujú** horizonty,
  - body **medzi H a D** sú zakryté → **nekreslia sa** a horizonty sa nemenia.

**Príklad použitia:** zobrazenie povrchu `z = f(x,y)` ako „terénu“ kresleného od prednej časti k zadnej.

---

## 52. Maliarov algoritmus riešenia viditeľnosti (Painter’s algorithm)

### Charakteristika
- **Objektovo orientovaný** prístup.
- Myšlienka: „maľuj odzadu dopredu“.

### Základný postup
1. Zoradiť polygóny/objekty podľa vzdialenosti od pozorovateľa (**Z-sort**).
2. Vykresľovať ich **od najvzdialenejších po najbližšie** (prekresľovaním sa zakrývajú zadné).

### Typické problémy
- Nie vždy je jednoznačné objekty zoradiť (pretínanie polygónov).
- Nevýhoda pri **cyklickom prekryve** (A zakrýva B, B zakrýva C, C zakrýva A).

### Podmienky/heuristiky uvádzané v materiáloch
- Ak `z1max < z2min`, potom je `P1` úplne za `P2`.
- Ak sa neprekrývajú priemety v rovine priemetne (SSZ), poradie je nezávislé.
- Testy s rovinami polygónov (vrcholy jedného polygónu „pod“ rovinou druhého a pod.).

**Príklad:** jednoduchá scéna bez pretínania objektov (napr. „vrstvy“ hôr v diaľke) – funguje dobre.

---

## 53. Freeman-Lotrelov algoritmus riešenia viditeľnosti

### Charakteristika
- Rieši sa v **3D**.
- Najprv filtruje steny na **neviditeľné** a **potenciálne viditeľné**.

### Kľúčová myšlienka (uhol s normálou)
- Závisí od uhla `φ` medzi:
  - vektorom pohľadu kamery
  - a **normálou steny**
- Interpretácia z materiálov:
  - **ostrý uhol** → stena je orientovaná ku kamere → potenciálne viditeľná,
  - **tupý uhol** → stena je otočená od kamery → neviditeľná (zadná strana).

### Podmienka
- Steny musia mať **rovnakú orientáciu** (v smere hodinových ručičiek alebo proti smeru) – kvôli konzistentným normálam.

**Príklad:** backface culling na uzavretom telese (kocka) – zadné steny sa vyradia ešte pred drahším riešením prekryvov.

---

## 54. Algoritmus pamäte hĺbky (Z-buffer)

### Charakteristika
- **Obrazovo orientovaný**, typicky najpoužívanejší.
- V materiáloch: „100 % vždy“ korektný (pre dané rozlíšenie a presnosť hĺbky).
- V praxi je často **hardvérovo podporovaný** v GPU.

### Základná idea
Používajú sa dve matice (buffer-y) s rozlíšením SSZ:
- **color buffer** (farba výsledného pixelu)
- **depth buffer** (hĺbka/Z hodnota)

### Postup
1. Inicializácia:
   - depth na „nekonečno“,
   - farba na farbu pozadia.
2. Pre každý rasterizovaný fragment/pixel polygónu sa vypočíta jeho hĺbka.
3. Ak je nová hĺbka **menšia** (bližšie ku kamere) než uložená:
   - prepíše sa depth aj farba.
4. Na konci sa zobrazí color buffer.

### Výhody (z materiálov)
- korektné riešenie viditeľnosti,
- polygóny sa môžu pretínať,
- kreslia sa v ľubovoľnom poradí (bez triedenia),
- vhodný pre veľa malých polygónov.

### Nevýhody (z materiálov)
- pamäťové nároky (minimálne ~2 * maxX * maxY bajtov),
- prekresľovanie (overdraw),
- menej efektívny pri veľkých scénach s veľkými polygónmi → urýchľuje sa napr. orezaním na zorný ihlan.

**Príklad:** moderné real‑time renderovanie v hrách – depth buffer rozhoduje, čo je v každom pixeli vpredu.

---

## 55. Metóda BSP stromov pri riešení viditeľnosti v rámci počítačovej grafiky, tvorba a prechod BSP stromom

### Charakteristika BSP
- BSP (Binary Space Partitioning) strom **binárne delí priestor** deliaci(mi) rovinami (v 2D priamkami).
- Pomáha riešiť aj **cyklické prekryvy** (scénu vie spraviť „acyklickou“ z pohľadu poradia kreslenia).

### Typy podľa materiálov
- podľa tvaru: **vyvážený / nevyvážený**
- podľa správania rovín:
  - statický (vypočíta sa raz),
  - dynamický (mení sa),
  - adaptívny (možný posun roviny),
  - stratový (zanedbávanie „nepodstatných“ častí)

### Tvorba BSP stromu (pointa)
1. Zvolí sa deliaca rovina (priamka).
2. Polygóny sa rozdelia na:
   - „vpredu“ (front),
   - „vzadu“ (back).
3. Ak polygón **pretína** deliacu rovinu, rozdelí sa na dve časti.
4. Rekurzívne sa pokračuje pre obe strany.

Poznámka: voľba deliacej roviny je kľúčová a môže byť náročná (ovplyvňuje vyváženosť a počet rezaní polygónov).

### Prechod stromom (traversal)
Používajú sa dva typické prechody (podľa toho, či chceme poradie kreslenia):
- **zozadu dopredu** (podobne ako maliar – správne prekrytie),
- **spredu dozadu** (môže pomôcť s urýchlením pri skorom vyradení).

Pointa rozhodovania:
- podľa toho, či je kamera na „front“ alebo „back“ strane deliacej roviny, sa určí, ktorý podstrom sa prejde ako prvý.

**Príklad:** interiéry/koridorové scény (sektory) – BSP pomáha držať konzistentné poradie kreslenia bez cyklov.

---

## 56. Metóda oktantových stromov pri riešení viditeľnosti v rámci počítačovej grafiky

### Charakteristika
- Podobná myšlienka ako BSP, ale delenie priestoru je **pravidelné**:
  - v 3D sa priestor delí na **8 oktantov** (octree),
  - deliace roviny sú **rovnobežné s osami** súradnicovej sústavy.
- Statické pravidelné delenie nemusí byť „ideálne“ → existujú:
  - adaptívne varianty (snaha znížiť rezanie objektov),
  - stratové varianty (zanedbanie častí pod hranicou straty).

### Výhoda / nevýhoda (z poznámok)
- výhoda: rýchle a jednoduché delenie,
- nevýhoda: objekty môžu byť rozrezané do viacerých buniek; optimálne rozdelenie je ťažké.

**Príklad:** priestorové indexovanie scény pre rýchle testy (čo je v ktorom „kúsku“ priestoru).

---

## 57. Urýchľovacie metódy pre riešenie viditeľnosti v počítačovej grafike, FV (BC) algoritmus

### Pointa urýchľovania
Cieľ: **znížiť počet objektov/polygónov**, ktoré vôbec vstúpia do drahých výpočtov viditeľnosti.

### FV (Front View) / BC (Back Cut)
- Najjednoduchší princíp: do výpočtu pustíme len to, čo je **pred pozorovateľom**.
- Vytvorí sa deliaca rovina; objekty „za“ pozorovateľom sa zahodia.

**Príklad:** kamera sa pozerá dopredu – objekty striktne za kamerou nemajú šancu prispieť do obrazu.

---

## 58. Orezávania na zorný ihlan pri riešení viditeľnosti v rámci počítačovej grafiky

### Zorný ihlan (frustum)
Zorný ihlan je časť priestoru vymedzená HFOV/VFOV, ktorá sa po projekcii (SSC → SSZ) zobrazí do obdĺžnika na priemetni – to je zorný priestor, ktorý vie skončiť na obrazovke.

### Orezávanie (frustum culling / clipping)
- Orezanie je možné robiť:
  - v **SSC** (súradnicová sústava kamery),
  - alebo v **USS** (globálna).
- Objekty, ktoré nijako nezasahujú do zorného ihlana, sa vyradia ešte pred ďalšími krokmi.

**Príklad:** veľký svet – renderuje sa len to, čo spadá do frustumu kamery.

---

## 59. Ohraničujúce objekty, sektorovanie a potenciál viditeľnosti pri urýchľovaní riešenia viditeľnosti

### Ohraničujúce útvary (bounding volumes)
- Zložité objekty (alebo skupiny objektov) sa uzavrú do jednoduchších útvarov.
- Najprv sa testuje priesečník s jednoduchým útvarom:
  - ak nie je priesečník → určite nie je ani s pôvodným objektom,
  - ak je priesečník → až potom sa rieši detailný objekt.

Uvádzané útvary (od „hrubších“ po presnejšie):
- hierarchia gúľ,
- AABB (osovo orientovaný kváder),
- OBB (objektovo orientovaný kváder),
- konvexná obálka (convex hull).

### Sektorovanie + potenciál viditeľnosti (PVS)
- Scéna sa rozdelí na **sektory**.
- Pre každý sektor sa určí **PVS (Potential Visible Set)**:
  - ktoré ďalšie sektory môžu byť viditeľné z daného sektora (stačí, že 1 bod je viditeľný).
- V renderi sa potom uvažuje len so sektormi v PVS.

**Príklad:** „portálové“ hry (miestnosti + dvere/prechody) – ak si v jednej miestnosti, renderujú sa len sektory, ktoré môžu byť cez portály viditeľné.

---

## 60. S-buffer pri riešení viditeľnosti v počítačovej grafike

### Pointa (span buffer)
- Urýchľovacia technika (z poznámok prioritne v 2D):
  - už vykreslené (zakrývajúce) časti sa evidujú ako „span-y“ (úseky) na riadkoch,
  - do ďalšieho spracovania sa púšťajú len pixely/úseky, ktoré ešte môžu byť viditeľné.
- Cieľ: znížiť zbytočné prekresľovanie (overdraw).

**Príklad:** pri kreslení stien v 2D priemete – úseky zakryté už „prednou“ stenou sa už znovu neriešia.

---

## Rýchle skúškové zhrnutie (čo vedieť povedať)
- Viditeľnosť = odstránenie zakrytých častí objektov po projekcii do 2D; rozhoduje „čo je v pixeli najbližšie ku kamere“.
- Kategorizácia: 3D vs 2D; objektovo vs obrazovo orientované; bez/s osvetlením; lokálny vs globálny vplyv chyby; real‑time vs mimo real‑time.
- Plávajúci horizont: plocha po rezoch, pre každý X horný/dolný horizont; body medzi nimi sú zakryté.
- Maliarov algoritmus: zoradiť podľa vzdialenosti, kresliť odzadu dopredu; problém cyklických prekryvov/pretínania.
- Freeman‑Lotrel: filtrovanie stien podľa uhla pohľad–normála; potreba konzistentnej orientácie stien.
- Z-buffer: color + depth buffer; pre každý pixel vyhrá najmenšia hĺbka; HW podpora; veľké pamäťové nároky/overdraw.
- BSP: binárne delenie priestoru rovinami; tvorba delením polygónov; traversal zozadu dopredu alebo spredu dozadu podľa polohy kamery.
- Octree: pravidelné delenie na oktanty; rýchle, ale môže rezať objekty; adaptívne/stratové varianty.
- Urýchľovanie: FV/BC (len pred kamerou), frustum orezanie, bounding volumes, sektorovanie + PVS, S-buffer.
