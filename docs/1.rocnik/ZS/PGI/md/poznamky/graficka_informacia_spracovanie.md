# Grafická informácia a jej spracovanie (otázky 14 - 21)

_[Zdroj: PG_2021_Otazky_z_predmetu.pdf, skuska2023.pdf, prednasky.pdf]_

---

## 14. Grafická informácia po objektovej aj typovej stránke

### Súvis s vizualizačným procesom
- Ide o **1. krok vizualizačného procesu** (pracujeme s tým, *čo* je v scéne a *ako* to vieme popísať/reprezentovať).

### Grafická informácia z pohľadu objektov (čo riešime pri objektoch)
V podkladoch je grafická informácia (objekty) rozdelená na:
1. **Typy**
2. **Primitíva**
   - implementácia primitív  
   - filtračné a rozptyľovacie metódy
3. **Popis objektu**
4. **Reprezentácia objektu**
5. **Priestor objektu**

### Grafická informácia z pohľadu typu (vektor vs raster)
- **Vektorová** (spojitý priestor) – „krajšia“ (presnejší popis funkciami/krivkami).
- **Rastrová** (nespojitý priestor) – „ľahšie vyrobiteľná“ (pracuje priamo s bodmi/pixelmi).

### Zväčšenie (škálovanie) – rozdiel medzi typmi
- **Vektorové**: zväčšenie bez straty informácie (v ideálnom zmysle).
- **Rastrové**: zväčšenie vedie k strate/rozmazaniu/kockateniu (strata informácií).

---

## 15. Základné 2D grafické primitíva a ich atribúty

### Základné grafické primitíva (podľa podkladov)
Pozn.: „prvé 2 sú raster aj vektor“, ostatné sú uvádzané ako vektorové.
1. **Bod**
2. **Sled bodov**
3. **Krivka**
4. **Lomená čiara**
5. **Grafický text**
6. **Plocha**
7. **Vyplnená oblasť**
8. **Výplňový vzor**
9. **Všeobecný grafický prvok**

### Atribúty primitív (čím riadime konečný tvar/vzhľad)
- **Farba**
- **Typ** (napr. typ čiary, typ písma a pod.)
- **Hrúbka** (napr. čiary, písma)
- **Poloha** (napr. písma)
- **Smer vykreslenia** (napr. horizontálny, vertikálny, ...)

### Ako sa priraďujú atribúty
Atribúty môžu byť priradené:
1. **Konvenčne / individuálne / pevne**  
   - môže viesť k nekompatibilite na rôznych zobrazovačoch.
2. **Symbolicky (kódom)** → **viazané (bundled) atribúty**  
   - voči zobrazovaciemu zariadeniu „transparentné“.

---

## 16. Spracovanie bodu a sledu bodov v rámci počítačovej grafiky

### Bod
- **Elementárny (atomárny) objekt**, **0-rozmerný**.
- Základné atribúty: **poloha** a **farba**, prípadne **čas** (ak sa uvažuje heterogénna štruktúra dimenzie priestoru).

#### Typy bodu (podľa podkladov)
- **Pixel**: obrazový bod charakterizovaný **dvomi súradnicami** polohy a **farbou**; najmenšia jednotka digitálnej rastrovej grafiky.
- **Voxel**: objemový bod (pixel v 3D) charakterizovaný **tromi polohovými súradnicami** a farbou.
- **Texel**: bod textúry; má polohu v SST (súradnicovej sústave textúry) + polohu v rámci výplňového vzoru (textúry) + reláciu priradenia k vypĺňanej oblasti.

### Fyzické vytvorenie bodu, rozlíšenie
- Na rastrovom zariadení (napr. monitor) je pixel vytvorený rozsvietením istej množiny **fyzických bodov** výstupnej jednotky.
- Jemnosť/hustota fyzických bodov ovplyvňuje kvalitu zobrazenia.
- Uvádza sa v **PPI (Pixel Per Inch)** alebo **DPI (Dot Per Inch)** (podľa zariadenia).

