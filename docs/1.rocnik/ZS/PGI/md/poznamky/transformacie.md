# Transformácie v počítačovej grafike (otázky 26 - 35)

_[Zdroj: PG_2021_Otazky_z_predmetu.pdf, skuska2023.pdf, prednasky.pdf]_

---

## 26. Transformácie a transformačné zobrazovacie reťazce v rámci počítačovej grafiky

### Kde sa to nachádza vo vizualizačnom procese
- **Transformácie patria do 2. fázy vizualizačného procesu.**

### Čo je transformácia
- **Transformácia** je proces, ktorý mení (transformuje) **vstupný objekt** (resp. jeho parametre) na **objekt výstupný**.

### Ako môžu byť transformácie aplikované
- **Paralelne** – transformácie sa navzájom neovplyvňujú.
- **Sekvenčne** – transformácia je zložená z viacerých dielčich transformácií.
  - aby bola výsledná transformácia **lineárna**, všetky dielčie transformácie musia byť **lineárne**.

### Lineárne vs. nelineárne transformácie (podľa podkladov)
- **Lineárne (afinné)**: posunutie, otočenie, zmena mierky, skosenie, zrkadlenie  
  (pozn.: v materiáloch sú tieto transformácie uvádzané ako afinné; pri lineárnom pohľade „nemenia charakter objektu“)
- **Nelineárne**: distorzia, rybie oko, panoráma, zošikmenie  
  (pozn.: v materiáloch sa uvádza, že „menia charakter objektu“)

### Medzisústavové transformácie v transformačnom reťazci
Podklady uvádzajú medzisústavové transformácie:
- **GT** – globálna (geometrická) transformácia  
- **PT** – pohľadová transformácia  
- **ZT** – zobrazovacia (premietacia) transformácia  
- **OT** – orezávacia transformácia  

Poznámka z materiálov:
- „kameru chápeme ako prevodové zariadenie medzi dimenziami“
- zreťazenie transformácií medzi súradnicovými sústavami sa chápe ako **transformačný reťazec** (2D aj 3D varianta)

---

## 27. Transformácie v rámci zobrazovacích reťazcov, transformačné matice a homogénne súradnice, afinné transformácie

### Kde v reťazci môžem aplikovať transformáciu
- Požadovanú zmenu môžem vykonať v rôznych bodoch reťazca.
- Príklad z podkladov: ak mám kocku a chcem ju **2× zväčšiť**, môžem to spraviť:
  - na úrovni **GT** (geometricky zväčším objekt),
  - na úrovni **PT** (zmením „kameru“ – napr. priblížim),
  - prípadne cez **ZT/OT** (podľa toho, čo presne chcem dosiahnuť).

### Homogénne súradnice (idea z podkladov)
- Zavádzajú sa ako „pomocná“ dimenzia/súradnica, ktorá umožní realizovať výpočty v jednoduchej forme.
- Podklady to vysvetľujú metaforou „paralelného vesmíru“:
  - „odskočím“ do pomocnej súradnicovej sústavy,
  - tam vykonám požadovanú operáciu,
  - a vrátim sa späť.

Dôležité praktické fakty z podkladov:
- Transformačné matice sú potom:
  - pre **2D: 3×3**
  - pre **3D: 4×4**
- Pri voľbe hodnoty na homogenizačnej osi sa volí taká hodnota, ktorá tvorí „neutrálnu hodnotu“ pre danú operáciu (v podkladoch je uvedený príklad: pri násobení matíc je to typicky **1**).

### Afinné transformácie (podľa podkladov)
Podklady medzi afinné transformácie zaraďujú:
- zrkadlenie (najmenej zložité),
- zmena mierky,
- posunutie,
- skosenie,
- otočenie (najviac zložité).

Poznámka:
- Implementácia afinných transformácií sa líši pre:
  - **vektorové objekty**
  - **rastrové objekty**
- Pri niektorých transformáciách je rozdiel výrazný, pri iných takmer žiaden (podľa podkladov).

---

## 28. Transformácia zrkadlenia

### Zrkadlenie (2D) – základné vzťahy (podľa podkladov)
- Zrkadlenie v 2D v podkladoch „spočíva vo výmene znamienok“:
  - vzhľadom na os **x**:  \(x' = x,\; y' = -y\)
  - vzhľadom na os **y**:  \(x' = -x,\; y' = y\)
  - vzhľadom na **stred**: \(x' = -x,\; y' = -y\)

### Poznámky k dimenzii „zrkadliaceho“ objektu (podľa podkladov)
- „Môžem zrkadliť nad objektom, ktorého dimenzia je nižšia ako objektu, nad ktorým robím zrkadlenie.“
- „Koľko znamienok mením, toľko je rozdiel dimenzií týchto objektov.“

