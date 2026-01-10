# Modularita a softvérová architektúra — odpovede (psi-lecture-notes-wip.pdf)

### 1. Vysvetlíte čo je to modularita a prečo je podstatná vo vývoji softvéru.
Modularita je **miera**, do akej vieme systém rozdeliť na **oddelené komponenty (moduly)** a tieto časti potom **znovu kombinovať**. Cieľom je najmä **flexibilita**: aby sa systém dal rozumne meniť, rozširovať a skladať bez toho, aby sme museli rozumieť alebo prerábať „všetko naraz“.

Prečo je modularita podstatná (hlavné dôvody):
- **Pochopenie kódu:** reálny softvér je zložitý; bez delenia na časti ho ako celok nedokážeme pochopiť. Modularizácia nám umožní rozumieť systému po menších, zvládnuteľných častiach.
- **Tímová práca:** keď vyvíja viac ľudí/tímov, potrebujeme deliť prácu tak, aby sa dalo pracovať **paralelne** a čo najnezávislejšie (bez neustáleho „šliapania“ po rovnakom kóde).
- **Flexibilita (zmeny):** softvér sa stále mení; modulárny systém znižuje riziko, že zmena v jednej oblasti „rozbije“ iné časti a zjednodušuje nájsť miesto zmeny aj ju bezpečne urobiť.

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 5–6*]_

---

### 2. Ako súvisí modularita s testovaním softvéru?
Modularita a testovanie sa podporujú navzájom:

- **Testovanie celého systému naraz** je pri zložitejších programoch problematické, lebo počet kombinácií vstupov a stavov je prakticky nekonečný.
- Pri **testovaní modulov samostatne** sa sústredíme len na premenné relevantné pre daný modul. Tým sa znižuje počet možností a testovanie je realistickejšie a lacnejšie.
- **Deterministické testy**: testy majú pri rovnakých vstupoch dávať rovnaký výsledok. Modulárny návrh pomáha izolovať moduly od času, paralelizmu a externých vplyvov, takže sa dá dosiahnuť deterministickosť.
- Praktická spätná väzba: keď sa k časti kódu **ťažko píšu testy**, často je problém práve v **štruktúre a dekompozícii**. TDD (test-driven development) prirodzene tlačí návrh smerom k lepšej modularite.
- Pri dobrej modularite a oddelení technických detailov vieme v testoch použiť **mock/fake** namiesto reálnej databázy či externých služieb.

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 6–7, 13, 24*]_

---

### 3. Vysvetlíte význam pojmu kohézia (cohesion) v softvéru.
**Kohézia (cohesion)** vyjadruje, **do akej miery prvky v jednom module patria k sebe** – teda či modul drží pokope tematicky a funkčne, rieši „jednu súvisiacu vec“.

Intuícia:
- Ak dáme **všetko do jedného modulu**, kohézia je paradoxne nízka (miešajú sa nesúvisiace záujmy).
- Ak dáme **každý malý fragment do samostatného modulu**, tiež klesá kohézia (veci, ktoré spolu úzko súvisia, sú zbytočne rozdelené) a typicky rastie prepojenosť medzi modulmi.
- Hľadáme **rovnováhu**, kde modul obsahuje súvisiace veci, ktoré sa typicky menia spolu.

Kohéziu podporuje aj princíp **oddelenia záujmov (Separation of Concerns)**: kód riešiaci „jednu vec“ má byť na jednom mieste a nemáme miešať nesúvisiace záujmy (napr. doménovú logiku s detailmi databázy alebo práv).

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 7–9, 19*]_

---

### 4. Vymenujte a stručne vysvetlite hlavné princípy pre dekompozíciu softvérových systémov.
Dekompozícia = rozhodnutie, **kde viesť hranice** medzi modulmi (viacúrovňovo: služby → komponenty → triedy → metódy). Dokument zdôrazňuje, že neexistuje jedno univerzálne pravidlo, ale sú princípy a kritériá, ktoré pomáhajú:

