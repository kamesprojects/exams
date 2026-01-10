# Formálne metódy – Petriho siete a B-metóda (FMmono)

> Podklady: **FMmono_SKor_SHud.pdf** (monografia, 2015)

---

## FM.1 Čo je formálna metóda a z čoho pozostáva? Aký je vzťah medzi formálnymi metódami a programovacími jazykmi? Aké sú výhody a nevýhody formálnych metód?

### Čo je formálna metóda (FM) a z čoho pozostáva
V informatike sa **formálnymi metódami** rozumejú **techniky založené na matematike**, určené na **špecifikáciu, vývoj, analýzu a verifikáciu** počítačových systémov. Formálna metóda typicky pozostáva z:  
1) **formálneho jazyka** s **jednoznačne definovanou syntaxou a sémantikou**,  
2) **súboru procedúr / techník**, ktoré umožňujú so špecifikáciami v danom jazyku pracovať (napr. overovanie vlastností, dôkazy, simulácia/animácia).  

Sémantika jazyka je definovaná pomocou matematického aparátu (napr. logika alebo teória množín), čo odstraňuje nejednoznačnosť výkladu.  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 1–2*]_

### Vzťah medzi FM a programovacími jazykmi
- Jazyky vo formálnych metódach sa líšia od „bežných“ programovacích či špecifikačných jazykov hlavne tým, že ich význam (sémantika) nie je popísaný prirodzeným jazykom, ale formálne, jednoznačne. To znižuje priestor pre rôzne interpretácie.  
- Formálna sémantika programovacích jazykov existuje, ale v praxi býva vnímaná skôr cez správanie prekladača / strojový kód (teda menej „čitateľná“ pre ľudí).  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 1*]_

### Výhody (čo získame)
- **Jednoznačná špecifikácia** už v raných fázach vývoja → rýchlejšie odhalenie nejasností a rozporov v požiadavkách (predtým, než sa zmenia na drahé chyby v implementácii).  
- **Možnosť formálneho overovania vlastností** (verifikácia) – od jednoduchých kontrol až po strojovo vykonané dôkazy.  
- Pri metódach typu B sa zdôrazňuje, že dobre definovaný verifikačný a vývojový proces umožňuje **dokázať zachovanie požadovaných vlastností** aj počas zjemňovania (refinement) až po implementáciu.  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 2–3, 52, 54*]_

### Nevýhody / praktické limity
- **Náklady na osvojenie**: nový jazyk, metodika, nástroje; často aj zmena vývojových návykov. (Toto je jedna z príčin „mýtu“, že FM vývoj vždy predražia.)  
- **Overovanie modelov (model checking)**: výhoda je automatickosť, nevýhoda sú **vysoké pamäťové a časové nároky** (stavová explózia) aj pri relatívne jednoduchých systémoch.  
- **Dokazovače teorém (theorem proving)**: nevyžadujú budovanie stavového priestoru, ale:
  - neúspech dôkazu neznamená automaticky, že vlastnosť neplatí,
  - často je potrebný zásah používateľa (nie úplná automatizácia).  
- Ani „silná“ FM nezaručí korektnosť, ak vlastnosť, ktorú overujeme/dokazujeme, **nezodpovedá skutočným požiadavkám** (správna formalizácia požiadaviek je kľúčová).  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 2–3*]_

---

## FM.2 Čo rozumieme pod pojmom vyjadrovacia sila formálnej metódy? Na aké úrovne vieme rozdeliť formálne metódy?

### Vyjadrovacia sila formálnej metódy
**Vyjadrovacia sila** (expressive power) formálnej metódy/jazyka vyjadruje, **akú triedu systémov, správaní a vlastností** vieme v danej notácii **presne vyjadriť** (a teda následne aj analyzovať/overovať).

Monografia používa tento pojem aj pri porovnávaní rôznych tried Petriho sietí: niektoré rozšírenia zvyšujú „modelovaciu silu“ (praktickú stručnosť a pohodlie zápisu), ale **vyjadrovacia sila môže zostať rovnaká** (t. j. trieda správaní, ktoré v princípe vieme opísať, sa nezmení).  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 33–34*]_

### Úrovne (delenie) formálnych metód podľa Bowena
Podľa J. P. Bowena sa formálne metódy (resp. ich použitie) delia na 3 úrovne:

