# PC Languages and Domain-Specific Languages (DSL): odpovede zo zdroja VyvojDSL_v3.pdf

### 1. Vysvetlite pojem DSL, porovnajte GPL a DSL
`Doménovo-špecifický jazyk (DSL)` je navrhnutý na špecifikáciu riešení v konkrétnej problémovej doméne, na rozdiel od `jazykov všeobecného použitia (GPL)`. Cieľom `DSL` je zvýšiť úroveň abstrakcie a používať pojmy a zápisy domény, aby sa riešenia dali zapisovať „rečou domény“. 
`DSL` môže mať `textovú` aj `vizuálnu` konkrétnu reprezentáciu. Jeden jazyk môže mať `viacero konkrétnych reprezentácií` pri rovnakej abstraktnej syntaxi.
`GPL` umožňujú zapísať ľubovoľný algoritmus a ich vyjadrovacia sila je ekvivalentná Turingovmu stroju (typicky sa uvádzajú ako Turing-úplné). Paradigmy programovacích jazykov sa v dokumente viažu práve k `GPL` a určujú ich „spôsob myslenia“.

---

**Porovnanie v skratke:**
- `DSL`: vyššia abstrakcia pre konkrétnu doménu, pojmy domény sú „priamo“ v jazyku, často lepšia statická analýza vďaka explicitným doménovým konštruktom.
- `GPL`: univerzálne použitie, ale riešenie doménových problémov často vyžaduje transformovať myslenie z domény problému do domény riešenia pomocou abstrakcií danej paradigmy.

_[*Zdroj: VyvojDSL_v3.pdf, str. 7, 9-11*]_

---

### 2. Vysvetlite čo je paradigma programovacieho jazyka, uveďte príklady
`Paradigma programovacieho jazyka` predstavuje základný spôsob myslenia v programovaní sprostredkovaný počítačovým jazykom. Paradigmy sa odlišujú tým, aké pojmy a abstrakcie používajú na reprezentáciu programov a ako vedú programátora pri transformácii riešenia do implementácie. Uvádza sa aj, že dnešné GPL bývajú často `multiparadigmatické` (podporujú viac paradigiem).

**Medzi najvýznamnejšie paradigmy v súčasnosti patria:**
- objektovo-orientovaná paradigma,
- komponentovo-orientovaná paradigma,
- funkcionálna paradigma,
- paradigma logického programovania,
- aspektovo-orientovaná paradigma.

_[*Zdroj: VyvojDSL_v3.pdf, str. 7*]_

---

### 3. Opíšte spôsob použitia DSL v softvérovom vývoji - architektúra spracovania DSL
`Abstraktná syntax jazyka` je definovaná doménovým modelom.Po vytvorení modelu sa určí konkrétna syntax (napr. anotáciami) a z anotovaného doménového modelu je vygenerovaný jazykový procesor. Jazykový procesor spracúva vety so znalosťou konkrétnej aj abstraktnej syntaxe a sémantiky. Dokument opisuje DSL v softvérovom vývoji najmä cez:
- `(a) typ DSL`, 
- `(b) jazykový procesor`.

**Jazykový procesor** (spracovanie viet jazyka):

1. **Externé DSL**: autor vytvára `samostatný jazykový procesor` (parser/kompilátor/interpreter) na spracovanie viet DSL. Typicky sa používajú `generátory jazykových procesorov`, kde vstupom je formálna špecifikácia (napr. bezkontextová gramatika) a výstupom zdrojový kód procesora.

2. **Interné DSL**: DSL je implementované „vnorením“ do hostiteľského jazyka (napr. Java) a využíva jeho syntaktické a sémantické mechanizmy (API, fluent rozhrania, atď.).

3. **Jazykové prostredia (language workbenches)**: prostredia, ktoré pomáhajú navrhovať jazyk, editory a nástroje (transformácie, generovanie, atď.).

