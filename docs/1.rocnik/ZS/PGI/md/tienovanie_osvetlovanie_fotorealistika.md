# Tieňovanie, osvetľovanie a fotorealistické zobrazovanie (otázky 69 - 77)

_[Zdroj: PG_2021_Otazky_z_predmetu.pdf, skuska2023.pdf, prednasky.pdf]_

---
## 69. Konštantné (flat) tieňovanie v rámci počítačovej grafiky

### Charakteristika
Konštantné (flat) tieňovanie vychádza z predpokladu, že normála potrebná na výpočet osvetlenia je rovnaká na celej ploche (stene/polygóne). To znamená:
- pre každú stenu sa vypočíta jedna normála,
- podľa nej sa určí jedna intenzita (t. j. jedna výsledná „tieňovaná“ farba) pre celú stenu.

Podmienka z pohľadu korektnosti:
- všetky steny musia byť rovnako orientované (konzistentná orientácia hrán/vrcholov), aby normály smerovali konzistentne.

### Výpočet normály steny
Normála steny sa určuje zo smerových vektorov hrán (na poradí záleží):
- zoberú sa dva smerové vektory hrán steny,
- normála sa získa ako vektorový súčin týchto smerových vektorov (a následne sa berie ako normálový smer plochy).

### Od čoho závisí intenzita tieňa
Intenzita tieňa (osvetlenia steny) je závislá od:
- uhla medzi vektorom dopadu lúča (smerom svetla) a normálou steny.

### Podporné technológie (v kontexte kvality obrazu)
- poltónovanie (halftoning),
- rozptyľovanie (dithering).

Príklad (kedy sa používa):
- nízkopolygónový vzhľad alebo situácie, kde nevadí, že sú viditeľné „hranaté“ prechody medzi stenami.

---

## 70. Tieňovanie interpoláciou farby (Gourard) v rámci počítačovej grafiky

### Charakteristika
Gouraudovo tieňovanie je tieňovanie založené na interpolácii farby (intenzity). Oproti flat tieňovaniu:
- nepočíta sa iba s normálami stien,
- ale zavádzajú sa aj normály hrán,
- z intenzít na hranách sa potom robí lineárna interpolácia do vnútra steny.

### Postup (kroky podľa materiálov)
1. Rovnako ako pri konštantnom tieňovaní sa vypočítajú normály plôch.
2. Vypočítajú sa normály hrán medzi plošnými uzlami ako vektorový súčet normál stien, ktoré tvoria danú hranu.
3. Predpokladá sa, že takto získaná normála je rovnaká pre celú hranu.
4. Pre dané miesta na hranách sa určí intenzita svetla podľa uhla alfa (medzi normálou a smerom svetla).
5. Následne sa urobí lineárna interpolácia intenzity medzi hranami do vnútra steny.

Poznámka:
- určenie intenzity svetla a interpolácia intenzity je podobná princípu vyplňovania spektrom (prechod farieb).

Príklad (čo treba vedieť povedať):
- ak poznám intenzity na hranách alebo v uzloch steny, viem ich lineárne „rozliať“ do celej plochy, takže prechod tieňa je plynulejší než pri flat.

---

## 71. Tieňovanie interpoláciou normály (Phong) v rámci počítačovej grafiky

### Charakteristika
Phongovo tieňovanie pracuje s interpoláciou normály (nie farby). Používa empirický osvetľovací model (Phong, 1977) a v materiáloch sa uvádzajú dve základné zložky:
- difúzna zložka (v zmysle normály N),
- reflexná/spekulárna zložka (v zmysle odrazového vektora R).

Výsledná intenzita (Iv) vzniká kombináciou informácie z N a R.

Dôsledok:
- normálu treba určiť v každom bode povrchu (veľa výpočtov, aj keď sú jednoduché),
- metóda je výpočtovo náročná pre reálny čas, ale vizuálne pôsobí fotorealistickejšie.