1. **Vysoká kohézia, nízka prepojenosť (coupling):** spolu majú byť veci, ktoré spolu súvisia a menia sa spolu; moduly medzi sebou majú mať čo najmenej väzieb.
2. **Oddelenie záujmov (SoC):** nemiešať nesúvisiace veci; oddeliť napr. doménovú logiku od technických detailov (DB/HTTP).
3. **Skrývanie informácií (information hiding):** deliť systém tak, aby každý modul skrýval konkrétne návrhové rozhodnutie – zmeny potom zasiahnu minimum modulov.
4. **Kritériá dekompozície podľa Parnasa:**  
   - **Zmeniteľnosť:** zmena jedného rozhodnutia (napr. spôsob uloženia dát) má meniť čo najmenej modulov.  
   - **Nezávislý vývoj:** tímy sa majú dohadovať najmä na abstraktných rozhraniach, nie na interných formátoch.  
   - **Jednoduchosť pochopenia:** moduly majú byť natoľko nezávislé, aby sme ich vedeli pochopiť bez nutnosti rozumieť celému systému.
5. **Rozhrania a abstrakcie:** medzi modulmi majú byť jasné (a malé) rozhrania; často sa používajú abstrakcie z domény (domain-driven design).
6. **Oddelenie technických detailov (napr. cez ports & adapters / dependency injection):** závislosti od technológií sa izolujú do adapterov a jadro zostáva čisté.

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 7–11, 13*]_

---

### 5. V čom spočíva princíp skrývania informácii (information hiding) v návrhu softvéru a ako súvisí s dekompozíciou?
**Information hiding** znamená: pri návrhu modulov **skryť návrhové rozhodnutia** (interné detaily), aby ich neskoršia zmena ovplyvnila **čo najmenej** ostatných modulov.

Ako to súvisí s dekompozíciou:
- Pri dekompozícii sa pýtame, **podľa čoho** rozdeliť systém. Parnas ukazuje, že dekompozícia podľa „krokov spracovania“ vedie k tomu, že moduly zdieľajú interné rozhodnutia (napr. formát uloženia dát) a potom zmena zasiahne veľa modulov.
- Dekompozícia založená na information hiding delí systém tak, že každý modul zodpovedá za jedno konkrétne rozhodnutie a ostatní k nemu pristupujú cez **abstraktné rozhranie**. Výsledok: lepšia zmeniteľnosť, jednoduchšia koordinácia tímov a ľahšie pochopenie.

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 10–11, 13*]_

---

### 6. Čo je to prepojenosť (coupling) v návrhu softvéru a ako ju môžeme znížiť?
**Coupling (prepojenosť)** je miera, **ako silno sú časti systému navzájom previazané**. Moduly nikdy nebudú úplne nezávislé (inak by netvorili jeden systém), ale coupling sa snažíme **minimalizovať**, aby sme získali výhody modularizácie.

Ako coupling znižovať (podľa dokumentu):
- **Definovať rozhrania** medzi modulmi: malé, jasné a čo najmenej odhaľujúce interné detaily. Rozhranie je „miesto dotyku“ modulov; čím väčšie a detailnejšie, tým vyšší coupling.
- **Skrývať interné fungovanie:** ak rozhranie odhaľuje interné detaily, klienti sa stanú závislí aj od implementácie.
- **Používať abstraktné rozhrania z domény:** rozhrania majú byť v pojmoch problému/domény, nie v pojmoch technológie.
- **Ports & Adapters + Dependency Inversion:** modul si definuje port (čo potrebuje), adaptér ho realizuje pre konkrétnu technológiu; tým sa zníži závislosť doménovej logiky od technických detailov.

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 12–13*]_

---

### 7. Vymenujte a stručne vysvetlíte 4 oblastí, ktoré sú súčasťou architektúry softvéru.
Podľa knihy *Fundamentals of Software Architecture* sú architektúrou tieto štyri oblasti:

1. **Štruktúra systému:** rozdelenie na komponenty a vzťahy medzi nimi.
2. **Architektonické charakteristiky („-ilities“):** vlastnosti ako testovateľnosť, udržiavateľnosť, spoľahlivosť a spôsoby, ako ich dosiahnuť.
3. **Architektonické rozhodnutia:** rozhodnutia o tom, ako bude systém fungovať počas vývoja aj prevádzky.
4. **Návrhové princípy:** princípy používané pri návrhu komponentov; systém je „fraktálny“ (komponenty sa delia na menšie), a princípy platia naprieč úrovňami.

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 14–15*]_