### Sled bodov (polymarker)
- Rozširujúci prvok nadväzujúci na bod.
- **Logicky zviazaná množina bodov** na základe relácie medzi prislúchajúcimi atribútmi bodov.
- Operácie sa chápu tak, že sa dejú **nad všetkými bodmi spolu**.

#### Typ relácie medzi atribútmi bodov polymarkra
- **Homogénna**: relácia medzi rovnakými atribútmi (napr. poloha ↔ poloha).
- **Heterogénna**: relácia medzi rôznymi atribútmi (napr. farba jedného bodu závisí od polohy druhého).

### Krivka a lomená čiara (doplnenie z podkladov pri spracovaní 1D útvarov)
- Ide o **1D útvar** definovaný **vrcholmi a hranami**:
  - **neuzavretý (acyklický)**: krivka (polyline),
  - **uzavretý (cyklický)**: plocha (polygon).
- Podľa typu hrán:
  - **lineárny**: všetky segmenty lineárne,
  - **nelineárny**: stačí jeden nelineárny segment.
- Podľa vplyvu vrcholov na tvar:
  - **interpolačné**: vrcholy sú súčasťou krivky,
  - **aproximačné**: vrcholy nemusia ležať na krivke, ale ovplyvňujú jej tvar.

---

## 17. DDA algoritmus

### Kontext: generovanie úsečky v rastrovej grafike
V podkladoch sa uvádza rovnica úsečky na priamke:
- **y = k · x + c**

Pri kreslení úsečky existujú viaceré prístupy:
- „štandardný algoritmus“: prechádzam po **x** a dopočítavam **y** podľa rovnice,
- **DDA (Digital Differential Analyzer)**,
- **Bresenhamov algoritmus**.

### DDA (Digital Differential Analyzer)
- **Prírastkový algoritmus** založený na postupnom pripočítavaní **konštantných prírastkov** k obom súradniciam **x** a **y**.
- Rozlišuje sa postup podľa smernice:
  - **smernica menšia ako 1**,
  - **smernica väčšia ako 1**.

---

## 18. Bresenhamov algoritmus

- Veľmi **efektívny** algoritmus generovania bodov na úsečke v rastrovej grafike.
- Hľadá body ležiace najbližšie skutočnej úsečke pomocou **predikčného chybového člena** (v podkladoch označený **ED**).
- Rieši sa pre dva prípady:
  - **smernica menšia ako 1**,
  - **smernica väčšia ako 1**.

Poznámky z podkladov (intuícia rozhodovania):
- V každom kroku sa „posúva“ po **riadiacej osi** (x alebo y) o 1 a podľa chyby sa rozhoduje, či sa upraví aj druhá súradnica.
- Spomína sa rozhodovanie „okolo 0.5“: ak je výsledok do 0.5 zostáva sa v danom riadku, ak je väčší, prejde sa do nového riadku (interpretácia zaokrúhľovania výberu najbližšieho bodu).

---

## 19. Spracovanie kružnice a elipsy v rámci počítačovej grafiky a základné metódy ich generovania

### Kružnica
- Kružnica je **množina bodov rovnako vzdialených od stredového bodu**.

**Metódy generovania (podľa podkladov):**
1. Algoritmus kreslenia kružnice na základe **parametrického vyjadrenia**.
2. Algoritmus kreslenia kružnice podľa **predikcie chyby** (analógia k Bresenhamovi; zaokrúhľovanie a voľba bodu v pôvodnom alebo novom riadku/stĺpci).
3. Algoritmus kreslenia kružnice využitím **osovej súmernosti** (v podkladoch označené ako najrýchlejšie):
   - kružnica je osovo súmerná,
   - netreba počítať celých 360°,
   - stačí počítať do približne **45°** a zvyšok doplniť súmernosťou.

### Elipsa
- Elipsa je **množina bodov rovnako vzdialených od dvoch ohnísk** (v podkladoch takto uvedené).

**Metódy generovania (podľa podkladov):**
1. Parametrické vyjadrenie.
2. Predikcia chyby.
3. Osová súmernosť (v podkladoch: výpočet do **90°** a zvyšok súmernosťou).

### Kružnicové/eliptické oblasti (podľa podkladov)
- **výsek**, **oblúk**, **odsek**