### Postup (kroky podľa materiálov)
1. Ako pri konštantnom tieňovaní: výpočet normál plôch.
2. Ako pri Gouraudovi: výpočet normál hrán.
3. Výpočet vrcholových normál (vektorov): napr. NV1 = NH13 + NH12 + NH23 + ... (vektorový súčet normál hrán v okolí vrcholu).
4. V ďalšom kroku sa určuje uhol alfa medzi smerom svetla a normálou.
5. Určí sa intenzita svetla.
6. Normála v ľubovoľnom bode povrchu sa získa interpoláciou medzi normálami vrcholov (nie je to jedna normála pre hranu).

### Viac svetelných zdrojov
Pri viacerých svetelných zdrojoch sa často pracuje so:
- sumou príspevkov všetkých zdrojov a prípadným percentuálnym podielom príspevku.

Príklad (čo treba vedieť povedať):
- Gouraud interpoluje intenzitu (farbu), Phong interpoluje normálu a až z nej určuje intenzitu, preto je výpočtovo náročnejší.

---

## 72. Osvetľovanie a osvetľovacie modely, svetelné zdroje

### Osvetľovanie (čo sa tým myslí)
Osvetľovanie je proces vplyvu svetelného zdroja/zdrojov, materiálu a iných objektov na svoje okolie resp. na iné objekty – vrhanie tieňov, odrazy, lom svetla pri prechode materiálom.

### Typy osvetľovania
- statické: svetlá sa nehýbu, výpočet sa môže urobiť „na začiatku“,
- dynamické: svetlá/objekty sa pohybujú, každý pohyb sa musí prejaviť v scéne.

### Osvetľovací model
Osvetľovací model je model vlastností povrchu (farba, lesklosť, matnosť, drsnosť a pod.). Základom je odrazová funkcia (reflection function):
- vyjadruje intenzitu rozptýleného svetla v závislosti od smeru dopadajúceho lúča, smeru pozorovania a vlnovej dĺžky,
- čím lepšie popisuje reálne správanie svetla, tým presvedčivejší je výsledný obraz.

### Svetelné zdroje (kategorizácia)
a) podľa farby:
- monochromatické,
- achromatické (napr. biele)

b) podľa spôsobu vyžarovania:
- bodové,
- reflektorové (spot),
- plošné

c) podľa kinematiky:
- statické,
- dynamické

### Osvetľovacie mapy (lightmaps)
Osvetľovacie mapy sú nadstavba – celkový počet vplyvov svetelných zdrojov na scénu.

---

## 73. Lambertov osvetľovací model

Lambertov osvetľovací model je jednoduchý model.

### Pointa
- ide o difúzny (matný) prístup,
- veľkosť difúznej zložky je úmerná kosínusu uhla dopadu (uhol medzi smerom svetla a normálou),
- nezáleží od smeru pohľadu (v zmysle zrkadlového efektu).

Príklad:
- matná stena: ak svetlo dopadá kolmo na povrch, je jas väčší; pri šikmom dopade je menší.

---

## 74. Phongov osvetľovací model

Phongov osvetľovací model je zložitejší model než Lambert.

### Zložky svetla podľa Phonga
- ambientná zložka (ambient light)  
  predstavuje svetlo prichádzajúce zo všetkých smerov, rozptýlené (často achromatické).
- difúzna zložka (diffuse)  
  nezáleží na smere pohľadu; po viacnásobnom odraze a lome je smer lúča náhodný; veľkosť zložky je úmerná kosínusu uhla dopadu; nesie informácie o farbe povrchu.
- zrkadlová zložka (specular)  
  záleží na smere pohľadu; veľkosť závisí od uhla dopadu a optických vlastností povrchu; viacnásobný odraz a lom spôsobujú útlm; pri odraze sa často riadi štatistickým rozdelením (Gaussova krivka).

Poznámky:
- celkový odraz svetla je tvorený difúznou a zrkadlovou zložkou,
- pre reálny čas sa často obmedzujú funkcie odrazu (zjednodušovanie).

