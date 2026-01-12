# PGI – otázky 1–80 (stručne)

`Legenda statusu skúšajúcich otázok:`

- 🟢 najčastejšie
- 🟠 často
- 🔴 občas

---

### Okruhy:

- `1 - 13:` Priestor, svetlo a farby
- `14 - 21:` Grafická informácia a jej spracovanie
- `22 - 25:` Grafický priestor a objekty
- `26 - 35:` Transformácie v počítačovej grafike
- `36 - 41:` Projekčné a zobrazovacie transformácie
- `42 - 49:` Krivky a plochy v počítačovej grafike
- `50 - 60:` Riešenie viditeľnosti v počítačovej grafike
- `61 - 68:` Vyplňovanie oblastí a textúrovanie
- `69 - 77:` Tieňovanie, osvetľovanie a fotorealistické zobrazovanie 
- `78 - 80:` Fraktály, časticové systémy, virtuálna realita a XR 

---

## [1 - 13] Priestor, svetlo a farby :

---

### 1. Používanie a spracovanie farieb v počítačovej grafike, atribúty svetla, farebný priestor, gamut

**Status:** 🟢

V počítačovej grafike sa farby používajú na realistické a informatívne zobrazenie objektov a scén. Farba je výsledkom `svetla`, ktoré má základné atribúty:

- `farba (odtieň)` – daná vlnovou dĺžkou,
- `jas` – intenzita svetla,
- `sýtosť` – čistota farby,
- `svetlosť` – podiel achromatickej (bielej) zložky.

`Farebný priestor` je množina farieb, ktoré daný farebný model dokáže popísať (napr. `RGB`).
`Gamut` je reálne dosiahnuteľná časť farebného priestoru – farby mimo gamutu sa dajú zobraziť len približne

---

### 2. Chromatický diagram, typy, odtieň a saturácia

**Status:** 🟢

`Chromatický diagram (`CIE`)` graficky znázorňuje všetky farby, ktoré dokáže vnímať ľudské oko. Je založený na `štandardnom pozorovateľovi` a `tristimulus hodnotách (X, Y, Z)`.

- `Odtieň (hue)` určuje, akú farbu vnímame (červená,, modrá…) – pohyb po kružnici.
- `Saturácia` určuje živosť farby – vzdialenosť od stredu (sivej) k okraju diagramu.

Existujú rôzne typy `CIE` diagramov (1931, 1964, 1976) s rôznym pozorovacím uhlom.

---

### 3. Farebné modely RGB a RGBA

**Status:** 🟢

`RGB model` je založený na `aditívnom miešaní svetla`:

- Red, Green, Blue sú základné zložky,
- zložky sa sčítavajú → čierna = (0,0,0), biela = (1,1,1).

Model sa používa najmä na `monitoroch a displejoch`.
`RGBA` rozširuje `RGB` o `alfa kanál`, ktorý určuje `priesvitnosť` objektu a umožňuje alfa-miešanie.

---

### 4. Farebné modely CMY a CMYK

**Status:** 🟢

- Model `CMY` (Cyan, Magenta, Yellow) používa `subtraktívne miešanie`, typické pre tlač – farby vznikajú `odoberaním svetla z bieleho podkladu`.
- Model `CMYK` pridáva zložku `K – čiernu`, pretože miešaním `CMY` sa nedá dosiahnuť ideálna čierna.
Používa sa hlavne v `tlačových zariadeniach`.

---

### 5. Farebný model HSB

**Status:** 🟢

Model `HSB` (Hue, Saturation, Brightness) je percepčný model, bližší ľudskému vnímaniu farieb:

- `Hue` – farebný tón,
- `Saturation` – sýtosť,
- `Brightness` – jas.

Používa sa najmä v grafických editoroch, kde je výber farby intuitívnejší než v `RGB`. Reprezentovaný je ako šesťboký ihlan.

---

### 6. Farebný model HLS

**Status:** 🟢

Model `HLS (Hue, Lightness, Saturation)` je podobný `HSB`, ale namiesto jasu používa `svetlosť (lightness)`.

- Svetlosť určuje pomer medzi bielou a čiernou,
- model má dvojitú kužeľovú reprezentáciu.

