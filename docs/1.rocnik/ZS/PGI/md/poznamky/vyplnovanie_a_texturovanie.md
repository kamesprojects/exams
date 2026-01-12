# Vyplňovanie oblastí a textúrovanie (otázky 61 - 68)

_[Zdroj: PG_2021_Otazky_z_predmetu.pdf, skuska2023.pdf, prednasky.pdf]_

---

## 61. Vyplňovanie oblastí používané v počítačovej grafike (charakteristika)

### Súvis s vizualizačným procesom
Vyplňovanie oblastí sa typicky viaže na:
- 4. vrstvu vizualizačného procesu (vyplňovanie/textúry v rámci generovania výsledného obrazu),
- 6. a 7. vrstvu (kompozícia, vykresľovanie – výsledné „dostavenie“ farieb/pixelov do obrazu).

### Typy vyplňovania (čo sa tým myslí)
- **Vyplňovanie oblasti 1 farbou**  
  Najjednoduchší prípad: všetky body oblasti dostanú tú istú farbu výplne.
- **Vyšrafovanie oblasti**  
  Vyplnenie oblasti čierno-bielym vzorom (šrafy, raster, opakujúci sa vzor).
- **Vyplnenie farebným vzorom (textúrovanie)**  
  Vyplnenie oblasti farebným obrazovým vzorom (textúrou) tak, aby vznikol dojem materiálu (drevo, kameň, kov a pod.).

### Rozdelenie algoritmov vyplňovania podľa toho, ako je zadaná hranica
Algoritmy sa delia podľa spôsobu zadania hranice vypĺňanej oblasti:
- **Hranica definovaná geometricky (výpočtovo)**  
  Hranica je daná vrcholmi/hranolmi/polygónom, priesečníky sa rátajú matematicky.
- **Hranica nakreslená na zobrazovači**  
  Hranica existuje ako pixely na obrazovke (pracuje sa priamo s farbou hranice/výplne).

### Metódy vyplňovania uvádzané v materiáloch
- **Metóda riadkového rozkladu**
- **Inverzné vyplňovanie** – riadkové a plotové
- **Vyplňovanie spektrom**
- **Semienkové vyplňovanie** – rekurzívne a nerekurzívne

---

## 62. Metóda riadkového rozkladu pri vyplňovaní oblastí (scanline fill)

### Základná charakteristika
- Použiteľné pri hranici **definovanej geometricky**.
- Oblasť sa vypĺňa po „rozkladových riadkoch“ rovnobežných s osou X (t. j. po riadkoch s konštantnou hodnotou Y).

### Postup (kroky)
1. **Postupuje sa od najvyššieho vrcholu oblasti k najnižšiemu**, a v rámci riadka spravidla zľava doprava.
2. Pre každý rozkladový riadok (konštantné `Y`, zvyčajne s krokom `-1`):
   - nájdu sa priesečníky riadka s hranami vypĺňanej oblasti,
   - priesečníky sa uložia do zoznamu.
3. Priesečníky sa **usporiadajú zľava doprava**.
4. Vyfarbia sa úseky medzi:
   - 1. a 2. priesečníkom,
   - 3. a 4. priesečníkom,
   - atď.

### Dôležitá podmienka
- Počet priesečníkov v každom riadku musí byť **párny**, aby sa dali korektne spárovať úseky „vnútri“ oblasti.

---

## 63. Vyplňovanie spektrom (prechod farieb)

Vyplňovanie spektrom je vyplňovanie oblasti, kde farba **plynule prechádza** z prvej farby do druhej (a nejde o jednu konštantnú farbu).

### Spôsoby realizácie
Uvádzajú sa dva spôsoby:

#### 3.1 Spôsob 1: cez metódu riadkového rozkladu
1. Mnohouholník sa najprv **otočí o uhol β** tak, aby smer vykresľovania úsečiek bol rovnobežný s osou X.
2. Následne sa použije **riadkový rozklad** a nájdu sa priesečníky.
3. Úsečky medzi priesečníkmi sa pri kreslení **spätne otočia o β** (vrátia sa do pôvodnej polohy).
4. Rozdiel oproti klasickému riadkovému vyplneniu: úseky sa nevypĺňajú jednou farbou, ale farba sa mení postupne.

#### 3.2 Spôsob 2: nastavenie orezávacej oblasti (napr. MS Windows)
1. Nastaví sa **orezávacia oblasť** na oblasť mnohouholníka.
2. Vypočítajú sa súradnice:
   - `Xmin, Xmax, Ymin, Ymax`.