0. **Formálna špecifikácia (úroveň 0)**  
   Máme formálnu notáciu (jazyk) na jednoznačný opis systému. Procedúry sú zvyčajne „ľahké“ (kontrola syntaxe, jednoduchá simulácia/animácia). Je to najlacnejšia úroveň – hlavný prínos je odstránenie nejednoznačností v raných fázach.

1. **Formálna verifikácia alebo vývoj (úroveň 1)**  
   Metóda poskytuje techniky na overenie, či opísaný systém má požadované vlastnosti, prípadne podporuje vývoj.

2. **Počítačom vykonaný dôkaz (úroveň 2)**  
   Navyše existujú nástroje na formálne dôkazy (napr. model checkery alebo dokazovače teorém). 

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 2*]_

---

## FM.3 Ako je formálne definovaná syntax a sémantika Petriho sietí?

Monografia sa v kapitole 2 sústreďuje na základný typ Petriho sietí – **P/T siete** (Place/Transition nets).

### Syntax (štruktúra) P/T siete
**P/T sieť** je definovaná ako usporiadaná štvorica:
\[
N = (P, T, pre, post)
\]
kde:
- \(P\) je konečná množina **miest**,
- \(T\) je konečná množina **prechodov**,
- \(pre : P \times T \to \mathbb{N}\) je **pre-podmienka** (koľko tokenov sa spotrebuje z miesta do prechodu),
- \(post : P \times T \to \mathbb{N}\) je **post-podmienka** (koľko tokenov sa vyprodukuje z prechodu do miesta).

Tieto funkcie zároveň určujú orientované hrany a ich váhy v grafe siete: hrana \(p\to t\) existuje, ak \(pre(p,t)>0\); hrana \(t\to p\) existuje, ak \(post(p,t)>0\).  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 7*]_

### Značenie (stav) a inicializovaná sieť
**Značenie** (marking) je funkcia:
\[
m : P \to \mathbb{N}
\]
kde \(m(p)\) je počet tokenov v mieste \(p\). Pri \(P = \{p_1,\dots,p_k}\) sa značenie zapisuje aj vektorovo:
\[
\vec{m} = (m(p_1),\dots,m(p_k))
\]
Inicializovaná sieť má aj počiatočné značenie \(m_0\):
\[
N_0 = (P, T, pre, post, m_0)
\]  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 7–8*]_

### Sémantika (správanie) – vykonateľnosť a vykonanie prechodu
Prechod \(t\in T\) je v značení \(m\) **vykonateľný** (enabled), ak:
\[
\forall p\in P:\; m(p) \ge pre(p,t)
\]
Po vykonaní (odpálení) prechodu \(t\) dostaneme nové značenie \(m'\):
\[
m'(p) = m(p) - pre(p,t) + post(p,t)
\]
Zmysel: tokeny sa odoberú z **pre-miest** prechodu a pridajú do jeho **post-miest**. 

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 9*]_

### Sekvencie prechodov a dosiahnuteľnosť
Sekvencia \(\sigma \in T^*\) je prípustná, ak existuje postupnosť značení, ktorá vznikne postupným vykonávaním prechodov. Značenie \(m_r\) je **dosiahnuteľné** z \(m_1\) cez \(\sigma\), ak takáto postupnosť existuje. Monografia definuje aj jazyk siete \(L(N_0)\) – množinu prípustných sekvencií z počiatočného značenia.  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 10*]_

---

## FM.4 Opíšte postup výpočtu invariantov v Petriho sieťach (môžete aj na príklade).

Invarianty sa v P/T sieťach získavajú **zo štruktúry siete** pomocou matíc (Pre, Post, incidenčná matica).

### Krok 1: Zostrojenie matíc siete
Pre sieť s \(|P|=k\), \(|T|=n\) sa definujú:
- **Pre-matica** \(Pre\in\mathbb{N}^{k\times n}\), kde \(Pre_{i,j} = pre(p_i,t_j)\),
- **Post-matica** \(Post\in\mathbb{N}^{k\times n}\), kde \(Post_{i,j} = post(p_i,t_j)\),
- **Incidenčná matica** \(C = Post - Pre\).  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 12*]_