Používa sa tam, kde je dôležité rovnomerné vnímanie zmien svetlosti.

---

### 7. Gama korekcia a alfa-miešanie

**Status:** 🟢

`Gama korekcia` upravuje vzťah medzi uloženou hodnotou pixelu a jeho skutočnou svietivosťou, aby obraz zodpovedal `ľudskému vnímaniu jasu`.

`Alfa-miešanie` kombinuje farby dvoch objektov podľa ich alfa hodnoty (priesvitnosti).

Môže byť:

- lineárne
- nelineárne 

Alfa-miešanie umožňuje plynulé prechody, priehľadnosť a efekty ako dym či oheň.

---

### 8. Ľudský vizuálny vnem a jeho vzťah k počítačovej grafike

**Status:** 🟠

Ľudské oko vníma obraz pomocou:

- `tyčiniek` – citlivé na jas a pohyb,
- `čapíkov` – citlivé na farby (červená, modrá–žltá).

Počítačová grafika využíva vlastnosti ľudského oka – napríklad `dithering`, kde sa z malej vzdialenosti pixely javia ako plynulá farba. Mozog dotvára chýbajúce informácie.

---

### 9. Miešanie a rozptyľovanie farieb (grayscale, halftoning, dithering)

**Status:** 🟠

- `Prevod do šedej škály:` vážený súčet `RGB` zložiek podľa citlivosti oka.
- `Halftoning:` simulácia odtieňov pomocou binárnych bodov (čierna/biela).
- `Dithering:` rozptyľovanie chýb medzi pixely, čím vzniká ilúzia väčšieho počtu farieb.

Tieto techniky znižujú pamäťové nároky a zlepšujú vizuálny dojem.

---

### 10. Ergonómia a symbolika farieb v počítačovej grafike

**Status:** 🟠

Farby majú `psychologický a symbolický význam` – červená upozorňuje, signalizuje správnosť, modrá pôsobí pokojne.

`Ergonómia farieb` rieši čitateľnosť, kontrast a únavu očí. Správne použitie farieb zlepšuje použiteľnosť rozhraní, orientáciu používateľa a znižuje chybovosť.

---

### 11. Dimenzia priestoru a dimenzia objektu, štruktúra dimenzie

**Status:** 🟠

`Dimenzia priestoru` určuje počet nezávislých smerov, v ktorých sa dá pohybovať (napr. 1D, 2D, 3D).
`Dimenzia objektu` je daná dimenziou priestoru, v ktorom existuje – objekt nižšej dimenzie môže existovať vo vyššej (bod v priestore).

`Štruktúra dimenzie` sa zapisuje ako `D = M + N`, napr. geometria + čas:

- homogénna – všetky dimenzie rovnakého typu,
- heterogénna – obsahuje čas alebo inú veličinu

---

### 12. Priestor a jeho súradnicová sústava, stupeň voľnosti

**Status:** 🟠

`Priestor` je definovaný pomocou `súradnicovej sústavy`, ktorá určuje počiatok (origin) a osi.
`Súradnice` jednoznačne určujú polohu bodu v priestore.

`Stupeň voľnosti (DOF)` je počet nezávislých parametrov pohybu objektu:

- v 3D priestore má tuhé teleso 6 DOF (3 translácie + 3 rotácie)

---

### 13. Vrstvy vizualizačného procesu

**Status:** 🟠

`Vizualizačný proces` sa skladá z viacerých vrstiev:

1. definovanie a spracovanie modelu,
2. geometrické transformácie,
3. riešenie viditeľnosti,
4. tieňovanie,
5. osvetľovanie,
6. realistické zobrazovanie,
7. kompozícia a vykresľovanie.

Cieľom je prevod dát na výsledný obraz.

---

## [14 - 21] Grafická informácia a jej spracovanie:

---

### 14. Grafická informácia po objektovej a typovej stránke

**Status:** 🟠

Grafická informácia opisuje čo `zobrazujeme (objekt)` a `ako to zobrazujeme (typ)`.

Základné typy grafickej informácie:

- `rastrová` – obraz zložený z pixelov,
- `vektorová` – objekty popísané matematicky.

Objektová stránka zahŕňa primitíva, ich atribúty, reprezentáciu a priestor.

---