Príklad:
- lesklý lakovaný povrch: okrem difúzneho zafarbenia vidno aj zrkadlový odlesk, ktorý závisí od uhla pohľadu.

---

## 75. Osvetľovacie mapy a zrkadlá

### Osvetľovacie mapy (lightmaps)
Osvetľovacia mapa je celkový výpočet vplyvov svetelných zdrojov na scénu (kde bude farba živšia/bledšia).

V materiáloch je uvedený proces:
1. Osvetľovacia mapa
2. Dodanie textúr
3. Dodanie svetelných zdrojov

### Zrkadlá
Uvádzajú sa dva prístupy:

- environmentálne zrkadlo: využitie pohľadu kamery umiestnenej v zrkadle ako textúry objektu zrkadla,
- geometrické zrkadlo: zrkadlové modelovanie scény viditeľné cez polopriehľadnú plochu.

Príklad:
- environmentálne zrkadlo = aproximácia odrazu textúrou; geometrické zrkadlo = presnejší odraz, ale drahší výpočet.

---

## 76. Realistické zobrazovanie a globálne osvetľovacie techniky v rámci počítačovej grafiky, metódy vychádzajúce od pozorovateľa a od svetelného zdroja

### Fotorealistika a globálne osvetľovanie
Fotorealistika: čo najvernejšie zobrazenie priestorových scén a objektov vrátane osvetlenia a riešenia viditeľnosti.

Globálne osvetľovacie techniky slúžia na riešenie zobrazovacej rovnice (vrátane riešenia viditeľnosti). Ich riešením je:
- výpočet osvetlenia všetkých plôch v scéne – pohľadovo nezávislé,
- výpočet osvetlenia pre určitý smer – pohľadovo závislé.

### Rozdelenie globálnych techník (podľa materiálov)
- Metódy vychádzajúce od pozorovateľa:
  - sledovanie lúča,
  - sledovanie cesty.
- Metódy vychádzajúce od svetelného zdroja:
  - sledovanie fotónov,
  - Monte Carlo sledovanie svetla.
- Obojsmerné metódy:
  - obojsmerné sledovanie cesty,
  - fotónové mapy.
- Vyžarovacia metóda (radiosity):
  - opticky najlepšia,
  - ťažká,
  - nevie si poradiť so zrkadlami.

### Metódy vychádzajúce od pozorovateľa (gathering methods)
- pohľadovo závislé metódy,
- zhromažďujú svetelnú informáciu (energiu), ktorú lúč akumuluje po trajektórii,
- spätné sledovanie trajektórie svetla.

### Metódy vychádzajúce od svetelného zdroja (shooting methods)
- energie „vystreľujúce“ metódy,
- riešia problémy ako kaustika a skryté svetelné zdroje,
- za cenu šumu (náhodné sledovanie dráh lúčov zo svetelného zdroja).

Príklady (podľa materiálov):
- photon tracing,
- light tracing.

---

## 77. Algoritmy fotorealistických metód a metóda raytracing

### Skupiny algoritmov fotorealistických metód (podľa materiálov)
a) algoritmy zobrazujúce povrchy (surface based)
- vytvárajú pomocnú geometrickú reprezentáciu,
- hľadajú hrany a body povrchu a interpretujú povrch 2D záplatami,
- snažia sa z objemových dát aproximovať povrch pomocou geometrických primitív,
- vnútro objektu je zahodené,
- príklady: contour tracking (sledovanie obrysov), marching cubes, marching tetrahedra, dividing cubes, opaque cubes.

b) objemové algoritmy
- využívajú celú priestorovú informáciu na vykreslenie,
- nezávislé od zložitosti scény,
- využívajú celú mriežku údajov, náročné na procesor a pamäť,
- delia sa na:
  - binárne (voxel úplne alebo vôbec),
  - pravdepodobnostné (voxelu je priradený percentuálny podiel objektu; príspevky vzoriek pozdĺž lúča sa nahrádzajú do jedného pixela).