### Krok 2: S-invarianty (miestové / place invariants)
S-invariant je stĺpcový vektor \(X\in\mathbb{Z}^k\) (typicky hľadáme aj nezáporné riešenia), ktorý spĺňa:
\[
C^T \cdot X = 0
\]
Takýto \(X\) vyjadruje lineárnu kombináciu počtov tokenov v miestach, ktorá sa **nemení** pri žiadnom odpálení prechodu. Pre všetky dosiahnuteľné značenia \(m\) platí:
\[
\vec{m}\cdot X = \vec{m_0}\cdot X
\]
Tieto rovnice sa často interpretujú ako „axiomy“ siete.  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 14–15*]_

### Krok 3: T-invarianty (prechodové / transition invariants)
T-invariant je vektor \(Y\in\mathbb{Z}^n\), ktorý spĺňa:
\[
C\cdot Y = 0
\]
Intuitívne: \(Y\) popisuje „multimnožinu“ prechodov, ktorej vykonaním (ak je realizovateľná ako nejaká sekvencia) sa sieť vráti do pôvodného značenia.  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 14*]_

### Krok 4: Riešenie sústavy rovníc
V praxi:
1) zostavíš \(C\),  
2) vyriešiš homogénnu sústavu (napr. Gaussovou elimináciou),  
3) vyberieš bázové riešenia (často so zmysluplnou interpretáciou, typicky nezáporné).

### Príklad (MutEx)
V príklade MutEx sa pre S-invarianty zostaví sústava rovníc z \(C^T\cdot X=0\), z ktorej vyplývajú konkrétne vektory \(X\) a následne axiomy typu:
- \(m(p_1)+m(p_2)=1\),
- \(m(p_3)+m(p_4)=1\),
- \(m(p_2)+m(p_4)+m(p_5)=1\),

čo zodpovedá intuitívnym vlastnostiam vzájomného vylúčenia (proces je buď mimo/v kritickej oblasti; semafor má jednu „značku“ atď.).  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 15–16*]_

---

## FM.5 Čo je B-Metóda? Aké špecifikačné komponenty sa v nej používajú? Ako je definovaný vývojový proces v B-Metóde?

### Čo je B-metóda
**B-metóda** je formálna metóda orientovaná najmä na **vývoj softvéru** (najmä sekvenčných systémov), s dôrazom na:
- formálnu špecifikáciu,
- postupné **zjemňovanie (refinement)** až na implementovateľnú úroveň,
- generovanie a dokazovanie **povinných dôkazov (proof obligations)**, ktoré potvrdzujú invarianty a korektnosť zjemnení.  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 3, 52–54*]_

### Špecifikačné komponenty v B
Základným špecifikačným stavebným prvkom je **abstraktný stroj (machine)**. Formálna špecifikácia systému je kolekcia abstraktných strojov, prepojených kompozičnými mechanizmami.

Typický (zjednodušený) tvar stroja obsahuje klauzuly ako:
- `MACHINE` (meno + parametre),
- `CONSTRAINTS` (obmedzenia parametrov),
- `SETS` (definície množín – enumerované alebo odložené),
- `ABSTRACT/CONCRETE CONSTANTS` a `PROPERTIES` (konštanty a ich typy/vlastnosti),
- `ABSTRACT/CONCRETE VARIABLES` (stavové premenné),
- `INVARIANT` (invariant stavu stroja – musí minimálne typovať premenné),
- `ASSERTIONS` (odvodené tvrdenia pre uľahčenie dôkazov),
- `DEFINITIONS` (makro-definície),
- `INITIALISATION` (počiatočný stav – substitúcia, aj nedeterministická),
- `OPERATIONS` (operácie s pre- a postpodmienkami, telo v GSL).  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 71–75*]_

Okrem `machine` sa v B vývoji objavujú aj špecifikačné komponenty typu **refinement** (zjemnenie) a **implementation** (implementácia), ktoré tvoria „reťaz“ od abstraktnej špecifikácie po implementovateľný návrh.  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 54*]_

### Vývojový proces v B-metóde (životný cyklus)
Monografia uvádza nasledujúce fázy vývoja v B:

1. **Analýza požiadaviek**  
   Neformálne alebo štruktúrované modely problému a požiadaviek (napr. UML).

2. **Vývoj špecifikácie**
   - (a) Formalizácia analytických modelov do abstraktných strojov (dekompozícia na komponenty),
   - (b) Animácia na validáciu špecifikácie voči požiadavkám a testovacím scenárom,
   - (c) Generovanie povinných dôkazov špecifikácie a ich dokazovanie.  
   Výsledok: formálna abstraktná špecifikácia (kolekcia `machine`).

