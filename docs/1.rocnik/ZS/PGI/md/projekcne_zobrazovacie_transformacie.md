# Projekčné a zobrazovacie transformácie (otázky 36 - 41)

_[Zdroj: PG_2021_Otazky_z_predmetu.pdf, skuska2023.pdf, prednasky.pdf]_

---

## 36. 2D premietacie transformácie používané v počítačovej grafike, logická a fyzická pracovná oblasť, otáčanie kamery na báze Eulerových uhlov

### Projekcie – všeobecná charakteristika (podľa podkladov)
- Projekcie sú **špeciálne transformácie**.
- Uvažujú sa v reťazci medzi **USS** (globálna/používateľská sústava) a **SSC** (súradnicová sústava kamery).
- Zvyčajne ide o transformácie medzi **rôznymi dimenziami** (najčastejšie **3D → 2D**).
- Súvisia s **2. vrstvou vizualizačného procesu** (transformácie).

### Pracovná oblasť – logická vs. fyzická (SSZ)
Pracovná oblasť v SSZ sa delí:
- **Logická oblasť SSZ**  
  - „virtuálna“ oblasť, zviazaná s USS (čo si definujem ako pracovný priestor).
- **Fyzická oblasť SSZ**  
  - oblasť daná **fyzickým zariadením** (čo reálne zobrazím / aké mám rozlíšenie, rozmery, výstup).

### Zorné pole (FOV) – podľa podkladov
- Premietanie sa viaže na zorné pole kamery (FOV).
- Premieta sa na „stred projekčnej šošovky“.
- Podklady uvádzajú 3 základné typy FOV:
  - **HFOV** – vodorovné (horizontal)
  - **VFOV** – zvislé (vertical)
  - **DFOV** – celkové (diagonálne – uhlopriečka)
- Typicky sa uvádza rozsah približne **60° – 70°**.
- FOV sa aplikuje v **pohľadovej transformácii** a v **súradnicovej sústave kamery**.

### Otáčanie kamery na báze Eulerových uhlov (podľa podkladov)
Otáčanie kamery je zložené z troch zložiek:
- otáčanie v **pôdoryse SSC**,
- **sklon/zdvih** pohľadu kamery v SSC,
- otáčanie okolo **vektora pohľadu** kamery v SSC.

### Typy premietacej transformácie (podľa podkladov)
Podklady uvádzajú tri základné typy premietania:
- **kolmá (ortografická)**,
- **axonometrická (axonometria)**,
- **perspektívna (perspektíva)** – najčastejšie využívaná.

Poznámka k 2D zobrazovacím transformáciám (podľa doplnkového zhrnutia):
- v reťazci sa uvádzajú aj 2D typy „zobrazovacích transformácií“:
  - **normalizačná** (z USS do NSS),
  - **orezávacia** (z NSS do SSZ).

---

## 37. Orezávacie algoritmy, Cohen–Sutherlandov algoritmus

### Cohen–Sutherlandov algoritmus (podľa podkladov)
- Ide o **orezávaciu transformáciu** (clipping).
- Logický priestor sa rozdelí na **9 oblastí** (3×3 okolo okna).
- Každá oblasť je popísaná **4-bit kódom**.
- Zobrazovacie okno (fyzická oblasť) je v strede a má kód **0000**.

### Princíp
Ak časť úsečky leží mimo okna:
- vypočíta sa **priesečník** úsečky s hranicou okna,
- vykreslí sa len viditeľná časť:
  - od viditeľného bodu po priesečník, alebo
  - od jedného priesečníka po druhý.
Ak je celá úsečka mimo:
- úsečka sa **nevykreslí**.

### Rozhodovanie podľa kódov koncových bodov (podľa podkladov)
1. **Oba kódy sú nulové**  
   - oba body sú vnútri okna → úsečku je možné vykresliť **bez orezania**.
2. **Jeden kód je nenulový**  
   - časť úsečky je mimo → je nutné **orezanie**.
3. **Oba kódy sú nenulové**  
   - sú dva prípady:
   - (a) úsečka je celá mimo → nevykreslí sa (typicky ak majú kódy spoločné „jednotkové bity“, napr. **1000 a 1010**),
   - (b) časť úsečky je v okne → je nutné orezanie (napr. **1000 a 0100**, kde nemajú „dva príslušné bity rovnaké“).

---

## 38. Kolmá (ortografická) projekcia, Mongeova projekcia

### Kolmá (ortografická) projekcia (podľa podkladov)
- Kolmá projekcia **nevytvára dojem hĺbky**.
- Na jednoznačné zobrazenie 3D objektu je potrebné použiť viac pohľadov, typicky:
  - **pôdorys**,
  - **bokorys**,
  - **nárys**  
  (podklady uvádzajú „aspoň 3“).