---

### 8. Aké vlastnosti by mal mať softvérový architekt?
Z textu vyplýva, že architekt je zodpovedný za kľúčové rozhodnutia a ich udržiavanie v čase. Mal by mať najmä:

- **Schopnosť robiť a priebežne vyhodnocovať architektonické rozhodnutia** o najdôležitejších vlastnostiach systému.
- **Prehľad o aktuálnych trendoch a technológiách** (nemá „uviaznuť“ v starých prístupoch).
- **Schopnosť presadzovať dodržiavanie rozhodnutí** (manažérsky aj technicky – napr. pomocou nástrojov a automatických kontrol).
- **Znalosť domény** (napr. bankovníctvo/medicína), aby vedel správne modelovať a deliť systém.
- **Soft skills, najmä komunikáciu:** komunikuje s tímom aj zákazníkom; musí sa orientovať aj v organizačnom kontexte.

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 15*]_

---

### 9. Vymenujte a stručne vysvetlite SOLID princípy.
SOLID je sada piatich princípov objektovo-orientovaného návrhu:

- **S — Single Responsibility Principle (SRP):** modul má mať **jeden dôvod na zmenu**. V texte sa dôvod viaže na konkrétneho „aktéra“ (typ používateľa/skupina), aby sme nemiešali potreby rôznych aktérov do jedného modulu.
- **O — Open–Closed Principle (OCP):** artefakt má byť **otvorený pre rozširovanie**, ale **uzavretý pre modifikáciu**. Správanie by sme mali meniť skôr rozšírením než úpravou existujúceho kódu, aby sme znížili riziko vedľajších efektov.
- **L — Liskov Substitution Principle (LSP):** objekt podtypu musí byť použiteľný všade tam, kde očakávame nadtyp, **bez rozbitia správania**; podtyp nesmie porušiť vlastnosti, ktoré platia pre nadtyp.
- **I — Interface Segregation Principle (ISP):** rozhrania navrhujeme z pohľadu klienta; klient nemá závisieť od metód, ktoré nepotrebuje. Preto je lepšie mať viac menších rozhraní.
- **D — Dependency Inversion Principle (DIP):** vysokoúrovňové moduly (doménová logika) nemajú závisieť od nízkoúrovňových (technické detaily). Obe majú závisieť od **abstrakcií**; detaily majú závisieť od abstrakcií, nie naopak.

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 16–19*]_

---

### 10. Vysvetlite princíp „čistej architektúry“.
Čistá architektúra (podľa R. C. Martina) sa snaží rozdeliť systém tak, aby sme **oddeliili doménovú logiku od technických detailov**.

Kruhový model vrstiev:
- **Entity (jadro):** základné doménové objekty a ich pravidlá – najstabilnejšia časť.
- **Scenáre použitia (use cases):** logika operácií/„príbehov“ systému.
- **Adaptéry/medzivrstva (kontroléry, prezentéry, brány/gateways):** preklad medzi doménou a vonkajším svetom.
- **Externé rozhrania (UI, DB, web, zariadenia, externé služby):** technické detaily na okraji.

Kľúčové pravidlo: **závislosti v kóde smerujú iba dovnútra** (vonkajšie vrstvy závisia od vnútorných, nie naopak). Vďaka tomu je jadro systému stabilné a menej závislé od rámcov, databáz a iných technológií.

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 22–24*]_

---

### 11. Vysvetlíte princíp otočenia závislostí a aký problém je možné pomocou neho riešiť.
**Otočenie závislostí (dependency inversion)** rieši problém, že doménová (vysokoúrovňová) logika by nemala byť „prilepená“ na konkrétne technické detaily (DB, API, UI).

Princíp:
- Namiesto toho, aby doménový modul priamo volal konkrétnu databázu/externú službu, vložíme medzi ne **abstrakciu (rozhranie/port)** definovanú v pojmoch domény.
- Doménový modul závisí od rozhrania; technický modul (adaptér) toto rozhranie implementuje. Tým sa závislosť v kóde **otočí** (detaily závisia od abstrakcií).

