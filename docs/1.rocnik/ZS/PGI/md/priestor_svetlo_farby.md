# Priestor, svetlo a farby (otázky 1 - 13)

_[Zdroj: PG_2021_Otazky_z_predmetu.pdf, skuska2023.pdf, prednasky.pdf]_

---

## 1. Používanie a spracovanie farieb v rámci počítačovej grafiky, základné atribúty svetla, farebný priestor, gamut

### Prečo sú farby dôležité
- Svetelný priestor je „bázický“; v podkladoch sa uvádza, že približne **80 % informácií vnímame zrakom**.

### Svetlo – reprezentácie a typy
**Dve reprezentácie svetla:**
- **Vlnová**: elektromagnetické vlnenie (v podkladoch: oblasť ~10^8 Hz).
- **Časticová**: prúd častíc – **fotónov**.

**Typy svetla:**
- **Achromatické**: zložené z viacerých zložiek spektra (typicky „biele svetlo“).
- **Monochromatické**: jedna zložka prevláda (v praxi nie je ideálne 100 % „jednofrekvenčné“).

### Základné atribúty svetla (podľa podkladov)
- **Farba**: závisí od frekvencie (resp. vlnovej dĺžky).
- **Jas**: zodpovedá intenzite svetla (amplitúde).
- **Sýtosť**: „čistota“ svetla; vyššia sýtosť = užšie spektrum obsiahnutých frekvencií.
- **Svetlosť**: veľkosť achromatickej zložky vo svetle s určitou dominantnou zložkou.

### Farebné modely, farebný priestor, farebná hĺbka, gamut
- **Farebný model** je definovaný:
  - množinou základných farieb,
  - spôsobom ich miešania,
  - pravidlami menenia farebných charakteristík.
- **Farebný priestor (color space)**: oblasť farieb pokrytá možnosťami príslušného farebného modelu.
- **Farebná hĺbka**: počet zobraziteľných farieb; udáva sa v bitoch.
  - Príklady režimov z podkladov: **HighColor (16 bitov)**, **TrueColor (24/32 bitov)**.
- **Gamut**: dosiahnuteľná oblasť farieb v danom farebnom priestore.
  - Farby mimo gamutu sa dajú zobraziť iba približne.

---

## 2. Chromatický diagram, typy, odtieň a saturácia

### Chromatický diagram (CIE)
- Chromatický diagram je farebný model vyvinutý na základe **štandardného pozorovateľa**.
- Používa sa trojzložkový (**tristimulus**) systém:
  - farba je určená trojicou **(X, Y, Z)**,
  - **Y** udáva **jas** objektu,
  - primárne zložky sú zvolené tak, aby boli farby definované ako pozitívne hodnoty.

### Typy chromatického diagramu (podľa podkladov)
- **CIELAB**: absorbované svetlo (atramenty, farbivá, pigmenty); **subtraktívne** miešanie (tlač).
- **CIELUV**: emitované svetlo (fosfor, farebné svetelné zdroje); **aditívne** miešanie (monitor).

Poznámka z podkladov:
- škála svetlosti (jasnosti) je pre oba modely rovnaká a je založená na tretej odmocnine svietivosti.

### Odtieň a saturácia
- **Odtieň (farebný tón)**: spôsob vnímania farby; popis prechodu medzi farbami (často kruh).
- **Saturácia**: živosť/nevýraznosť; blízkosť k sivej alebo k čistému odtieňu.
  - Podklady: farby v strede sú sivé (matné), sýtejšie smerom k obvodu.

### Aditívne vs. subtraktívne miešanie (zhrnutie z podkladov)
- **Aditívne**: základ čierna; pridaním všetkých zložiek → biela.
- **Subtraktívne**: základ biela; pridaním všetkých zložiek → čierna.

---

## 3. Farebné modely RGB a RGBA

### RGB
- Zložky: **R, G, B**.
- Miešanie: **aditívne**.
- Zmena zložky: **lineárna**.