3. Podľa veľkosti uhla β sa vyplní príslušný rovnobežník; orezávacia oblasť zabezpečí, že výsledok zostane len v oblasti mnohouholníka.

Poznámka: tento spôsob je viazaný na konkrétne grafické rozhrania (v materiáloch sa spomína Windows).

### Typy zmeny farby / prechodu
- **Lineárna** zmena farby (jednoduchšia)
- **Radiálna** zmena farby

### Plynulý prechod farieb v RGB priestore (výpočet prírastkov)
Pre dve farby `C1=(R1,G1,B1)` a `C2=(R2,G2,B2)`:
1. Zistia sa rozdiely zložiek:  
   - `ΔR = R2 - R1`, `ΔG = G2 - G1`, `ΔB = B2 - B1`.
2. Určí sa počet úsečiek (krokov) `n` v rovnobežníku/prechode.
3. Prírastky na krok:  
   - `pR = ΔR / n`, `pG = ΔG / n`, `pB = ΔB / n`.
4. Farba sa mení po krokoch:  
   - `Ri = R1 + i*pR`, `Gi = G1 + i*pG`, `Bi = B1 + i*pB`.

Materiály uvádzajú, že plynulý prechod je **ekvivalentom alfa miešania** (v zmysle plynulého prechodu medzi dvoma farbami).

---

## 64. Inverzné a plotové vyplňovanie

### Základná charakteristika
- Vyžaduje, aby zobrazovač umožňoval **dynamickú zmenu obsahu** (typicky monitor).
- Nie je implementovateľné na zariadeniach, kde „nevieš prepisovať obsah“ (v materiáloch sa uvádza príklad tlačiarne).
- Hranica je **na zobrazovači** (pracuje sa priamo s pixelmi hranice).

### XOR princíp
Používa sa operácia XOR (výhradne alebo), t. j.:
- `0 XOR 0 = 0`
- `1 XOR 1 = 0`
- `0 XOR 1 = 1`
- `1 XOR 0 = 1`

Interpretácia pri vyplňovaní:
- ak prejdeš cez tú istú oblasť druhýkrát, XOR ju „odfarbí“ (1 XOR 1 = 0).

### Dva typy inverzného vyplňovania
1. **Vodorovné (riadkové) vyplňovanie**  
   - rýchlejšie (typicky lepší prístup do pamäte).
2. **Zvislé (plotové) vyplňovanie**  
   - pomalšie (offsetové odskoky, horší pamäťový prístup).

### Typický postup
1. Pre každú hranu/hranový pixel:
2. XOR metódou sa „zafarbí“ všetko od hrany po pravý (alebo ľavý) okraj obrazovky.
3. Pri ďalšej hrane sa operácia opakuje.
4. Tam, kde sa prechody prekryjú, dôjde k odfarbovaniu (1 XOR 1 = 0) a výsledkom je vyplnená oblasť.

Poznámka z materiálov:
- metóda „100 % nájde výsledok“, ale nie je „100 %“ pri „naliezovaní“ výplne (t. j. niektoré degenerované prípady môžu byť problematické).

---

## 65. Rekurzívne aj nerekurzívne semienkové vyplňovanie

Semienkové vyplňovanie začína vnútri oblasti zvolením počiatočného bodu (semienka) a rozširuje sa do okolia.

### 5.1 Rekurzívne semienkové vyplňovanie
- Hranica je definovaná **na obrazovke**.
- Pre každý pixel sa zisťuje:
  - či je pixel farby hranice,
  - alebo už je pixel farby výplne.
- Ak nie je ani hranica, ani už vyplnený, pixel sa vyplní a rekurzívne sa pokračuje.

Typicky sa používa 4-susednosť:
- hore, dole, vľavo, vpravo.

Nevýhody:
- potrebuje veľa pamäte (rekurzia = zásobník volaní),
- bez úprav je pre veľké plochy prakticky nepoužiteľný.

### 5.2 Nerekurzívne semienkové vyplňovanie
- Základná myšlienka je rovnaká, ale body návratu sa ukladajú do vlastnej štruktúry:
  - zásobník (stack).
- Najbližší „bod rozvoja“ je 1. voľný bod v zásobníku (podľa stratégie DFS/BFS).

Výhody:
- menšie pamäťové nároky než čistá rekurzia,
- je to prakticky použiteľná forma seed fill.

---

## 66. Textúrovanie a jeho vzťah k zobrazovacím reťazcom

### Definícia (textúrovacia transformácia)
Textúrovanie je proces (textúrovacia transformácia, TT) nanášania obrazových vzoriek (textúr, „tapiet“) na povrch alebo objem objektu tak, aby vznikol vizuálny dojem materiálu (drevo, kameň, kov a pod.).