### 15. Základné 2D grafické primitíva a ich atribúty

**Status:** 🟠

`Základné primitíva sú:`

- bod,
- sled bodov,
- čiara, lomená čiara,
- krivka,
- plocha,
- text.

`Atribúty primitív:`

- farba,
- poloha,
- hrúbka,
- typ čiary,
- smer vykreslenia.

Sú základom každého grafického systému.

---

### 16. Spracovanie bodu a sledu bodov v počítačovej grafike

**Status:** 🟠

`Bod` je elementárny grafický objekt s atribútmi poloha a farba.

`Typy bodov:`

- `pixel` – bod rastrovej grafiky,
- `voxel` – objemový bod v 3D,
- `texel` – bod textúry.

`Sled bodov` (polymarker) je logicky zviazaná množina bodov spracovávaná ako celok.

---

### 17. DDA algoritmus

**Status:** 🟢

`DDA (Digital Differential Analyzer)` je inkrementálny algoritmus na vykresľovanie úsečiek v rastrovej grafike.
Pracuje na princípe `postupného pripočítavania konštantných prírastkov` k súradniciam x a y.

Používa sa pre úsečky so smernicou menšou aj väčšou ako 1.

---

### 18. Bresenhamov algoritmus

**Status:** 🟢

`Bresenhamov algoritmus` je efektívny algoritmus na kreslenie úsečiek, ktorý používa iba `celočíselnú aritmetiku`.

Vyberá pixel najbližší ideálnej úsečke na základe `chybového člena`.
Je rýchlejší a presnejší než `DDA`, vhodný pre real-time grafiku.

---

### 19. Spracovanie kružnice a elipsy, metódy generovania

**Status:** 🟠

`Kružnica` je množina bodov rovnako vzdialených od stredu,
`elipsa` je množina bodov s konštantným súčtom vzdialeností od ohnísk.

`Používané metódy:`

- parametrické vyjadrenie,
- inkrementálne algoritmy s predikciou chyby.

Využívajú symetriu na zrýchlenie výpočtu.

---

### 20. Antialiasing

**Status:** 🟠

`Antialiasing` je technika na potlačenie „schodíkového efektu“ vznikajúceho pri rasterizácii.

`Dosahuje sa:`

- vyhladzovaním hrán,
- priemerovaním farieb pixelov,
- alebo rozptyľovacími metódami (`dithering`, `halftoning`).

Cieľom je plynulejší a realistickejší obraz.

---

### 21. Filtrovacie a rozptyľovacie metódy, mediánový filter, poltónovanie, dithering

**Status:** 🟠

Filtrovacie metódy upravujú obraz pomocou lokálneho spracovania pixelov.

- Mediánový filter odstraňuje šum tak, že nahradí hodnotu pixelu mediánom z okolia.

Rozptyľovacie metódy simulujú odtiene pomocou obmedzeného počtu farieb:

- `poltónovanie` (halftoning) používa binárne vzory,
- `dithering` rozptyľuje chybu medzi susedné pixely (napr. Floyd–Steinberg).

Cieľom je lepší vizuálny dojem pri nižšej farebnej hĺbke.

---

## [22 - 25] Grafický priestor a objekty:

---

### 22. Popis a reprezentácia objektov v počítačovej grafike, priestor a jeho parametre

**Status:** 🟠

`Popis objektu` určuje, čo objekt je (geometria, topológia), `reprezentácia` určuje, ako je uložený a spracovaný.

`Priestor môže byť:`

- translačný,
- rotačný,
- kombinovaný.

Objekty sa môžu reprezentovať ako body, hrany, plochy alebo objemy.

---

### 23. Hraničná reprezentácia

**Status:** 🟠

`Hraničná reprezentácia (B-rep)` popisuje objekt pomocou jeho povrchu – hrán, vrcholov a plôch.

`Výhody:`

- presný popis tvaru,
- vhodná pre vizualizáciu.

`Nevýhoda:`

- môže byť nejednoznačná (napr. wireframe).

---

### 24. Konštruktívna geometria telies

**Status:** 🟠

`CSG (Constructive Solid Geometry)` vytvára zložité telesá kombináciou jednoduchých pomocou:

- zjednotenia,
- prieniku,
- rozdielu.

