# Krivky a plochy v počítačovej grafike (otázky 42 - 49)

_[Zdroj: PG_2021_Otazky_z_predmetu.pdf, skuska2023.pdf, prednasky.pdf]_

---

## 42. Krivky používané v počítačovej grafike, spôsob využitia, 1D krivkové útvary

### Zaradenie vo vizualizačnom procese
Krivky (a neskôr plochy) patria typicky do:
- **1. vrstvy** – definovanie/spracovanie modelu (geometrická reprezentácia),
- **2. vrstvy** – transformácie nad objektami (krivky/plochy sa transformujú rovnako ako iná geometria).

### Základné typy kriviek (podľa spôsobu popisu)
- **Krivky dané analytickým popisom** (dané funkciou/rovnicou).
- **Interpolačné krivky** – riadiace body (vrcholy) *sú súčasťou* krivky (krivka nimi prechádza).
- **Aproximačné krivky** – riadiace body nemusia ležať na krivke, ale *ovplyvňujú jej tvar*.

### Spôsob využitia kriviek (na čo sa používajú)
- **Geometrická reprezentácia** – krivka je priamo súčasť modelu (obrys, hrana, profil).
- **Riadiaca funkcia** – krivka riadi niečo iné (napr. trajektóriu pohybu).

**Príklad (riadiaca funkcia):** trajektória lietadla/drónu môže byť definovaná krivkou – objekt sa „hýbe po krivke“.

### 1D krivkové útvary
#### Polyline (lomená čiara)
1D útvar definovaný **vrcholmi a hranami (segmentmi)**:
- **neuzavretý (acyklický)** – min. 2 vrcholy,
- **uzavretý (cyklický)** – min. 3 vrcholy (najjednoduchší je trojuholník).

Podľa typu segmentov:
- **lineárny** – *lineárny je iba vtedy*, ak sú **všetky** segmenty lineárne,
- **nelineárny** – stačí jeden nelineárny segment a celý útvar je nelineárny.

Podľa vplyvu vrcholov na tvar:
- **interpolačný** – vrcholy sú súčasťou krivky,
- **aproximačný** – vrcholy nemusia byť súčasťou krivky, ale určujú jej tvar.

### Používané krivky (prehľad zo skrípt)
- **lineárne**: lineárna interpolácia, lomená čiara,
- **nelineárne**:
  - Bézierove krivky stupňa *n*,
  - racionálne Bézierove krivky stupňa *n*,
  - B-spline krivky stupňa *n*,
  - kubické B-spline krivky (uniformné / neuniformné),
  - racionálne B-spline krivky stupňa *n* (najzložitejšie).

### Modifikovateľnosť kriviek
Krivky je možné modifikovať najmä:
- **zmenou polohy riadiacich vrcholov**,
- **zmenou váh riadiacich vrcholov**,
- **modifikáciou uzlového vektora**.

---

## 43. Fergusonova krivka

### Charakteristika
- **Interpolačná krivka**, nelineárna.
- Spájaná s **James Ferguson (1963)**.
- V materiáloch sa spomína použitie (napr. „krídlo Boeingu“).

### Definícia (podľa podkladov)
Je definovaná **4 základnými vektormi**:
- **G, H** – polohové vektory začiatku a konca,
- **g, h** – dotyčnicové (tangent) vektory v bodoch G a H (štartový a koncový).

### Poznámka z podkladov
- uvádza sa **príliš veľká citlivosť pre zaoblenie** (t. j. malé zmeny dotyčníc môžu výrazne meniť tvar).

---

## 44. Bézierove krivky

### Charakteristika (kubická Bézierova krivka)
- **Aproximačná** krivka, typicky uvádzaná ako **kubická**.
- Spájaná s **Pierre Bézier (1960s)** (v materiáloch sa spomína Citroën).
- **Interpoluje koncové vrcholy** (prechádza začiatočným a koncovým bodom), ostatné riadiace body určujú „zaoblenie“.