### Typy textúr podľa topologického rozmeru
- 1D, 2D, 3D.

### Typy textúr podľa spôsobu nanášania
- **Statické** (nemenné textúry),
- **Dynamické**,
- **Procedurálne** (textúra sa počíta funkciou, napr. fraktálnou),
- **Animačné** (zmena textúry v čase, typicky poradím statických textúr, často klasická 2D animácia).

### Textúra v transformačnom reťazci
- Zavádza sa **SST (súradnicová sústava textúry)** naviazaná na súradnicovú sústavu objektu.
- Namiesto priestorových súradníc (x, y, z) sa pracuje so súradnicami textúry (u, v) v tzv. „UV priestore“.
- TT je proces, ktorý mapuje body povrchu objektu na body textúry v SST.

Poznámka z materiálov:
- textúrovacia transformácia je vnímaná ako prvý krok v transformačnom reťazci pre textúry,
- typicky sa viaže najmä na súradnicovú sústavu objektu (SSO), s výnimkami (napr. pozadie SSZ).

---

## 67. Bilineárne textúrovanie, bump-map textúrovací procees a technológia „pečenia“ textúr

### Charakteristika
- Ide o základný spôsob UV textúrovania, kde sa ako vzor najčastejšie používa obrázok (textúra).
- Textúra používa 2D súradnicovú sústavu **SST [u, v]**:
  - `u` zodpovedá x-ovej osi textúry,
  - `v` zodpovedá y-ovej osi textúry.
- Jedna jednotka v u/v zodpovedá dĺžke/šírke obrázka textúry.

### Bilineárne UV textúrovanie na nelineárnu plochu (napr. Bézierova plocha)

- Pri nelineárnych plochách nie je mapovanie vždy lineárne („u a v nie sú lineárne“).
- Súradnica `[u, v]` z textúry sa mapuje na priestorový bod `[x, y]` (resp. `[x, y, z]`) na ploche.
- Dá sa tak aplikovať textúra na ľubovoľnú plochu, ale:
  - časová náročnosť je vyššia,
  - pri viacerých plochách treba riešiť aj nadväzovanie textúr (seamy; bázická plocha).

### Bump map (výšková mapa)

- Bump mapping pracuje s výškovou mapou (height map) a vytvára dojem, že povrch má nerovnosti.
- Vplyv svetla na bod povrchu je ovplyvnený „výškou“ z bump mapy.
- V praxi sa upravuje výsledný vzhľad (napr. jas, prípadne saturácia) bodov textúry tak, aby vznikol dojem hrboľatosti (3D efekt bez reálnej zmeny geometrie).
- Umožňuje simulovať aj pohyb svetelného zdroja.
- Vyžaduje vyšší výpočtový výkon.

### Pečenie textúr

„Pečenie“ textúr je prenos (prepočítanie) detailných informácií zo zložitejšieho (detailnejšieho) 3D modelu na jednoduchší (lowpoly) model tak, aby jednoduchší model pôsobil vizuálne detailne.

V kontexte optimalizácie sa to často zaraďuje medzi LOD prístupy, lebo:
- geometria sa zjednoduší (menej polygónov),
- ale časť vizuálnych detailov sa zachová v mapách/textúrach.

### Čo sa typicky „pečie“
Do textúr sa môže zapísať napríklad:
- farba/albedo,
- osvetlenie a tiene (lightmapy, AO),
- normálové informácie (normal map),
- odrazové informácie a iné materiálové parametre.

### Prečo sa to robí (dôvody)
- lowpoly model má menej dát, teda menší súbor a rýchlejšie spracovanie,
- real-time aplikácie (hry, web, VR) často nezvládnu highpoly modely v reálnom čase,
- vizuálna kvalita sa dá udržať cez mapy, aj keď geometria je jednoduchá.

### Praktický príklad
- Highpoly sochy/architektúra: tisíce až milióny polygonov, veľa jemných detailov.
- Lowpoly verzia: výrazne menej polygonov, ale:
  - normal map a AO map spôsobia, že pri osvetlení objekt vyzerá detailne,
  - lightmap môže niesť statické osvetlenie interiéru.
  
---

## 68. LOD technológie v rámci počítačovej grafiky

Level of Detail (LOD) je technika optimalizácie, ktorá znižuje výpočtovú náročnosť tým, že znižuje zložitosť objektov alebo ich parametrov, najčastejšie podľa:
- vzdialenosti od kamery,
- uhla/smeru pohľadu (vrátane zorného poľa).