Výsledok sa často reprezentuje stromovou štruktúrou.
Metóda je vhodná pre `presné modelovanie telies`.

---

### 25. Súradnicové sústavy v počítačovej grafike, súradnicový reťazec

**Status:** 🟢

Používajú sa viaceré súradnicové sústavy:

- objektová,
- svetová,
- kamerová,
- projekčná,
- obrazová.

`Súradnicový reťazec` je postup transformácií medzi týmito sústavami, ktoré umožňujú správne zobrazenie objektu na obrazovke.

---

## [26 - 35] Transformácie v počítačovej grafike:

---

### 26. Transformácie a transformačné zobrazovacie reťazce

**Status:** 🟢

Transformácie menia polohu, orientáciu a veľkosť objektov:

- posun,
- otočenie,
- zmena mierky.

`Transformačný reťazec` je sekvencia matíc, ktorými sa objekt prevádza zo svojej lokálnej sústavy až do obrazovej roviny.

---

### 27. Transformácie v zobrazovacích reťazcoch, homogénne súradnice

**Status:** 🟢

Transformácie sa realizujú pomocou `maticového zápisu`.
Na ich zjednotenie sa používajú `homogénne súradnice`, ktoré umožňujú zapísať aj posun ako maticu.

Rozlišujeme `afinné transformácie` – zachovávajú rovnobežnosť priamok

---

### 28. Transformácia zrkadlenia

**Status:** 🟠

`Zrkadlenie` je transformácia, pri ktorej sa objekt preklopí podľa osi alebo roviny.

Mení orientáciu objektu, ale zachováva jeho tvar a rozmery.
Používa sa pri symetriách a modelovaní.

---

### 29. Transformácia posunutia

**Status:** 🟠

`Posunutie (translácia)` mení polohu objektu bez zmeny jeho tvaru a orientácie.

Je definované vektorom posunu a realizuje sa pomocou transformačnej matice v homogénnych súradniciach.

---

### 30. Transformácia zmeny mierky, zväčšenie/zmenšenie rastrového objektu

**Status:** 🟠

`Zmena mierky (škálovanie)` mení veľkosť objektu.

- `rovnomerné` – zachováva pomery,
- `nerovnomerné` – deformuje tvar.

Pri rastrových objektoch môže spôsobiť:

- rozmazanie (interpolácia),
- aliasing pri zmenšení.

---

### 31. Transformácia skosenia, skosenie rastrového objektu

**Status:** 🟠

`Skosenie (shear)` je afinná transformácia, pri ktorej sa objekt „nakloní“ v jednom smere úmerne k druhej osi.
Zachováva rovnobežnosť priamok, ale `mení uhly`.

Pri rastrových objektoch môže skosenie spôsobiť aliasing, preto sa používa interpolácia.

---

### 32. Transformácia otočenia

**Status:** 🟠

`Otočenie (rotácia)` mení orientáciu objektu okolo zvoleného bodu alebo osi.
V 2D ide o otočenie okolo bodu, v 3D okolo osi.

Realizuje sa pomocou rotačných matíc a zachováva tvar aj veľkosť objektu

---

### 33. Otáčanie okolo všeobecnej priamky, Eulerove uhly, gimbal lock, kvaternióny

**Status:** 🟠

Otáčanie okolo všeobecnej priamky sa často realizuje pomocou `Eulerových uhlov` (rotácie okolo osí X, Y, Z).

Nevýhodou je `gimbal lock` – strata jedného stupňa voľnosti.
`Kvaternióny` tento problém riešia a umožňujú plynulé a stabilné rotácie v 3D priestore.

---

### 34. Transformácia otočenia rastrového objektu

**Status:** 🟠

Pri rotácii rastrového objektu sa prepočítavajú polohy pixelov.
Výsledok si vyžaduje `interpoláciu hodnôt`, inak vzniká aliasing alebo „diery“ v obraze.

Často sa používa spätné mapovanie pixelov.

---

### 35. Morphing, warping

**Status:** 🟠

`Morphing` je plynulý prechod medzi dvoma tvarmi alebo obrazmi.
`Warping` je deformácia obrazu na základe mapovania bodov.