V čistej architektúre sa to prejaví cez **vstupné/výstupné porty**: scenár použitia komunikuje smerom von cez rozhranie (port), ktoré implementuje prezentér alebo iný adaptér. Tok riadenia počas behu môže ísť „z vonku dovnútra a späť“, ale závislosti v zdrojáku ostávajú smerom dovnútra.

Aký problém tým riešime:
- **Zníženie prepojenosti** a izolácia náhodnej zložitosti (technológie) od podstatnej zložitosti (doména).
- **Testovanie:** v testoch vieme dať fake/mock implementáciu portu namiesto reálnej databázy či služby.
- **Vymeniteľnosť technológií:** zmena DB/frameworku nevyžaduje zásah do jadra domény.

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 13, 19, 23–24*]_

---

### 12. Vymenujte a stručne opíšte aspoň 4 architektonické štýly.
Dokument uvádza prehľad štýlov (Richards a Ford 2020) a stručne opisuje najmä tieto:

- **Layered (vrstvená, n-tier):** systém je rozdelený na vrstvy (napr. databáza, biznis logika, UI). Je to technologické delenie, typicky s 3+ vrstvami.
- **Service-Based:** systém je rozdelený na viac služieb podľa častí domény; služby môžu mať rôzne UI/DB modely (spoločné alebo oddelené), variabilita je veľká.
- **Event-Driven:** časti systému komunikujú pomocou udalostí cez message queues; spracovanie je reakciou na udalosti.
- **Space-Based:** práca s dátami bez jednej centrálnej databázy; dáta sú distribuované.
- **Service-Oriented Architecture (SOA, orchestration-driven):** prístup založený na službách s centrálnym message hubom/orchestrátorom, ktorý riadi komunikáciu; orchestrácia môže byť komplexná.
- **Microservices:** systém rozdelený na veľké množstvo menších služieb; delenie má vychádzať z domény a prepojenie má byť čo najjednoduchšie.

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 25–27*]_

---

### 13. Aké sú výhody a nevýhody distribuovaných architektúr.
**Výhody:**
- **Flexibilita a nezávislosť služieb:** služby sú samostatné procesy; môžeme použiť rôzne jazyky/technológie podľa potreby (napr. UI v JavaScripte, AI v Pythone, biznis logika v Jave).
- **Nezávislé tímy:** rozdelenie systému na služby často kopíruje rozdelenie tímov.
- **Vynútenie hraníc:** sieťová komunikácia núti používať definovaný protokol, takže sa ťažšie „nepozorovane“ porušia hranice ako v monolite.
- **Škálovateľnosť:** výkonovo náročné časti vieme spúšťať viackrát na viacerých počítačoch.

**Nevýhody:**
- **Drahšia komunikácia:** oproti volaniu metódy je HTTP/sieťová komunikácia náročnejšia; pridáva latenciu a nové miesta zlyhania.
- **Riziko zlého rozdelenia:** ak služby musia komunikovať príliš často, systém trpí a neskoršia zmena rozdelenia je náročná.
- **Vysoká zložitosť:** pribúda množstvo problémov typických pre distribuované systémy (napr. „fallacies of distributed computing“ – sieť nie je spoľahlivá, latencia nie je nulová, atď.).  

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 26–28*]_

---

### 14. Aký je význam záznamov o architektonických rozhodnutiach (Architecture Decision Records) a aké položky by mali obsahovať?
**Architecture Decision Records (ADR)** sú textové záznamy (často Markdown), kde tím **zaznamenáva architektonické rozhodnutia** a hlavne **prečo** boli urobené. Odporúča sa mať ich spolu s kódom (napr. v Gite) alebo vo wiki.

Význam:
- Umožňujú sa **spätne vrátiť** k tomu, prečo bolo rozhodnutie prijaté.
- Keď sa zmení kontext/predpoklady, ADR pomôže rozhodnutie **prehodnotiť** alebo nahradiť.
- Podporujú tímovú diskusiu a prenos znalostí; dokument uvádza, že ide o bežnú prax odporúčanú aj veľkými firmami.

Položky, ktoré by ADR mal obsahovať:
1. **Title**
2. **Context**
3. **Decision**
4. **Status**
5. **Consequences**

_[*Zdroj: psi-lecture-notes-wip.pdf, str. 28–29*]_