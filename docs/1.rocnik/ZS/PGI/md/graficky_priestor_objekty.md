# Grafický priestor a objekty (otázky 22 - 25)

_[Zdroj: PG_2021_Otazky_z_predmetu.pdf, skuska2023.pdf, prednasky.pdf]_

---

## 22. Popis a reprezentácia objektov v počítačovej grafike, priestor a jeho parametre

### Súvis s vizualizačným procesom
- Téma patrí stále do **1. úrovne vizualizačného procesu** (modelovanie: čo je objekt, ako ho popíšem, v akom priestore).

### Priestor a jeho parametre (delenie podľa podkladov)

**Podľa charakteru priestoru:**
1. **Translačný priestor**
2. **Rotačný priestor**
3. **Kombinovaný priestor**

**Podľa typu dimenzie:**
1. **Celočíselné** (topologické)
2. **Neceločíselné**

**Podľa štruktúry dimenzií (primárne geometria) a ich počtu:**
1. **Homogénna štruktúra (N + 0)**  
   - ND priestor  
   - iba 1 zložka na definovanie štruktúry dimenzie
2. **Heterogénna štruktúra (N1 + N2 + ... + Nn)**  
   - (N1 + N2 + ... + Nn)D priestor  
   - 2 a viac zložiek, typicky **geometria + čas** (niekedy aj farba)

Poznámka z podkladov:
- uvádzajú sa aj príklady typu „celočíselný translačný priestor, celočíselný rotačný priestor“.

### Objekty v počítačovej grafike (podľa topologickej dimenzie)
1. **0-rozmerný objekt** (bod)
2. **1-rozmerný objekt** (priamka, úsečka)
3. **2-rozmerný objekt** (plocha)
4. **3-rozmerný objekt** (teleso)

Dôležité tvrdenia z podkladov:
- Všetky geometrické objekty sa dajú spojitou transformáciou previesť na vyššie uvedené objekty, ak majú rovnakú topologickú dimenziu.
- Objekty môžu reprezentovať vyššie uvedené objekty, ak majú rovnakú alebo nižšiu topologickú dimenziu.

### Popis vs. reprezentácia objektu
Pri spracovaní objektu sú dôležité dve hľadiská:
- **popis objektu**
- **reprezentácia objektu**

### Základné spôsoby popisu telies (modelovanie podľa podkladov)
V podkladoch sa uvádzajú tri základné spôsoby popisu:
- **Hraničná reprezentácia** (a jej štruktúrovaná derivácia **B-rep**)
- **Konštruktívna geometria telies (CSG)**
- **Vypočítavanie obsadených častí priestoru** (v podkladoch: „už sa nepoužíva“)

Súčasne sa uvádza aj rozdelenie systémov podľa toho, na čom je modelovanie založené:
- **množina bodov** (mračná bodov / point clouds) – 0
- **drôtový model** (wire frame model) – 1
- **povrchový model** (surface model) – 2
- **objemový model** (solid model) – 3

---

## 23. Hraničná reprezentácia

### Základná myšlienka
- Hraničná reprezentácia vychádza z predstavy, že najvýznamnejšie na telese sú **hraničné elementy**:
  - hrany,
  - povrch, ktorý tvorí hranicu medzi hmotou telesa a okolitým priestorom.

### Typy hraničných plôch (podľa podkladov)
- **časti rovín**
- **analytické plochy**
- **špeciálne parametrické plochy**

### Najjednoduchšia metóda popisu hranice telies
- Stanovenie **hrán a vrcholov** na povrchu telesa → **drôtový model**.
- V podkladoch je poznámka, že môže byť **nejednoznačný**.

### B-rep (Boundary Representation) – štruktúrovanejšia forma
- **B-rep** definuje objekt jeho **povrchom**.
- Povrch je zložený zo **stien**, ktoré sa môžu dotýkať iba na spoločných hranách.
- Každá hrana je **orientovaná** – musí byť jednoznačne určené, či je **vonkajšia** alebo **vnútorná**.

#### Údajová štruktúra (podľa podkladov)
- Objekt je reprezentovaný dynamickou údajovou štruktúrou **Winged Edge Structure**.
- Uvádzajú sa **4 druhy uzlov**:
  1. **Vrchol (Vertex)**
  2. **Hrana (Edge)**
  3. **Stena / plocha (Face)**
  4. **Teleso (Solid)**

---

## 24. Konštruktívna geometria telies (CSG)

### Základná charakteristika
- **CSG (Constructive Solid Geometry)** je definovaná abstraktnou údajovou štruktúrou – **stromom**.

### Časti stromu (podľa podkladov)
- **Listy**: atomárne elementy, z ktorých sa objekt skladá.
- **Uzly**: operácie medzi elementami/objektmi/subobjektami na danej úrovni stromu:
  - **zjednotenie**
  - **rozdiel**
  - **prienik**