Používajú sa v animáciách, špeciálnych efektoch a prechodoch medzi objektmi.

---

## [36 - 41] Projekčné a zobrazovacie transformácie:

---

### 36. 2D premietacie transformácie, logická a fyzická pracovná oblasť, kamera

**Status:** 🟢

2D premietacie transformácie mapujú objekty z `logickej pracovnej oblasti` do `fyzickej oblasti` (obrazovky).

Kamera určuje pohľad na scénu a jej rotácia sa často realizuje pomocou `Eulerových uhlov`.

---

### 37. Orezávacie algoritmy, Cohen–Sutherlandov algoritmus

**Status:** 🟢

`Orezávanie (clipping)` odstraňuje časti objektov mimo zobrazovanej oblasti.

`Cohen–Sutherlandov algoritmus` používa kódovanie koncových bodov úsečky a rýchlo rozhoduje, či je úsečka:

- úplne viditeľná,
- úplne neviditeľná,
- alebo čiastočne viditeľná.

---

### 38. Kolmá (ortografická) projekcia, Mongeova projekcia

**Status:** 🟢

`Kolmá (ortografická) projekcia` zobrazuje objekt bez perspektívneho skreslenia – zachováva rozmery.

`Mongeova projekcia` používa viac pohľadov (pôdorys, nárys, bokorys) a je typická pre technické kreslenie.

---

### 39. Axonometria

**Status:** 🟢

`Axonometria` je druh rovnobežného premietania, kde sú viditeľné tri osi priestoru.

`Typy:`

- izometrická,
- dimetrická,
- trimetrická.

Používa sa v technických a herných vizualizáciách.

---

### 40. Perspektíva

**Status:** 🟢

`Perspektívna projekcia` simuluje ľudské videnie – vzdialenejšie objekty sa javia menšie.

`Základné prvky:`

- stred premietania,
- obrazová rovina,
- úbežníky.

Používa sa v realistickej 3D grafike a hrách.

---

### 41. Nelineárne premietacie transformácie, distorzia obrazu, rybie oko

**Status:** 🔴

`Nelineárne projekcie` nedeformujú obraz lineárne – vzdialenosti a uhly sa nemenia rovnomerne.
Používajú sa pri `distorzii obrazu`, napr. efekt `rybieho oka`, kde sa obraz rozťahuje smerom k okrajom.

Využitie: špeciálne efekty, širokouhlé kamery, `VR`.

---

## [42 - 49] Krivky a plochy v počítačovej grafike:

---

### 42. Krivky používané v počítačovej grafike, spôsob využitia, 1D krivkové útvary

**Status:** 🟠

Krivky v CG slúžia na `plynulý popis tvarov`.
Sú to `1D útvary` definované v 2D alebo 3D priestore.

`Použitie:`

- modelovanie tvarov,
- animácie,
- trajektórie pohybu,
- fonty a obrysy objektov.

---

### 43. Fergusonova krivka

**Status:** 🔴

`Fergusonova krivka` je kubická interpolujúca krivka definovaná:

- dvoma koncovými bodmi,
- dvoma tangentami v týchto bodoch.

Krivka prechádza presne cez zadané body a umožňuje kontrolu tvaru pomocou smerníc.

---

### 44. Bézierove krivky

**Status:** 🔴

`Bézierove krivky` sú definované riadiacimi bodmi.

Krivka:

- prechádza prvým a posledným bodom,
- leží v konvexnom obale riadiacich bodov.

Používajú sa v grafických editoroch, fontoch a animáciách pre jednoduché a stabilné modelovanie.

---

### 45. Spline, Catmull–Rom spline a B-spline

**Status:** 🔴

`Spline krivky` sú zložené z viacerých polynómových segmentov.

- `Catmull–Rom spline` interpoluje všetky riadiace body,
- `B-spline` je aproximujúca krivka – poskytuje vysokú hladkosť a lokálnu kontrolu.

Používajú sa v modelovaní a animácii.

---

### 46. NURBS krivky

**Status:** 🔴

`NURBS (Non-Uniform Rational B-Splines)` sú univerzálne krivky, ktoré dokážu presne reprezentovať aj kružnice a elipsy.

Umožňujú:

- váhovanie riadiacich bodov,
- vysokú presnosť a flexibilitu.