### Zrkadlenie rastrového objektu (poznámka z podkladov)
- „RASTER – nemôžem zrkadliť naraz“
- vymieňam buď po **stĺpcoch** alebo **riadkoch**
- používa sa napr. keď chcem „otočiť len objekt, ale pozadie nie“

### Zrkadlenie (3D)
- Podklady uvádzajú aj „Zrkadlenie (3D)“ (bez ďalších detailov v tomto výpise).

---

## 29. Transformácia posunutia

- Podklady uvádzajú posunutie ako **TRANSLÁCIU** (bez rozpisu rovníc v tomto výpise).

---

## 30. Transformácia zmeny mierky, zväčšenie/zmenšenie rastrového objektu

### Zmena mierky ako afinná transformácia
- patrí medzi afinné transformácie (uvedené pri otázke 27).

### Zväčšenie rastrového objektu (podľa podkladov)
Podklady uvádzajú postup (najmä pre prípad, keď desatinná časť koeficientu spadá do určitého intervalu):
1. výpočet nového rozmeru podľa koeficientu zmeny mierky,
2. výpočet priameho a korekčného koeficientu a nového celočíselného rozmeru,
3. výpočet rozdielu nového rozmeru a celočíselného rozmeru, následne výpočet krokov aplikácie korekčného koeficientu  
   - idea: „koľko pixelov ešte musím dopracovať v každom smere“ a „v ktorom kroku aplikovať korekčný krok“,
4. aplikácia na pixely rastrového objektu.

V alternatívnom zhrnutí v podkladoch sa uvádzajú kroky:
1. výpočet predpokladaného nového rozmeru,
2. určenie celočíselnej a desatinnej časti koeficientu,
3. otestovanie, či desatinná časť je > 0,5,
4. určenie pomocného priameho koeficientu,
5. výpočet veľkosti rozmeru rastra,
6. výpočet rozdielu (aby sme vedeli koľko bodov doplniť),
7. výpočet korekčného kroku,
8. konečné priradenie koeficientov v jednotlivých krokoch.

### Zmenšenie rastrového objektu (podľa podkladov)
1. koeficient zmeny mierky sa počíta „opačne“: **M = 1/M**  
   - tým sa určí, aká matica pixelov tvorí „subpixel“ (napr. 2×2, 3×3, 3×2),
2. určí sa farba subpixelu, napr.:
   - spriemerovanie / mediánová funkcia (4/8 susedstvo),
   - najčastejší výskyt,
   - najmenší výskyt,
   - farba ľavého horného bodu.

---

## 31. Transformácia skosenia, skosenie rastrového objektu

- Podklady uvádzajú:
  - **Skosenie (2D)**
  - **Skosenie (3D)**
  - **Skosenie rastrových objektov**
- (V tomto výpise nie sú doplnené konkrétne vzorce/postup, preto sa uvádza len existencia témy podľa podkladov.)

---

## 32. Transformácia otočenia

### Otočenie (všeobecne)
Podklady uvádzajú dva prístupy:
- otáčanie definované **Eulerovými uhlami** a reprezentované všeobecnými transformačnými maticami  
  - vždy treba definovať, okolo ktorej osi sa deje čiastková rotácia  
  - podklady uvádzajú, že „neumožňuje všeobecnú rovnicu pre rotáciu“ (v zmysle jedného univerzálneho tvaru bez rozkladu na osi)
- otáčanie definované **Eulerovým teorémom** a reprezentované **quaterniónmi** (v podkladoch poznámka: 1841; dnes používané)

Podklady osobitne uvádzajú:
- Otočenie (rotácia) 2D
- Otočenie (rotácia) 3D  
  - „nesmiem to spraviť naraz v 1 matici (mením 2 súr.)“  
  - „robí sa to krok po kroku“  
  - „dá sa kombinovať s posunom (neprekrývajú sa koeficienty)“

---

## 33. Otáčanie okolo všeobecnej priamky využitím Eulerových uhlov, gimbal lock, quaternióny

### Rotácia okolo všeobecnej priamky (pri Eulerových uhloch)
Podklady uvádzajú postup (len pre Eulerove uhly; pri quaterniónoch sa to robí naraz):
1. posunieme sústavu/objekty tak, aby os otáčania prechádzala počiatkom súradnicovej sústavy (**Tp**)
2. celé to (vrátane osi) „sklopím do pôdorysu“ (**Toa**)
3. os otáčania stotožním s niektorou osou sústavy (**Tob**)
4. vykonám rotáciu okolo požadovanej osi (**To**)
5.–7. návrat do pôvodnej polohy (inverzie), aby os otáčania bola tam kde na začiatku