3. **Návrh**
   - (a) Identifikácia dekompozície implementácie (vrátane znovupoužiteľných komponentov),
   - (b) Zjemňovanie vybraných komponentov špecifikácie (refinement),
   - (c) Generovanie povinných dôkazov zjemnení a ich dokazovanie (overenie, že zjemnenie zachováva invarianty).  
   Výsledok: konkrétny formálny návrh až po `implementation`.

4. **Kódovanie, integrácia, testovanie**
   - (a) Generovanie kódu z návrhov najnižšej úrovne / implementácií,
   - (b) Testovanie vygenerovaného kódu podľa modelových prípadov.  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 52–54*]_

---

## FM.6 Čo je zovšeobecnená substitúcia (generalised substitution)? Ako je formálne definovaná sémantika zovšeobecnenej substitúcie?

### Čo je zovšeobecnená substitúcia (GS)
**Zovšeobecnená substitúcia (generalised substitution, GS)** je základný „príkazový“ konštrukt v B (časť GSL – Generalised Substitution Language), ktorým sa zapisujú telá operácií a inicializácia. GS zahŕňa:
- priradenie \(x := e\),
- `skip`,
- nedeterministickú voľbu \(S_1 [] S_2\),
- výber/obmedzenie \(E | S\),
- precondition (predpoklad) \(E =⇒ S\),
- kvantifikovanú/nedeterministickú substitúciu \(@v.S\),
- sekvenčnú kompozíciu \(S_1 ; S_2\),
- vetvenie `if E then S1 else S2 end`,
- cyklus `while` (s invariantom a variantom) atď.

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 64–65*]_

### Formálna sémantika GS: predikátové transforméry (najslabšia pre-podmienka)
Sémantika GS je definovaná pomocou **kalkulu najslabšej pre-podmienky** (weakest precondition calculus) v zmysle Dijkstru. Každá substitúcia \(S\) sa chápe ako **transformér predikátov**:

- \([S]P\) znamená (intuícia): *najslabšia podmienka pred vykonaním S, ktorá zaručí postpodmienku P po vykonaní S*.

Monografia uvádza transformačné pravidlá, napr.:
- \([x := e]P \Leftrightarrow P[x := e]\)
- \([skip]P \Leftrightarrow P\)
- \([S_1 [] S_2]P \Leftrightarrow [S_1]P \land [S_2]P\)
- \([E|S]P \Leftrightarrow E \land [S]P\)
- \([E =⇒ S]P \Leftrightarrow E \Rightarrow [S]P\)
- \([@v.S]P \Leftrightarrow \forall v : [S]P\)
- \([S_1 ; S_2]P \Leftrightarrow [S_1]([S_2]P)\)
- \([if\ E\ then\ S_1\ else\ S_2\ end]P \Leftrightarrow (E\Rightarrow [S_1]P)\land(\neg E\Rightarrow [S_2]P)\)  

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 65*]_

### Ďalšie dôležité predikáty definované cez \([S]\cdot\)
Okrem \([S]P\) monografia definuje:
- **feasibility** (vykonateľnosť v zmysle „existuje korektný post-stav“):  
  \[
  fis(S) = \neg([S]false)
  \]
- **termination condition** (podmienka terminácie):  
  \[
  trm(S) = [S]true
  \]
- **before-after predicate** \(prd_x(S)\), ktorý charakterizuje zmenu stavu (pred-stav \(x\) a po-stav \(x'\)):  
  \[
  prd_x(S) = \neg([S](x \ne x'))
  \]

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 67–68*]_

### Rovnosť (ekvivalencia) zovšeobecnených substitúcií
Dve GS \(S_1\) a \(S_2\) sú rovnaké práve vtedy, keď pre každý predikát \(P\) dávajú ekvivalentnú najslabšiu pre-podmienku:
\[
(S_1 = S_2) \Leftrightarrow \forall P:\; ([S_1]P \Leftrightarrow [S_2]P)
\]
Toto vystihuje, že význam GS je plne daný tým, ako transformuje postpodmienky na prepodmienky.

_[*Zdroj: FMmono_SKor_SHud.pdf, str. 66*]_