Pri spracovaní viet (v dokumente najmä na príklade YAJCo) je typická architektúra:
- `vstupná veta (text)` → rozpoznanie vety (parser) → konštrukcia AST (abstraktný syntaktický strom) ako objektov doménových tried,
- `následne sémantika` realizovaná ako metódy/akcie nad uzlami AST (napr. vyhodnotenie, validácia, interpretácia alebo generovanie).

_[*Zdroj: VyvojDSL_v3.pdf, str. 7, 20-23, 31, 50, 65*]_

---

### 4. Porovnajte modely a programy - rozdiely a podobnosti, vykonateľné modely
`Doménový model` je abstrakcia domény, ktorá definuje pojmy, ich vzťahy a význam. `Program` je veta vytvorená programovacím jazykom. 

**Pojem `počítačové jazyky` môže okrem programovacích jazykov zahŕňať:**
- doménovo-špecifické jazyky, 
- údajové modely, 
- ontológie a modelovacie jazyky.

**Podstatné je, že:**
- abstraktná syntax (napr. metamodel alebo doménový model) opisuje pojmy a vzťahy, a je úzko spätá so sémantikou,
- `vykonateľnosť` je dosiahnutá tým, že sa sémantika realizuje buď `interpretáciou` (priamo sa vyhodnocuje/ vykonávajú sa akcie), alebo `generovaním` (transformácia do iného jazyka alebo artefaktu).

Príklad vykonateľnosti v dokumente: pre jazyk didaktických testov je možné generovať HTML test (výstupný artefakt) alebo priamo interpretovať test pri skúšaní.
Obe sú formálne artefakty so štruktúrou a významom. `Model` môže byť vykonateľný vtedy, ak má definovanú `sémantiku` a existuje `procesor`, ktorý ju realizuje interpretáciou alebo generovaním.

_[*Zdroj: VyvojDSL_v3.pdf, str. 5, 7, 15, 31, 63-65*]_

---

### 5. Charakterizujte výhody a nevýhody použitia DSL v softvérovom vývoji
**Výhody:** 
- vyššia úroveň abstrakcie, 
- riešenia sa zapisujú pojmami a štýlom domény,
- možnosť efektívnejšej statickej analýzy programov, keďže pojmy domény sú explicitné. 

**Nevýhody:** 
- implementácia textových DSL je často náročná
- vyžaduje expertné znalosti jazykových procesorov a gramatík a je často náročná
- autor musí mať expertízu v doméne aj vo vývoji jazykov.

_[*Zdroj: VyvojDSL_v3.pdf, str. 9-12*]_

---

### 6. Argumentujte prečo je nejaký konkrétny jazyk DSL, resp. GPL
**Dokument rozlišuje DSL a GPL primárne podľa cieľa a rozsahu použitia:**
- jazyk je `DS`L, ak je navrhnutý na špecifikáciu riešení v konkrétnej problémovej doméne a používa pojmy domény,
- jazyk `GPL` je určený na všeobecné použitie, umožňuje zapísať ľubovoľný algoritmus (jeho vyjadrovacia sila je ekvivalentná Turingovmu stroju) a paradigmy charakterizujú jeho štýl programovania.

_[*Zdroj: VyvojDSL_v3.pdf, str. 7, 9, 11*]_

---

### 7. Opíšte a rozlíšte konkrétnu a abstraktnú syntax jazyka a sémantiku jazyka
**Abstraktná syntax**: vnútorná štruktúra jazyka - pojmy jazyka a pravidlá ich kompozície, opisuje vnútornú štruktúru jazyka a používa sa pre definovanie sémantiky jazyka a programov. 

**Konkrétna syntax**: zápis abstraktných konštrukcií pomocou konkrétnych symbolov (textových alebo vizuálnych). Určuje, ako sú jazykové elementy reprezentované v podobe, ktorú môže interpretovať človek aj počítač. Existuje viacero foriem pre konkrétnu reprezentáciu jazyka. 

**Medzi tieto formy patrí napríklad:** 
- textová forma, 
- vizuálna forma, 
- respektíve kombinácia týchto foriem. 