Používajú sa v CAD systémoch

---

### 47. Plochy používané v počítačovej grafike, 2D plošné útvary

**Status:** 🔴

`Plochy` sú 2D útvary definované v 3D priestore.
Slúžia na modelovanie povrchov objektov.

Dôležitá je ich `modifikovateľnosť` – schopnosť meniť tvar pomocou riadiacich parametrov.

---

### 48. Coonsova bilineárna plocha

**Status:** 🔴

`Coonsova plocha` je definovaná štyrmi hraničnými krivkami.
Vnútro plochy sa vypočíta interpoláciou medzi hranami.

Používa sa na jednoduché modelovanie hladkých povrchov.

---

### 49. Bézierová bikubická plocha

**Status:** 🔴

`Bikubická Bézierova plocha` je definovaná maticou `4×4 riadiacich bodov`.

Umožňuje plynulé prechody a presnú kontrolu tvaru povrchu.
Používa sa v 3D modelovaní a animáciách.

---

## [50 - 60] Riešenie viditeľnosti v počítačovej grafike:

---

### 50. Problém riešenia viditeľnosti a jeho kategorizácia

**Status:** 🟠

Riešenie viditeľnosti určuje, `ktoré časti objektov sú viditeľné z pohľadu kamery`.

Kategórie riešení:

- objektové metódy,
- obrazové metódy,
- hybridné metódy.

Je kľúčové pre správne vykreslenie 3D scény.

---

### 51. Algoritmus plávajúceho horizontu

**Status:** 🔴

`Algoritmus plávajúceho horizontu` rieši viditeľnosť pri zobrazovaní funkcií a terénov.
Udržiava sa `horný a dolný horizont` už vykreslených častí a nové body sa kreslia len vtedy, ak sú mimo týchto hraníc.

Používa sa hlavne pri `drôtových modeloch a terénoch`.

---

### 52. Maliarov algoritmus riešenia viditeľnosti

**Status:** 🟠

`Maliarov algoritmus (Painter’s algorithm)` vykresľuje objekty `od najvzdialenejších po najbližšie` k pozorovateľovi.

`Výhoda:`

- jednoduchá implementácia.

`Nevýhoda:`

- problémy pri vzájomnom prekrývaní objektov.



---

### 53. Freeman–Lotrelov algoritmus riešenia viditeľnosti

**Status:** 🔴

Tento algoritmus rieši viditeľnosť `hranových reprezentácií (wireframe)`.
Zameriava sa na `detekciu viditeľných a skrytých hrán` pomocou geometrických vzťahov medzi plochami.

Používa sa pri technických a analytických zobrazeniach.

---

### 54. Algoritmus pamäte hĺbky (Z-buffer)

**Status:** 🟢

`Z-buffer` je obrazová metóda viditeľnosti.
Pre každý pixel sa ukladá `hĺbka (Z-hodnota)` najbližšieho objektu.

Pri vykresľovaní sa pixel zobrazí len vtedy, ak má menšiu Z-hodnotu než uložená.
Je rýchly a veľmi používaný v real-time grafike.

---

### 55. Metóda BSP stromov pri riešení viditeľnosti

**Status:** 🟠

`BSP (Binary Space Partitioning)` delí priestor na podpriestory pomocou rovín.
Vzniká `BSP strom`, ktorý umožňuje efektívne triedenie objektov podľa polohy voči kamere.

Používa sa v herných enginoch a interiérových scénach.

---

### 56. Metóda oktantových stromov pri riešení viditeľnosti

**Status:** 🟠

`Oktantový strom (Octree)` rozdeľuje 3D priestor na osem menších kociek.

`Umožňuje:`

- zrýchlenie testov viditeľnosti,
- efektívne ukladanie scén.

Používa sa najmä pri veľkých a riedkych scénach.

---

### 57. Urýchľovacie metódy riešenia viditeľnosti, FV (BC) algoritmus

**Status:** 🔴

Urýchľovacie metódy znižujú počet testovaných objektov.

`FV (Back-face Culling)` odstraňuje plochy, ktoré sú otočené chrbtom ku kamere.
Zvyšuje výkon bez vplyvu na výsledný obraz.

---