### RGBA
- RGB + **A (alfa – priesvitnosť)**.
- Miešanie: **aditívne**.
- Zmena zložky: **lineárna**.

---

## 4. Farebné modely CMY a CMYK

### CMY
- Zložky: **C, M, Y** (Cyan – tyrkysová/azúrová, Magenta – purpurová, Yellow – žltá).
- Miešanie: **subtraktívne**.
- Zmena zložky: **lineárna**.

### CMYK
- CMY + **K (blacK – technologická čierna)**.
- Miešanie: **subtraktívne**.
- Zmena zložky: **lineárna**.

Poznámka z podkladov:
- **RGB vs. CMY** pokrývajú inú časť farebného priestoru; nie všetky farby sú dosiahnuteľné oboma modelmi.

---

## 5. Farebný model HSB

- Označovaný aj ako **HSB (HSV)**.
- Zložky: **Hue**, **Saturation**, **Brightness** (v podkladoch aj „value“).
- Miešanie: **aditívne**.
- Zmena zložky: **uhlová a lineárna**.

---

## 6. Farebný model HLS

- V podkladoch: „najlepší pre ľudské oko“.
- Zložky: **Hue**, **Lightness**, **Saturation**.
- Miešanie: **aditívne**.
- Zmena zložky: **uhlová a lineárna**.

---

## 7. Gama korekcia a alfa-miešanie

### Gama (γ) a gama korekcia
- **Gama** určuje vzťah medzi číselnou hodnotou bodu a jeho skutočnou svietivosťou.
- Podklady uvádzajú potrebu korekcie, lebo ľudské oko nie je „lineárny senzor“ (citlivosť v tme/tieni vs. v jase) a technické zariadenia často pracujú lineárne.
- Uvádza sa aj technická stránka: „ideál vs realita“, kalibrácia monitorov (napätie).

### Alfa-miešanie
- Založené na **alfa hodnote** (priesvitnosti).
- Pri prekrytí objektov sa podľa alfa vrchnej vrstvy určí výsledné správanie farieb.

---

## 8. Problematika ľudského vizuálneho vnemu a jeho spracovania v relácii s počítačovou grafikou

- Orgán príjmu: **oko**.
- Orgán spracovania: **mozog**.
- Receptory: **tyčinky** a **čapíky**.

### Čapíky a tyčinky (podľa podkladov)
- **Čapíky (cones)**:
  - cca **6–7 mil.**, stred sietnice,
  - citlivé na farby,
  - skupiny: **červená–zelená (RG-cones)** (dominantné) a **modrá–žltá (BY-cones)**.
- **Tyčinky (rods)**:
  - cca **75–150 mil.**, rovnomerne po sietnici,
  - vnem obrysov a jasu (všeobecné obrazové informácie).

---

## 9. Miešania a rozptyľovania farieb (prevod do šedej škály, halftoning, dithering) v rámci počítačovej grafiky

### Prevod do šedej škály
- **I = 0.299 · R + 0.587 · G + 0.114 · B**

### Halftoning
- Simulácia plynulého prechodu medzi odtieňmi pomocou bodov a medzier rôznych veľkostí.
- Pri dostatočnej vzdialenosti oko nevníma body jednotlivo.
- Podklady: 1 pixel nahradený množinou pixelov binárnou maskou (2 farby); zmienka o monochromatickej laserovej tlači (potreba vyššieho rozlíšenia).

### Dithering
- Používa vzory z pixelov singulárnych farieb; oko vo vzdialenosti vníma výslednú farbu/tón.

### Určenie farby (pravidlá uvedené v podkladoch)
- náhodne,
- spriemernením bodov oblasti alebo mediánovou funkciou,
- podľa najčastejšieho výskytu farby v oblasti,
- podľa najmenej častého výskytu,
- podľa farby ľavého horného bodu oblasti.

---

## 10. Ergonómia a symbolika farieb, použitie farieb v počítačovej grafike

V dodaných podkladoch k tomuto okruhu nie sú konkrétne body (je uvedený len názov otázky).  
Aby sa dodržalo „nevymýšľanie“ mimo materiálov, táto časť ostáva bez doplnených tvrdení.