### Spôsob aktivácie
- Diskrétne LOD: prepínanie v skokoch (napr. 3 verzie modelu podľa vzdialenosti).
- Kontinuálne LOD: plynulé dynamické prispôsobovanie (napr. priebežná zmena teselácie alebo detailu).

### Základné typy LOD (stručne + príklady)
- Geometrický LOD (tessellation LOD): mení počet trojuholníkov.
  - Príklad: blízky objekt má viac detailov, vzdialený má zjednodušený mesh.
- Substitučný LOD (impostor/billboard): vzdialený 3D objekt sa nahradí 2D obrazom.
  - Príklad: stromy v diaľke ako billboardy.
- Screen-space LOD: detail podľa toho, koľko pixelov objekt zaberá na obrazovke.
  - Príklad: malý objekt ďaleko má nižší detail než objekt, ktorý zaberá veľa pixelov.
- Hierarchický LOD (HLOD/group LOD): vzdialené objekty sa zhlukujú do skupín.
  - Príklad: zhluk stromov sa zobrazí ako jeden jednoduchý objekt.
- Terrain LOD (geomipmapping): terén je rozdelený na dlaždice, každá s vlastným detailom.
  - Príklad: dlaždice blízko kamery sú detailné, ďaleké sú hrubšie.
- Materiálový/textúrovací LOD: mení sa kvalita textúr/materiálu (mipmapping, streaming, baking).
  - Príklad: vo veľkej vzdialenosti postačí farba alebo nízke rozlíšenie textúry.
- Osvetľovací LOD: mení sa zložitosť osvetľovacieho modelu alebo sa používajú lightmapy.
  - Príklad: vzdialené objekty bez dynamických tieňov, s jednoduchým Lambertom.
- Tieňovací LOD (shading LOD): voľba jednoduchšieho/zložitejšieho tieňovania podľa vzdialenosti.
  - Príklad: blízko Phong, ďaleko jednoduchšie tieňovanie.
- Foveated LOD (eye-tracked): najvyšší detail len v oblasti fovey, periféria má nižší detail.
  - Príklad: vo VR sa detail znižuje mimo miesta, kam sa používateľ pozerá.

### Rozšírené a urýchľovacie techniky (stručná pointa)
- Mesh simplification/decimation: redukcia vrcholov a trojuholníkov s minimalizáciou vizuálnej straty.
  - Príklad: edge-collapse, vertex-clustering; často s minimalizáciou chyby (quadric error metrics).
- Occlusion culling v kombinácii s LOD: nevykresľujú sa objekty, ktoré sú úplne zakryté.
- Neural geometric LOD: generovanie/optimalizácia detailu neurónovou sieťou (napr. cez SDF a adaptívne štruktúry).

---

## Rýchle skúškové zhrnutie (čo vedieť povedať)
- Typy vyplňovania: 1 farba, vyšrafovanie, farebný vzor (textúra).
- Rozdelenie podľa hranice: geometricky definovaná vs nakreslená na zobrazovači.
- Scanline: priesečníky na riadku, zoradiť, vyfarbiť medzi nepárnym a párnym; párny počet priesečníkov.
- Spektrum: dva spôsoby (otočenie o β + scanline; alebo orezávacia oblasť); lineárny/radiálny prechod; prírastky RGB; ekvivalent alfa miešania.
- Inverzné vyplňovanie: XOR, riadkové vs plotové, potrebuje dynamický výstup.
- Semienkové vyplňovanie: rekurzívne (pamäťovo náročné) vs nerekurzívne (stack).
- Textúrovanie: SST, UV priestor, typy textúr (1D/2D/3D; statické/dynamické/procedurálne/animačné).
- Bilineárne textúrovanie: mapovanie [u,v] na povrch, pri nelineárnych plochách náročnejšie, riešiť nadväzovanie.
- Bump map: výšková mapa + vplyv svetla, dojem nerovností, vyššie nároky.
- Pečenie textúr (texture baking): prenos detailov z highpoly modelu na lowpoly model pomocou textúr (normal map, AO, lightmap); znižuje počet polygónov pri zachovaní vizuálneho detailu; používa sa najmä v real-time aplikáciách (hry, web, VR).
- LOD (Level of Detail): optimalizačná technika, ktorá mení zložitosť geometrie, textúr, materiálov alebo osvetlenia podľa vzdialenosti/uhla pohľadu; môže byť diskrétna (prepínanie verzií) alebo kontinuálna; zahŕňa geometrický, textúrový, osvetľovací, tieňovací a ďalšie typy LOD.