### 58. Orezávanie na zorný ihlan pri riešení viditeľnosti

**Status:** 🔴

`Orezávanie (clipping)` odstraňuje časti objektov mimo `zorného ihlana kamery`.

Znižuje výpočtovú náročnosť a zabraňuje zbytočnému vykresľovaniu neviditeľných objektov.

---

### 59. Ohraničujúce objekty, sektorovanie a potenciál viditeľnosti

**Status:** 🔴

`Ohraničujúce objekty` (bounding box, bounding sphere) zjednodušujú testy viditeľnosti.

`Sektorovanie priestoru` delí scénu na oblasti.
`Potenciál viditeľnosti (PVS)` určuje, ktoré sektory môžu byť z daného miesta viditeľné.

---

### 60. S-buffer pri riešení viditeľnosti

**Status:** 🔴

`S-buffer` je rozšírenie Z-bufferu, ktoré umožňuje správne riešiť `prieniky plôch a transparentnosť`.

Ukladá viac hĺbkových intervalov na pixel, čím dosahuje presnejšie výsledky.

---

## [61 - 68] Vyplňovanie oblastí a textúrovanie:

---

### 61. Vyplňovanie oblastí používané v počítačovej grafike

**Status:** 🟠

Vyplňovanie oblastí slúži na `zafarbenie uzavretých plôch` v 2D grafike.
Používa sa pri polygonoch, oblastiach a uzavretých krivkách.

`Základné prístupy:`

- riadkové vyplňovanie,
- semienkové vyplňovanie,
- spektrálne vyplňovanie.

---

### 62. Algoritmus riadkového rozkladu pri vyplňovaní oblastí

**Status:** 🟠

`Riadkový rozklad (scanline fill)` prechádza obraz `po vodorovných riadkoch`.
Na každom riadku sa vypočítajú priesečníky s hranami polygónu a vyplní sa oblasť medzi nimi.

Je rýchly a efektívny, často používaný v rastrových systémoch.

---

### 63. Vyplňovanie spektrom

**Status:** 🟠

`Spektrálne vyplňovanie` používa `plynulý prechod farieb` v rámci oblasti.
Farba sa mení podľa polohy bodu v ploche (napr. lineárne alebo radiálne gradienty).

Používa sa na zvýšenie vizuálnej kvality a plasticity objektov.

---

### 64. Inverzné a plotové vyplňovanie

**Status:** 🟠

`Inverzné vyplňovanie` mení stav pixelov pri každom prechode hranou – využíva paritné pravidlo.

`Plotové vyplňovanie` využíva pomyselnú „plotovú čiaru“, podľa ktorej sa určuje vnútro oblasti.

Používajú sa pri zložitejších tvaroch.

---

### 65. Rekurzívne a nerekurzívne semienkové vyplňovanie

**Status:** 🟠

`Semienkové vyplňovanie (seed fill)` začína z jedného bodu vnútri oblasti a šíri sa do okolia.

- `rekurzívne` – jednoduché, ale pamäťovo náročné,
- `nerekurzívne` – používa zásobník alebo front, bezpečnejšie pre veľké oblasti.

---

### 66. Textúrovanie a jeho vzťah k zobrazovacím reťazcom

**Status:** 🟢

`Textúrovanie` priraďuje 2D obraz (textúru) na povrch 3D objektu.
Prebieha v rámci `zobrazovacieho reťazca` po transformáciách objektu.

Zvyšuje realizmus bez zvyšovania geometrickej zložitosti.

---

### 67. Bilineárne textúrovanie, bump-map a „pečenie“ textúr

**Status:** 🟢

- `Bilineárne textúrovanie` interpoluje farby zo štyroch susedných texelov.
- `Bump mapping` simuluje nerovnosti povrchu zmenou normál.
- `Pečenie textúr (texture baking)` ukladá osvetlenie alebo detaily priamo do textúry.

Používa sa na optimalizáciu výkonu.

---

### 68. LOD technológie v počítačovej grafike

**Status:** 🟢

`LOD (Level of Detail)` mení detail objektu podľa jeho vzdialenosti od kamery.
Blízke objekty majú vysoký detail, vzdialené nízky.

Cieľom je `zvýšiť výkon` bez viditeľnej straty kvality.