**Sémantika**: definuje význam viet jazyka prostredníctvom významu elementov a pravidiel ich kompozície.

_[*Zdroj: VyvojDSL_v3.pdf, str. 14-16, 19, 37*]_

---

### 8. Charakterizujte jazykový (sémantický) model a jeho zápis v OOP, uveďte príklad zápisu jazykového modelu v OOP
Doménový (jazykový) model predstavuje abstrakciu domény a definuje pojmy, ich vzťahy a význam. Môže byť reprezentovaný diagramom tried a v implementácii aj triedami jazyka Java. 

**Príklad zápisu doménového modelu v OOP:**
```java
public abstract class Expression {
    // Sémantické funkcie
    public abstract long eval();
    public abstract List<Instruction> code();
}
```

**Zápis v OOP (Java):**
- pojmy jazyka sa mapujú na doménové triedy a ich vzťahy na OOP väzby (napr. dedičnosť cez `extends`, rozhrania cez `implements`),
- dokument priamo ukazuje mapovanie dedičnosti (napr. `Statement`, `If`, `While`) a ekvivalent v BNF: `Statement ::= If | While`,
- v prístupe YAJCo sú doménové triedy základom pre AST (uzly AST sú objekty doménových tried) a sémantika sa realizuje ako metódy nad nimi.

_[*Zdroj: VyvojDSL_v3.pdf, str. 15, 29, 31, 35, 50*]_

---

## DSL typy a implementácia

### 9. Porovnajte externé a interné DSL, ich vlastnosti, výhody a nevýhody ich aplikácie
**Externé DSL:** 
- nie sú závislé od iných jazykov,
- vyžadujú vlastný jazykový procesor (často generovaný parser generátorom), čo dáva úplnú kontrolu nad syntaxou a umožňuje syntaktickú aj sémantickú kontrolu, no vyžaduje znalosť technológií spracovania textu a generátorov procesorov. 

**Interné DSL:** 
- sú vložené do hostiteľského GPL (napr. java) a využívajú jeho mechanizmy,
- nevyžadujú samostatný procesor a zjednodušujú implementáciu, ale syntax je ovplyvnená hostiteľským jazykom.

**Jazykové prostredia** sú tretí prístup, kde veľa podpory pre editor, transformácie a generovanie poskytuje nástroj (workbench).

_[*Zdroj: VyvojDSL_v3.pdf, str. 20-21, 23, 66-68*]_

---

### 10. Aký je rozdiel medzi použitím generovania a interpretácie pri implementácii DSL
**sémantika v jazykových procesoroch sa najčastejšie realizuje**:
- `generatívnym prístupom`: z vety v DSL sa vygeneruje veta/artefakt v inom jazyku (napr. HTML výstup),
- `interpretačným prístupom`: vstupná veta sa priamo interpretuje (vyhodnocuje), čo vedie k vykonaniu akcií.

Výber generovania vs interpretácie závisí od rozhodnutia dizajnéra a okolností použitia (nie od samotnej syntaxe).

_[*Zdroj: VyvojDSL_v3.pdf, str. 63-65*]_

---

### 11. Rozlíšte vzory pre implementácie interných DSL
**Function Sequence:** 
- veta je zapísaná ako postupnosť volaní definovaných funkcií,
- implementácia typicky udržiava „rozostavaný“ stav (aktuálnu otázku, zoznam odpovedí) a pri prechode medzi časťami skladá výsledný model.

**Nested Function:** 
- veta je zapísaná ako postupnosť volaní vnorených funkcií,
- dokument uvádza aj implementáciu buildera, kde sa vety skladajú cez volania, ktoré vytvárajú `Question`, `Answer`, atď.

**Method Chaining:** 
- veta je zapísaná ako zreťazenie volaní metód.