### Vlastnosti uvádzané v materiáloch
- Definovaná **polynomiálnou funkciou stupňa n** (v poznámkach: „n = počet riadiacich vrcholov“).
- Krivka **leží v konvexnom obale** riadiacich vrcholov.
- **Pseudolokálna kontrola** – posun riadiaceho vrcholu mení krivku najmä v jeho okolí.
- **Afinná invariancia** – ak aplikujem afinnú transformáciu na riadiace body (napr. otočenie), zachová sa tvar krivky (transformuje sa spolu s nimi).

**Príklad (afinná invariancia):** ak chcem krivku otočiť, stačí otočiť jej riadiace body a krivka sa „otočí správne“.

---

## 45. Spline, Catmull-Rom spline a B-spline krivka

### Spline (všeobecne)
- Spline krivka je (v podkladoch) popísaná funkciou **f(x)**, ktorá je po intervaloch polynóm:
  - na intervale ⟨x_k, x_{k+1}⟩ platí **f(x) = f_k(x)**, kde **f_k** je polynóm stupňa **m**,
  - spline má **spojité derivácie** až do rádu **(m−1)**.
- Najčastejšie sa používajú **kubické spline funkcie** (**m = 3**).
- V poznámkach sa uvádza, že spline je „aproximačná (vychádza z Bézierovej)“ a má **hladko nadväzujúce segmenty**.

### Catmull-Rom spline
V materiáloch sa uvádza ako spline typ (najmä v druhom bloku poznámok):
- patrí medzi **interpolačné krivky** (prechádza riadiacimi bodmi).

(Ďalšie detaily v dodaných poznámkach nie sú rozpracované, preto sa držíme tejto charakteristiky.)

### B-spline krivka
- B-spline je zovšeobecnenie Bézierových kriviek; v podkladoch sa uvádza, že:
  - namiesto Bernsteinových polynómov sa používajú „jednoduchšie funkcie“,
  - je „hladšia ako Bézier“, ale „ťažšie sa ovláda“.
- Vlastnosti:
  - **aproximačná**, často uvádzaná ako **uniformná**,
  - **pseudolokálna kontrola** a **segmentovateľnosť** (dá sa rozbiť na segmenty nižšieho rádu so spojitými deriváciami),
  - **afinná invariancia**.

Poznámka z materiálov k začiatku/koncu krivky:
- uvádza sa, že špeciálnym zadaním **násobností** (uzlového vektora) sa dá dosiahnuť, že krivka začne/končí v určených bodoch,
- zároveň sa spomína nevýhoda, že bez úprav krivka nemusí začínať a končiť v prvom/poslednom bode riadiaceho polygónu; „odstráni sa“ zmenou násobností prvých a posledných prvkov uzlového vektora.

---

## 46. NURBS krivky

V podkladoch sa NURBS objavujú v prehľade ako:
- **racionálne B-spline krivky stupňa n** (uvádzané ako „najzložitejšie“),
- spolu s tým sa uvádza modifikovateľnosť cez:
  - polohu riadiacich vrcholov,
  - váhy,
  - uzlový vektor.

Prakticky: ide o krivky, kde sa okrem riadiacich bodov pracuje aj s **váhami** a **uzlovým vektorom**, čo dáva širšie možnosti tvarovania.

---

## 47. Plochy používané v počítačovej grafike, 2D plošné útvary, modifikovateľnosť plôch

### Základné typy plôch (podľa spôsobu popisu)
- **Plochy dané analytickým popisom**
- **Interpolačné plochy**
- **Aproximačné plochy**

### 2D plošné útvary
V podkladoch sa ako základ uvádza **polygón** (2D útvar definovaný vrcholmi a hranami):
- **lineárny** – všetky segmenty musia byť lineárne (najjednoduchší lineárny je **trigón** – trojuholník),
- **nelineárny** – najjednoduchší nelineárny sa v poznámkach uvádza ako **digón**.

### Používané plochy (prehľad zo skrípt)
- **lineárne**: rovinné (pravítkové) plochy,
- **nelineárne**:
  - Bézierove plochy,
  - B-spline plochy,
  - racionálne B-spline plochy,
  - uniformné / neuniformné varianty.