- **Hrany**: transformácie atomárnych elementov / subobjektov vstupujúcich do rodičovského uzla.
- **Koreň**: výsledný celý objekt.

### Typy stromu (podľa podkladov)
- Strom môže byť:
  - **cyklický (B)** – môže byť viac časovo náročný,
  - **acyklický (A)** – viac pamäťovo náročný.

Poznámky z podkladov:
- Jeden objekt môže vzniknúť viacerými postupmi (rôzne „stavy“) a na začiatku sa nemusí dať jednoducho povedať, či ide o „to isté“.
- Strom sa typicky **vyhodnocuje zdola nahor**.

---

## 25. Súradnicová sústava priestoru, súradnicové sústavy používané v počítačovej grafike, súradnicový reťazec

### Čo je súradnicová sústava (základné časti)
Súradnicová sústava umožňuje parametrizovať priestor a definovať jeho počiatočný bod. Podľa podkladov ju tvoria:
1. **Počiatok (ORIGIN)** – stred súradnicovej sústavy
2. **Os** – definuje smer rozvoja fyzikálnej veličiny v príslušnej dimenzii priestoru  
   - poznámka: os nemusí byť len priamka, môže to byť aj krivka
3. **Súradnice (parametre)** – jednoznačne definujú polohu v rámci súradnicovej sústavy  
   - počet súradníc závisí od počtu dimenzií priestoru

### Delenie súradnicových sústav (podľa podkladov)

**Podľa rozvoja hodnôt veličín dimenzií:**
1. **Lineárne súradnicové sústavy**
2. **Nelineárne súradnicové sústavy**

**Podľa vzťahu osí súradnicového systému:**
1. **Pravouhlé**
2. **Nepravouhlé**

Poznámka z podkladov:
- Pre počítačovú grafiku sa primárne používajú **celočíselné translačné alebo rotačné lineárne** súradnicové sústavy, najčastejšie **lineárne pravouhlé kombinované**.

### Typické druhy (podľa podkladov)
- **Karteziánska**: pravouhlá, translačná, lineárna
- **Polárna** (a v 3D **sférická**): rotačná, lineárna

Podklady uvádzajú aj príklady podľa dimenzie:
- **2D (topologicky 2+0)** translačná pravouhlá lineárna súradnicová sústava
- **3D (topologicky 3+0)** translačná pravouhlá lineárna súradnicová sústava
- **4D (topologicky 4+0)** translačná pravouhlá lineárna súradnicová sústava (projekcia do 3D, „disfenoid“)

### Základné súradnicové sústavy používané v počítačovej grafike (pracovné priestory)
V podkladoch sú uvedené tieto „základné“ sústavy:
1. **USS** – univerzálna (používateľská, globálna) súradnicová sústava
2. **SSO** – súradnicová sústava objektu
3. **NSS** – normalizovaná súradnicová sústava (kontrola limitov)
4. **SSZ** – súradnicová sústava zariadenia (monitor, hologram)
5. **SSC** – súradnicová sústava kamery
6. **SST** – súradnicová sústava textúry

### Súradnicový reťazec (idea z podkladov)
- Súradnicový reťazec predstavuje **vzťahy medzi jednotlivými pracovnými priestormi** – typicky od súradnicovej sústavy objektu až po súradnicovú sústavu zariadenia (SSO → ... → SSZ).

---

## Rýchle skúškové zhrnutie (čo vedieť povedať)
- Stále 1. úroveň vizualizačného procesu: priestor, parametre, popis a reprezentácia objektov.
- Priestor: translačný/rotačný/kombinovaný; dimenzie celočíselné vs neceločíselné; štruktúra homogénna (N+0) vs heterogénna (N1+...+Nn), často geometria+čas.
- Objekty podľa dimenzie: 0D bod, 1D úsečka/priamka, 2D plocha, 3D teleso; spojité transformácie a reprezentácia podľa topologickej dimenzie.
- Spôsoby popisu telies: hraničná reprezentácia (B-rep), CSG, obsadené časti priestoru (v podkladoch: už sa nepoužíva); plus rozdelenie na point clouds, wireframe, surface, solid.
- Hraničná reprezentácia: hranice (hrany/povrch); typy plôch; drôtový model môže byť nejednoznačný; B-rep: povrch zo stien, dotyk len na hranách, orientované hrany; Winged Edge Structure (Vertex, Edge, Face, Solid).
- CSG: strom – listy (atomárne prvky), uzly (zjednotenie/rozdiel/prienik), hrany (transformácie), koreň (objekt); strom cyklický vs acyklický; vyhodnocovanie zdola nahor.
- Súradnicové sústavy: počiatok, osi, súradnice; delenie lineárne/nelineárne, pravouhlé/nepravouhlé; typy karteziánska, polárna/sférická; pracovné sústavy USS, SSO, NSS, SSZ, SSC, SST; súradnicový reťazec = vzťahy medzi nimi (najmä SSO → SSZ).