**Literal List/Map:**
- dokument demonštruje zápis viet DSL pomocou formátov `XML/JSON/YAML`, kde sa štruktúra prirodzene vyjadruje cez `zoznamy a mapy`,
- následne sa objekty načítavajú/ukladajú (napr. cez knižnicu Jackson).

_[*Zdroj: VyvojDSL_v3.pdf, str. 66-71*]_

---

### 12. Porovnajte regulárne a bezkontextové jazyky - štruktúra gramatiky a automatu
Formálne jazyky môžu byť definované gramatikou G = (N, T, P, S)
**BNF / bezkontextové gramatiky:**
- najbežnejší spôsob vyjadrenia abstraktnej a konkrétnej.

**lexikálne symboly (tokeny):**
- môžu byť definované regulárnymi výrazmi. 

**Z pohľadu spracovania viet v texte to znamená:**
- úroveň `lexikálnych jednotiek` sa definuje oddelene od vyššej štruktúry vety,
- úroveň `syntaktickej štruktúry` vety je vyjadrená produkčnými pravidlami (BNF/CFG).

Pri `bezkontextových gramatikách` sa upozorňuje, že nie pre každú bezkontextovú gramatiku je možné skonštruovať `deterministický zásobníkový automat`.

_[*Zdroj: VyvojDSL_v3.pdf, str. 6, 14-16, 22, 37, 42*]_

---

### 13. Opíšte lexikálnu, syntaktickú a sémantickú analýzu - fázy spracovania vety jazyka
**Lexikálna fáza:** 
- pracuje s lexikálnymi jednotkami (tokenmi), ktoré môžu byť definované regulárnymi výrazmi. 
**Syntaktická fáza:** 
- je založená na bezkontextovej gramatike/BNF a výsledkom je abstraktný syntaktický strom (AST) ako reprezentácia vety, kde konštrukcia AST prebieha od listov ku koreňu. 

**Sémantická fáza:** 
- využíva sémantické funkcie, ktoré mapujú syntaktické oblasti do sémantických oblastí významu.
- realizovanú ako sémantické funkcie / metódy nad doménovými triedami (napr. generovanie, interpretácia), prípadne validácia obmedzení.

_[*Zdroj: VyvojDSL_v3.pdf, str. 16, 18, 30, 33, 37, 42, 50, 63*]_

---

### 14. Porovnajte prístupy pri spracovaní vety z jazyka - zhora nadol (top-down) a zdola nahor (bottom-up)
**zhora nadol (top-down):**
- postupuje od koreňa (štartovacieho symbolu gramatiky) smerom k listom (skutočným slovám vo vete). Snaží sa predpovedať, ktoré pravidlo gramatiky bolo použité,
- je intuitívnejší pre ručné písanie parsera,
- nezvláda ľavú rekurziu (musí sa z gramatiky odstrániť),
- príklad nástroja: `JavaCC, ANTLR`a typické gramatiky sú LL (napr. LL(k)).

**zdola nahor (bottom-up):**
- začína od jednotlivých slov (listov) a postupne ich zoskupuje (redukuje) do vyšších syntaktických celkov, až kým nedosiahne koreň,
- je silnejší, dokáže spracovať širšiu triedu gramatík (vrátane ľavej rekurzie),
- je náročnejší na manuálnu implementáciu, zvyčajne sa generuje automaticky.
- príklad nástroja: `YACC, Bison` a typické gramatiky: `LR (napr. LR(1), LALR)`.

_[*Zdroj: VyvojDSL_v3.pdf, str. 26-27*]_

---

### 15. Opíšte ako funguje spracovanie viet na základe oddeľovačov - delimiter-directed translation (parsing)
Pri definovaní konkrétnej syntaxe sa používajú lexikálne symboly, ktoré predchádzajú alebo nasledujú konštrukcie, a `oddeľovače` (napr. čiarky) na oddelenie postupnosti konštrukcií toho istého typu. Takéto delimiterové symboly pomáhajú parseru určiť hranice konštrukcií vo vete.