### Modifikovateľnosť plôch
Analogicky ako krivky:
- zmena polohy riadiacich vrcholov,
- zmena váh riadiacich vrcholov,
- modifikácia uzlových vektorov.

### Príklady použitia (zo skrípt)
- **povrchy/terén** (digitálny terén, 3D skenovanie terénu),
- **3D skenovanie a 3D tlač**,
- medzi príklady analytických plôch sa uvádzajú napr. **guľovitá** a **elipsovitá**.

Poznámka k pojmom z podkladov:
- **Morphing**: proces „prechodu medzi tvarmi“,
- **Warping**: „prebratie tvaru“ (cieľového tvaru),
- v poznámkach sa uvádza, že často stačí morfovať **len riadiace vrcholy**.

---

## 48. Coonsova bilineárna plocha

### Charakteristika
- **Coonsova bilineárna plocha** je všeobecnejšia ako pravítková plocha:
  - ak sú protiľahlé strany úsečky, dostaneme **priamkovú (pravítkovú) plochu**.
- V materiáloch je popísaná cez **9 riadiacich bodov**, čo zodpovedá matici **3×3**.

### Parametrizácia a výpočet (podľa podkladov)
- používa sa dvojica parametrov **(u, w)**,
- výpočet sa typicky realizuje ako:
  - **dvojitý cyklus** (cez u, w),
  - pre každú zložku súradníc (**x, y, z**),
- v poznámkach sa spomína „hlavná vypuklosť“ (dominantný vplyv stredového bodu P(u,w) v strede).

Poznámka z ďalších poznámok:
- uvádza sa, že problémom môže byť náročnejšie dosiahnuť **hladké spojenie dvoch plôch** (kvôli dotyčnicovým vektorom).

---

## 49. Bézierová bikubická plocha

### Charakteristika
- Základná Bézierova plocha sa uvádza ako **Bézierova bikubická plocha**.
- Je daná maticou **4×4 riadiacich bodov**, teda **16 uzlov** \(B_{ij}, i,j = 0..3\).
- V podkladoch sa uvádza, že plocha je definovaná **explicitnou rovnicou** (bez potreby ju tu rozpisovať).

Praktická poznámka zo zhrnutia:
- Bézierove plochy sú vhodné na **hladké povrchy**, manipulácia je „ľahká“ cez riadiace body,
- priamy výpočet niektorých operácií môže byť náročný (v poznámkach sa uvádza napr. priesečník s čiarami ako bariéra pre niektoré geometrické techniky).

---

## Rýchle skúškové zhrnutie (čo vedieť povedať)

- Krivky (a plochy) patria do **1. vrstvy (model)** a **2. vrstvy (transformácie)** vizualizačného procesu.
- Typy kriviek/plôch: **analytické**, **interpolačné**, **aproximačné**.
- Použitie kriviek:  
  - **geometrická reprezentácia** (časť objektu),  
  - **riadiaca funkcia** (trajektória, riadenie pohybu).
- 1D útvar **polyline**: acyklický/cyklický, lineárny/nelineárny, interpolačný/aproximačný.
- Fergusonova krivka: **interpolačná**, definovaná (G,H) a dotyčnicami (g,h).
- Bézierova krivka: **aproximačná**, interpoluje koncové body; **konvexný obal**, **pseudolokálna kontrola**, **afinná invariancia**.
- Spline: po intervaloch polynóm, dôležité sú **spojité derivácie**, často **kubické**.
- B-spline: zovšeobecnenie Bézier; „hladšie“, segmentovateľné, pseudolokálna kontrola; dá sa ovplyvniť **uzlovým vektorom** (násobnosti).
- NURBS: v podkladoch ako **racionálne B-spline** (váhy + uzlový vektor + riadiace body).
- Plochy: analytické/interpolačné/aproximačné; polygón lineárny (trigón) / nelineárny (digón); modifikácia cez **riadiace body, váhy, uzly**.
- Coons bilineárna plocha: **3×3 (9 bodov)**, parametre **u,w**, výpočet dvojitým cyklom; všeobecnejšia než pravítková plocha.
- Bézier bikubická plocha: **4×4 (16 bodov)**, definovaná explicitne (v podkladoch).