- Podklady uvádzajú poznámku: „100% viditeľnosť“ je až pri **6 pohľadoch**.

### Mongeova projekcia (v kontexte podkladov)
- Mongeova projekcia je v praxi viazaná na sústavu kolmých priemetov (nárys/pôdorys/bokorys),
  teda zodpovedá spôsobu, kde sa objekt popíše viacerými **ortografickými** pohľadmi.

---

## 39. Axonometria

### Axonometrická projekcia (podľa podkladov)
- Podklady ju popisujú v štýle „stredová projekcia“ s charakteristikou:
  - os, ktorá ide „nahor“, má projekciu takú, ako ju vidíme,
  - zvyšné dve osi sú pod uhlom,
  - vzdialenosť kamery nie je taká podstatná.
- Spomína sa „axonometrický kríž (trojuholník)“.

### Typy axonometrije (podľa podkladov)
- **Izometria**: \(J_X = J_Y = J_Z\) a \(\alpha = \beta\)
- **Dimetria**: \(J_X = J_Y\) a \(\alpha = \beta\)
- **Trimetria**: \(J_X \ne J_Y \ne J_Z\) a \(\alpha \ne \beta\)
- **Technická axonometria**: \(J_X = J_Y\), \(J_Z = \tfrac{1}{2}J_X\), \(\alpha = 45°\), \(\beta = 0°\)

---

## 40. Perspektíva

### Perspektívna projekcia (podľa podkladov)
- Je dôležitá **vzdialenosť kamery** od projekčnej roviny (podklady spomínajú „ihlan pohľadu“).
- Podklady uvádzajú, že „rovina xz je zobrazovacia“.
- Postup (konštrukčne):
  - mám bod **B** v scéne,
  - spojím ho so stredom projekcie **S**,
  - vypočítam priesečník priamky **SB** so zobrazovacou rovinou → dostanem obraz bodu **B'**.

Poznámka z doplnkového zhrnutia:
- spomína sa aj „da Vinciho okno“ (interpretácia perspektívy ako pohľadu cez sklenenú plochu, na ktorú sa „premieta“ scéna).

---

## 41. Nelineárne premietacie transformácie, distorzia obrazu, rybie oko

### Distorzia obrazu (podľa podkladov)
- Distorzia (skreslenie) je **optická chyba** spôsobená rôznou mierou zväčšenia naprieč plochou obrazu.
- Narušuje predmetovú a obrazovú podobnosť:
  - zobrazenie jednotlivých bodov môže byť „správne“,
  - ale **konfigurácia bodov** (geometrické vzťahy) je skreslená.

### Rybie oko (fisheye) – nelineárna transformácia (podľa podkladov)
Podklady uvádzajú premenné:
- **y** – vzdialenosť snímku svetelného lúča (prechádzajúceho bodom O) od hlavného bodu H,
- **f** – ohnisková vzdialenosť objektívu,
- **β** – uhol medzi lúčom a optickou osou objektívu (pohľadový uhol kamery).

Podklady uvádzajú 3 typy rybieho oka:
- **Ortografické**: \(y = f \cdot \sin(\beta)\) – „najčastejšie“
- **Rovnoploché**: \(y = 2f \cdot \sin(\beta/2)\) – „najmenej používané“
- **Ekvidistančné**: \(y = f \cdot \beta\)

---

## Rýchle skúškové zhrnutie (čo vedieť povedať)
- Projekcie sú špeciálne transformácie medzi USS a SSC; často 3D→2D; súvisia s 2. vrstvou vizualizačného procesu.
- Pracovná oblasť SSZ: logická (virtuálna, zviazaná s USS) vs fyzická (daná zariadením).
- FOV: HFOV, VFOV, DFOV; typicky 60°–70°; používa sa v PT/SSC.
- Typy premietania: kolmá (ortografická), axonometrická, perspektívna (najčastejšie).
- Kolmá projekcia: bez dojmu hĺbky; na popis 3D treba viac pohľadov (pôdorys/bokorys/nárys; „100%“ až pri 6).
- Cohen–Sutherland: 9 oblastí, 4-bit kódy; okno = 0000; podľa kódov rozhodnem: bez orezania / orezať / zahodiť (napr. 1000 & 1010 mimo, 1000 & 0100 → orezanie).
- Axonometria: izometria/dimetria/trimetria/technická axonometria podľa mierok a uhlov.
- Perspektíva: spoj S–B a priesečník so zobrazovacou rovinou dá B′; dôležitá vzdialenosť (ihlan pohľadu).
- Nelineárne projekcie: distorzia = nerovnomerné zväčšenie naprieč obrazom; rybie oko má typy ortografické/rovnoploché/ekvidistančné s rovnicami pre y.