**oddeľovače**:
- anotácie **@Before, @After, @Separator** určujú lexikálne symboly, ktoré sa majú objaviť pred/za konštrukciou alebo medzi prvkami zoznamu,
- tieto oddeľovače nemajú vplyv na sémantiku; slúžia na jednoznačné určenie štruktúry vety.

[*Zdroj: VyvojDSL_v3.pdf, str. 37-39*]

---

### 16. Napíšte gramatiku v BNF pre určený jazyk
Príklad BNF (jazyk stavových automatov):
```bnf
StateMachine ::= StartState State+ Transition+
State ::= Identifier
StartState ::= Identifier
Transition ::= Identifier Identifier
```
[*Zdroj: VyvojDSL_v3.pdf, str. 17*]

```
Expression1 ::= Expression2 (('-' | '+') Expression2)*
Expression2 ::= Expression3 (('*' | '/') Expression3)*
Expression3 ::= '-' Expression3 | Expression
Expression ::= Number | 'LPAR' Expression1 'RPAR'
Number ::= <VALUE>
```
[*Zdroj: VyvojDSL_v3.pdf, str. 52*]

### 17. Opíšte stromové reprezentácie viet - strom odvodenia (parse tree), abstraktný syntaktický strom - ich vytvorenie a prechádzanie
Bezkontextové gramatiky definujú množinu `stromov`, prostredníctvom ktorých je možné reprezentovať vety z jazyka (strom odvodenia). `Abstraktný syntaktický strom` je stromová reprezentácia abstraktnej štruktúry vety, kde každý uzol predstavuje výskyt jazykového pojmu. `AST` je vytvorený jazykovým procesorom zo vstupnej vety.

**AST:**
- parser rozpozná vetu a **konštruuje AST**, ktorého uzly sú **objekty doménových tried**,
- AST sa konštruuje **od listov ku koreňu**,
- sémantika sa vykonáva nad uzlami (napr. metódy, visitor v príkladoch).

Dokument tiež porovnáva metamodely a bezkontextové gramatiky tým, že metamodely definujú množinu syntaktických grafov, zatiaľ čo bezkontextové gramatiky definujú množinu stromov pre reprezentáciu viet.

_[*Zdroj: VyvojDSL_v3.pdf, str. 15, 17-18, 34, 50*]_

---

### 18. Charakterizujte prácu so symbolmi v programoch - tabuľka symbolov, oblasti viditeľnosti
Textové jazyky používajú `identifikátory` na odkazovanie na výskyty pojmov. `Identifikátor` musí jednoznačne identifikovať `výskyt` pojmu a okrem mena rozhoduje aj `kontext` (oblasť platnosti). `Referencie` medzi výskytmi pojmov sú následne realizované v a`bstraktnom syntaktickom grafe` a môžu byť vytvorené nástrojom na vyhľadávanie referencií. `Jazykový procesor` po rozpoznaní vety určuje referencie a vytvára zdieľanie výskytov pojmov (graf).

_[*Zdroj: VyvojDSL_v3.pdf, str. 52-55*]_

---

### 19. Opíšte generátory jazykových procesorov - načo slúžia a ako sa používajú (napr. Antlr)
Generátor jazykových procesorov vytvára jazykový procesor z formálnej špecifikácie. Vstupom býva bezkontextová gramatika a výstupom zdrojový kód procesora. Generátory umožňujú určiť konkrétnu syntax aj sémantické akcie a často vedia automaticky generovať AST. 

**Medzi známe generátory patria:** 
- Lex/Yacc, 
- JavaCC, 
- ANTLR.

Zároveň dokument prezentuje prístup, kde sa procesor negeneruje priamo z gramatiky, ale z `doménového modelu rozšíreného anotáciami` (YAJCo), pričom výsledkom je parser a konštrukcia AST z objektov doménových tried.

_[*Zdroj: VyvojDSL_v3.pdf, str. 20, 22, 26, 50*]_

---