---

## 20. Antialiasing

### Čo je aliasing (prečo vzniká problém)
- Keď máme **vektorový objekt** a vykresľujeme ho na **rastrový** monitor, vzniká rastrová náhrada (**alias**).
- Aliasovanie sa prejavuje ako **kostrbatosť / schodíkovosť** hrán.

### Typické prípady aliasingu (z podkladov)
- Schodovité zobrazovanie priamych čiar a hraníc polygónov na rastrových displejoch.
- Zobrazovaný objekt je menší ako veľkosť pixelu:
  - malé objekty sa nemusia vôbec zobraziť,
  - tenké čiary nemusia byť opticky hladké/ucelené (nepravidelná postupnosť bodov).
- Pri zložitejšej scéne s blízkymi detailmi (napr. základné obrázky z raytracingu):
  - detaily sú potlačené alebo skreslené (v podkladoch spomenuté aj v súvislosti s LOD).

### Pointa antialiasingu
- Antialiasing je proces, ktorý sa snaží znížiť tieto alias artefakty (vyhladiť hrany).
- Podklady uvádzajú, že namiesto neho alebo spolu s ním sa používajú aj **filtrovacie a rozptyľovacie techniky**.

---

## 21. Filtrovacie a rozptyľovacie metódy, medián filter, poltónovanie, dithering, distribúcia chyby pri rozptyľovaní

### Prečo sa používajú (motivácia z podkladov)
- Riešia rozdiel medzi požadovanou kvalitou výsledných obrazov a:
  - obmedzenými možnosťami farebného priestoru zariadenia,
  - alebo technikami používanými na podporu antialiasingu.

### Základné rozdelenie (podľa podkladov)
a) **Rozptyľovanie** – **dithering**  
- použitie viacerých farieb (vzorovanie).

b) **Poltónovanie** – **halftoning**  
- používa len **2 farby**.

### Medián filter
- V podkladoch je uvedený ako príklad **filtrovacej metódy** (bez ďalších detailov v dodanom texte).

### Distribúcia chyby pri rozptyľovaní
- Podklady uvádzajú „distribúciu chyby“ ako súčasť rozptyľovacích techník (v dodanom texte bez rozpisu konkrétnych pravidiel).

---

## Rýchle skúškové zhrnutie (čo vedieť povedať)
- Grafická informácia (1. krok vizualizácie): typy + primitíva + implementácia primitív + filtračné/rozptyľovacie metódy + popis/reprezentácia + priestor objektu.
- Typy grafiky: vektorová (spojitá, „krajšia“) vs rastrová (nespojitá, „ľahšie vyrobiteľná“); zväčšenie: vektor bez straty, raster so stratou.
- Primitíva: bod, sled bodov, krivka, lomená čiara, text, plocha, vyplnená oblasť, výplňový vzor, všeobecný prvok.
- Atribúty: farba, typ, hrúbka, poloha, smer vykreslenia; priraďovanie: konvenčne (možná nekompatibilita) vs symbolicky (bundled).
- Bod: 0D; atribúty poloha+farba (+čas); pixel/voxel/texel; PPI/DPI; polymarker = logicky zviazané body (homogénna vs heterogénna relácia).
- Úsečka: existuje štandardný výpočet y=kx+c, DDA a Bresenham.
- DDA: prírastkový, konštantné prírastky do x a y; prípady smernica <1 a >1.
- Bresenham: efektívny, predikčný chybový člen ED, voľba najbližšieho bodu; prípady smernica <1 a >1.
- Kružnica/elipsa: parametrické vyjadrenie, predikcia chyby, osová súmernosť (kružnica do ~45°, elipsa do 90°); oblasti: výsek, oblúk, odsek.
- Antialiasing: riešenie schodíkovosti pri prevode vektora na raster; problémy pri tenkých čiarach, malých objektoch a jemných detailoch; súvis s filtráciou/rozptyľovaním.
- Filtrovanie/rozptyľovanie: dithering (viac farieb), halftoning (2 farby), medián filter, distribúcia chyby (uvedené v podkladoch).