---

## [69 - 77] Tieňovanie, osvetľovanie a fotorealistické zobrazovanie:

---

### 69. Konštantné (flat) tieňovanie

**Status:** 🟢

`Flat shading` priraďuje `jednu farbu celej ploche` podľa jej normály.

`Výhody:`

- rýchle výpočty.

`Nevýhody:`

- neplynulé prechody medzi plochami,
- menej realistický vzhľad.

---

### 70. Tieňovanie interpoláciou farby (Gouraud)

**Status:** 🟢

`Gouraud shading` počíta osvetlenie vo vrcholoch a `interpoluje farbu` po ploche.

`Výhody:`

- plynulejší vzhľad než flat shading.

`Nevýhoda:`

- slabšie zvýraznenie špeculárnych odleskov.

---

### 71. Tieňovanie interpoláciou normály (Phong)

**Status:** 🟢

`Phong shading` interpoluje normály medzi vrcholmi a osvetlenie počíta `pre každý pixel`.

`Výhody:`

- realistické osvetlenie,
- správne špeculárne odlesky.

`Nevýhoda:`

- vyššia výpočtová náročnosť než `Gouraud`.

---

### 72. Osvetľovanie a osvetľovacie modely, svetelné zdroje

**Status:** 🟢

Osvetľovanie simuluje `interakciu svetla s objektmi`.

`Typy svetelných zdrojov:`

- bodové,
- smerové,
- reflektorové,
- plošné.

Osvetľovací model určuje, ako sa počíta výsledná farba povrchu.

---

### 73. Lambertov osvetľovací model

**Status:** 🟢

`Lambertov model` popisuje `difúzne osvetlenie`.
Intenzita svetla závisí od uhla medzi normálou povrchu a smerom svetla.

Je jednoduchý, rýchly, ale `nepočíta so zrkadlením`.

---

### 74. Phongov osvetľovací model

**Status:** 🟢

`Phongov model` kombinuje tri zložky:

- ambientnú,
- difúznu,
- špeculárnu.

Umožňuje realistické odlesky a je základom mnohých shading techník.

---

### 75. Osvetľovacie mapy a zrkadlá

**Status:** 🟠

`Osvetľovacie mapy` (light maps, environment maps) ukladajú informácie o osvetlení do textúr.

`Zrkadlá` využívajú odrazové mapovanie alebo `ray tracing` na simuláciu odrazov.

---

### 76. Realistické zobrazovanie a globálne osvetlenie

**Status:** 🟠

Realistické zobrazovanie simuluje `šírenie svetla v celej scéne`.

`Metódy:`

- od pozorovateľa (`ray tracing`),
- od svetelného zdroja (radiosity).

Zohľadňujú odrazy, tiene a rozptyl svetla.

---

### 77. Fotorealistické metódy a ray tracing

**Status:** 🟢

`Ray tracing` sleduje lúče svetla od kamery do scény.

`Umožňuje:`

- presné odrazy,
- lomy,
- mäkké tiene.

Nevýhodou je vysoká výpočtová náročnosť.

---

## [78 - 80] Fraktály, časticové systémy, virtuálna realita a XR:

---

### 78. Fraktály a časticové systémy

**Status:** 🟠

`Fraktály` sú sebepodobné štruktúry používané na modelovanie prírody.

`Časticové systémy` simulujú javy ako dym, oheň, dážď pomocou veľkého množstva jednoduchých častíc.

---

### 79. Virtuálna realita – pojmy, kategorizácia, podsystémy

**Status:** 🟠

`Virtuálna realita (VR)` vytvára imerzívne digitálne prostredie.

`Základné podsystémy:`

- zobrazovanie,
- sledovanie pohybu,
- interakcia,
- výpočtový systém.

Cieľom je pocit prítomnosti v prostredí.

---

### 80. XR, kolaboratívna VR, interakcia a UI

**Status:** 🟠

`XR (Extended Reality)` zahŕňa:

- VR,
- AR,
- MR.

`Kolaboratívna VR` umožňuje viacerým používateľom interagovať v jednom virtuálnom priestore.
Používajú sa špeciálne `rozhrania a interakčné zariadenia` (gestá, ovládače, haptika).

---