### 20. Opíšte vzťah doménovo-špecifických jazykov a modelom riadeného vývoja softvéru - DSL a MDSD
Vyvoj DSL je opisovaný ako prístup k budovaniu softvéru v kontexte modelom riadeného vývoja. Používanie DSL pri MDSD zjednodušuje realizáciu evolúcie, no vyžaduje riešenie kompozície DSL a mechanizmov ich evolúcie.

**Dokument spája DSL s modelom riadeným vývojom najmä cez:**
- `metamodely` ako prístup definície abstraktnej syntaxe (významné postavenie v MDSD; príklad UML),
- vytváranie jazykov a nástrojov, ktoré možno začleniť do procesu tvorby riešenia „v prípade modelom riadeného vývoja“.

_[*Zdroj: VyvojDSL_v3.pdf, str. 5, 15, 77*]_

---

### 21. Charakterizujte jazykové prostredie - funkcie, význam, príklady (language workbenches)
Language workbenche sú prostredia pre tvorbu DSL a doménové modelovanie. 

**Umožňujú vytvárať:**
- grafické dizajnéry pre vizuálne jazyky, 
- návrh jazykov (najmä grafických),
- písať transformácie z grafických modelov do výstupného jazyka
- generovať výstupné vety.

_[*Zdroj: VyvojDSL_v3.pdf, str. 23-25*]_

---

### 22. Opíšte princíp projekčných editorov, porovnajte ich s klasickými textovými editormi
Zdroj explicitne nepomenúva projekčné editory. Uvádza však, že DSL môže mať textovú aj grafickú (vizuálnu) konkrétnu reprezentáciu a že language workbenche umožňujú vytvárať grafické dizajnéry pre vizuálne jazyky.

_[*Zdroj: VyvojDSL_v3.pdf, str. 11, 25*]_

---

### 23. Opíšte generovanie kódu z modelu a porovnajte – generovanie pomocou šablón vs. generovanie transformáciou
Pri generovaní sémantiky transformáciou metódy opisujú, ako sa transformuje vstupná veta (abstraktný syntaktický graf) na výstupnú vetu v cieľovom jazyku. Alternatívou je použitie šablónovacích systémov, ktoré sú vhodné, keď je veľká časť výstupu nemenná a v šablóne je výstupný text ľahšie identifikovateľný. Zdroj tiež popisuje generovanie jazykového procesora z doménového modelu rozšíreného o anotácie konkrétnej syntaxe.

**Dokument ukazuje dva praktické prístupy:**
- `generovanie transformáciou „v kóde“`: metódy v Jave opisujú transformáciu vstupnej vety (AST) na výstupný text,
- `generovanie pomocou šablónovacích systémov`: vhodné, keď je veľká časť výstupu nemenná, uvedený príklad je `Velocity`.

_[*Zdroj: VyvojDSL_v3.pdf, str. 30, 64-66*]_

---

### 24. Ako je možné prepojiť generovaný kód a ručne napísaný kód – význam jeho oddelenia
**Cieľ oddelenia:** aby si mohol kód **znovu generovať bez straty ručných úprav** a aby bol jasný rozdiel medzi „mechanicky“ generovanou časťou a biznis logikou.

**Bežné spôsoby prepojenia:**
- **Generation Gap (dedenie):** generátor vytvorí základnú triedu, ručný kód ju rozšíri (`Foo extends FooGenerated`).
- **Rozhranie + implementácia:** generátor vytvorí `IFoo`, ručný kód dodá implementáciu alebo adapter.
- **Kompozícia/delegácia:** ručný kód obalí generovaný a deleguje volania (wrapper/facade).
- **Partial classes/methods (napr. C#):** generované a ručné časti sú v separátnych súboroch, kompilátor ich spojí.
- **Protected regions / merge:** generátor zachová označené ručné bloky alebo zlučuje zmeny.

**Prečo to robiť:** bezpečná regenerácia, jednoduchšia údržba, čistejšia architektúra a menej konfliktov pri zmenách modelu/generátora.