---

## 11. Dimenzia priestoru a dimenzia objektu, štruktúra dimenzie

### Dimenzia (rozmer) priestoru
- Minimálne množstvo parametrov definujúcich ľubovoľný bod v priestore.

### Typy/druhy dimenzií (podľa podkladov)
- **Číselná**: celočíselná (topologická) aj neceločíselná.
- **Nečíselná**: napr. informačná, dimenzia sebepodobnosti; uvádzajú sa aj topologická, Hausdorffova, farebná, fraktálna, kapacitná, dimenzia rotácií a pod.

### Štruktúra dimenzie
- **3 = 3 + 0** (geometria + čas) – homogénna štruktúra,
- **3 = 2 + 1** (geometria + čas) – nehomogénna štruktúra.

### Rozmer objektov
- 0D bod, 1D priamka/úsečka, 2D plocha, 3D teleso.

Poznámka z podkladov:
- geometrické objekty sa dajú spojitou transformáciou previesť na vyššie uvedené objekty, ak majú rovnakú topologickú dimenziu.

---

## 12. Priestor a jeho súradnicová sústava, stupeň voľnosti

- Koordinačný systém parametrizuje priestor (počiatočný bod, smery).
- Súradnice jednoznačne definujú polohu.

### Stupeň voľnosti (DoF)
- Počet nezávislých parametrov konfigurácie/stavu; translačné a rotačné smery.
- Príklady z podkladov:
  - častica v 3D: **3 DoF** (x, y, z),
  - teleso v 3D: **6 DoF** (3 translačné + 3 rotačné).

---

## 13. Vrstvy vizualizačného procesu

### Pojmy (z podkladov)
- **Vision**: analýza obrazov na tvorbu počítačových modelov sveta.
- **Rendering**: syntéza obrazu z modelov sveta.
- **Vizualizácia**: transformácia popisu modelu virtuálneho sveta do výstupného obrazu na zobrazovači.

### Vrstvy (1 – 7)
1. Definovanie/spracovanie modelu (reprezentácia, súradnicové systémy)
2. Transformácie nad objektami (geometrické)
3. Riešenie viditeľnosti
4. Tieňovanie
5. Osvetľovanie
6. Realistické zobrazovanie
7. Kompozícia a vykresľovanie

---

## Rýchle skúškové zhrnutie (čo vedieť povedať)
- Svetlo: vlnová a časticová reprezentácia; achromatické vs monochromatické; atribúty farba/jas/sýtosť/svetlosť.
- Farebný priestor = oblasť farieb modelu; farebná hĺbka v bitoch (HighColor, TrueColor); gamut = dosiahnuteľné farby.
- CIE chromatický diagram: tristimulus (X,Y,Z), Y = jas; typy CIELAB (subtraktívne – tlač) a CIELUV (aditívne – monitor); odtieň a saturácia.
- RGB/RGBA: aditívne, lineárne; A = priesvitnosť. CMY/CMYK: subtraktívne, K = technologická čierna.
- HSB(HSV) a HLS: Hue + (S,B) alebo (L,S); zmena uhlová/lineárna.
- Gama korekcia: vzťah číslo ↔ svietivosť; ideál vs realita a kalibrácia; alfa-miešanie podľa alfa.
- Vizuálny vnem: čapíky (RG, BY) a tyčinky; oko prijíma, mozog spracúva.
- Šedá škála: I = 0.299R + 0.587G + 0.114B; halftoning a dithering ako miešanie/rozptyľovanie farieb.
- Dimenzie: číselné/nečíselné; štruktúra 3=3+0 vs 3=2+1; rozmer objektov 0D–3D.
- Súradnicová sústava a DoF: 3 DoF pre bod/časticu v 3D, 6 DoF pre teleso.
- Vrstvy vizualizácie: model → transformácie → viditeľnosť → tieňovanie → osvetľovanie → realistické → kompozícia/rendering.