c) algoritmy pracujúce v obrazovom priestore
- pre každý pixel výsledného obrazu sa hľadajú voxely v objektovom priestore, ktoré prispievajú do farby,
- často je nutná interpolácia pre hodnoty voxelov mimo vrcholov mriežky,
- príklady: trasovanie lúčov (raytracing, raycasting), Sábelova metóda.

d) algoritmy pracujúce v objektovom priestore
- pre každý voxel objektového priestoru sa hľadajú pixely výsledného obrazu, ktoré daný voxel ovplyvnia,
- príklady: V-buffer, splatting.

e) algoritmy pracujúce na hybridnom princípe
- kombinujú výhody predchádzajúcich prístupov,
- shear-warp: posun rezov tak, aby mapovanie do 2D bolo rýchle; nevýhody: 2 kroky prevzorkovania (rozmazanie), iba 2D rekonštrukčný filter, bilineárna interpolácia v rezoch a najbližší sused medzi rezmi, aliasing pri podvzorkovaní.

### Metóda raytracing (sledovanie lúča) – stručný popis
- z každého obrazového bodu je vyslaný lúč smerom do scény,
- sleduje sa jeho správanie v scéne,
- lúč končí, keď dosiahne zdroj svetla alebo dopadne mimo scénu (príp. sa obmedzí hĺbka rekurzie),
- po nájdení svetelného zdroja sa postupuje spätne,
- zápis je reprezentovaný stromom, koreňom je zobrazovaný bod,
- výpočet intenzity je suma intenzít jednotlivých zložiek.

Príklad:
- pri zrkadlovom odraze môže lúč pokračovať ďalej; preto sa v praxi obmedzuje hĺbka rekurzie.

---

## Rýchle skúškové zhrnutie (čo vedieť povedať)
- Flat: 1 normála na stenu, 1 intenzita na stenu; normála zo smerových vektorov hrán; intenzita podľa uhla medzi svetlom a normálou; konzistentná orientácia stien.
- Gouraud: normály plôch + normály hrán (súčet normál stien); intenzita sa určí na hranách/uzloch a lineárne interpoluje do vnútra steny (analógia so spektrom).
- Phong tieňovanie: interpoluje sa normála v každom bode povrchu; difúzna + spekulárna zložka; veľa výpočtov, fotorealistickejšie; pri viacerých svetlách sčítavanie príspevkov.
- Osvetľovanie: vplyv svetiel, materiálu a objektov (tiene, odrazy, lom); statické vs dynamické.
- Osvetľovací model: odrazová funkcia; lepšie priblíženie reality = lepší vizuálny vnem.
- Svetlá: podľa farby (mono/achro), vyžarovania (bodové/spot/plošné), kinematiky (statické/dynamické).
- Lambert: jednoduchý difúzny model; intenzita úmerná cos uhla dopadu.
- Phong model: ambient + difúzna + zrkadlová; zrkadlová závisí od smeru pohľadu a vlastností povrchu; často štatistické rozdelenie (Gauss).
- Lightmapy: celkový vplyv svetiel na scénu; proces (1) osvetľovacia mapa, (2) textúry, (3) svetlá.
- Zrkadlá: environmentálne (kamera → textúra) vs geometrické (zrkadlenie scény).
- Globálne osvetľovanie: riešenie zobrazovacej rovnice a viditeľnosti; od pozorovateľa (gathering) vs od zdroja (shooting), obojsmerné, radiosity (ťažká, nevie zrkadlá).
- Algoritmy fotorealistických metód: surface-based (marching cubes…), objemové (binárne/pravdepodobnostné), obrazový priestor (raytracing/raycasting), objektový priestor (V-buffer, splatting), hybrid (shear-warp).
- Raytracing: lúč z pixelu do scény, rekurzia/obmedzenie hĺbky; spätné skladanie príspevkov; strom s koreňom v pixeli.