### Problémy uvedené v podkladoch
1. inverzná matica nemusí existovať,
2. pri určitých uhloch (blízko 0° a 90°) môže vzniknúť nedefinovaný výsledok (podklady to viažu na tangens a nespojitý obor hodnôt).

### Gimbal lock (strata stupňa voľnosti)
- Podklady: „Je možné vytvoriť takú postupnosť rotácií, že vo výslednej rotácii sa stratí jeden stupeň voľnosti.“
- Táto situácia sa nazýva **gimbal lock** (strata stupňa voľnosti).

**Stupeň voľnosti (DOF)** – podľa podkladov:
- počet transformácií (najčastejšie translačných a rotačných) vzhľadom na počet nezávislých súradníc (dimenzií) z hľadiska pohyblivosti objektu v danej súradnicovej sústave,
- v kartezianskej sústave: translácia DOF = 3, rotácia DOF = 3 → spolu typicky 6 DOF.

### Quaternióny (poznámka z podkladov)
- Podklady uvádzajú quaternión ako „komplexné číslo tvorené 4 zložkami“:
  - jedna zložka popisuje veľkosť zmeny mierky,
  - jedna zložka popisuje veľkosť uhla,
  - dve zložky označujú rovinu, v ktorej sa vektor bude otáčať.

---

## 34. Transformácia otočenia rastrového objektu

Podklady rozlišujú dve stratégie:

### a) Priame otáčanie (s interpoláciou protiľahlých bodov)
- „idem po pixeloch a hľadám ich nové pozície“
- problém: v rastri pracujeme s celými číslami, vznikajú float hodnoty a pri zaokrúhľovaní:
  - môže sa stať, že na 1 miesto „padnú“ 2 pixely  
    - stratégie podľa podkladov: farba prvého / farba posledného
  - môžu vznikať „diery“
    - riešenie: masková matica obsadenosti (0/1); tam kde ostane 0, doplní sa farba (v podkladoch: „väčšinou medián“)

### b) Spätné otáčanie (s interpoláciou všetkých bodov)
- vezmem vzor a otočím len jeho hraničné body (vrcholy),
- medzi vrcholmi vypočítam úsečky (Bresenham) → dostanem hrany,
- v ohraničenej oblasti počítam **spätne transformáciu**, aby som správne určil farby,
- použijem **inverznú maticu**,
- podľa podkladov „vedie jednoznačne k cieľu“.

---

## 35. Morphing, warping

- Podklady v tomto výpise neuvádzajú konkrétny postup alebo definície pre morphing/warping (je tu len názov otázky).  
- Zároveň sa v podkladoch uvádza existencia **nelineárnych transformácií** (napr. distorzia, rybie oko, panoráma, zošikmenie), do ktorých sa morphing/warping tematicky zaraďujú.

---

## Rýchle skúškové zhrnutie (čo vedieť povedať)
- Transformácie patria do 2. fázy vizualizačného procesu; transformácia mení vstupný objekt na výstupný.
- Transformácie môžu byť paralelné alebo sekvenčné; aby bolo zreťazenie lineárne, všetky dielčie transformácie musia byť lineárne.
- Lineárne/afinné: zrkadlenie, zmena mierky, posunutie, skosenie, otočenie; nelineárne: distorzia, rybie oko, panoráma, zošikmenie.
- Transformančný reťazec (medzisústavové transformácie): GT, PT, ZT, OT; zmenu (napr. „zväčšenie“) viem spraviť v rôznych častiach reťazca.
- Homogénne súradnice: pomocná dimenzia; matice pre 2D 3×3, pre 3D 4×4; typicky neutralita 1 v homogenizačnej osi pri maticových výpočtoch.
- Zrkadlenie 2D: výmena znamienok podľa osi (x, y, stred); raster sa zrkadlí výmenou po riadkoch/stĺpcoch.
- Zmena mierky raster: zväčšenie s priamym a korekčným koeficientom; zmenšenie cez subpixely (2×2, 3×3, ...) a určenie farby (priemer/medián/častosť/...).
- Rotácia: Eulerove uhly (postupné rotácie okolo osí) vs quaternióny; rotácia okolo všeobecnej priamky cez posuny/rotácie a návraty.
- Gimbal lock: strata stupňa voľnosti; DOF vysvetliť (napr. v 3D translácia 3 + rotácia 3).
- Rotácia rastra: priame otáčanie (kolízie, diery → maska + doplnenie farby) vs spätné otáčanie (inverzná matica, jednoznačný výsledok).
