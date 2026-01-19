# DSI – Poznámky (MD)/kiko

## Otázky:

6. Vysvetlite koncept Lamportových logických hodín a jeho využitie v úplne usporiadanom skupinovom vysielaní. Vysvetlite, ako umožňujú vektorové hodiny zachytiť kauzalitu medzi vysielanými správami.
7. Vysvetlite, čo je to konsenzus v skupine replikovaných procesov v distribuovanom systéme odolnom voči byzantským poruchám a aký je dôvod pre jeho zavedenie. Vysvetlite konsenzuálny protokol PBFT.
8. Presne opíšte, čo znamená pojem škálovateľný distribuovaný systém.
9. Nech klient volá asynchrónnym RPC server a následne čaká, kým server nevráti odpoveď pomocou iného asynchrónneho RPC volania. Vysvetlite, či je tento prístup rovnaký ako nechať klienta volať normálne RPC. Čo by sa stalo, ak nahradíme asynchrónne RPC volania jednosmernými (one-way) RPC volaniami?
10. Majme neblokujúci primary-backup protokol pre zabezpečenie sekvenčnej konzistencie v distribuovanom systéme. Poskytuje takýto distribuovaný systém vždy read-your-writes konzistenciu? Svoju odpoveď zdôvodnite.
11. Vysvetlite koncept spoľahlivej skupinovej komunikácie medzi replikovanými procesmi a možnosti jej škálovania. Popíšte fungovanie atómovej skupinovej komunikácie.
12. Vysvetlite problém konzistencie zameranej na údaje v distribuovanom systéme a uveďte konkrétne konzistenčné modely založené na usporadúvaní operácií. Aký je význam použitia modelu konečnej konzistencie (eventual consistency model) v praktických aplikáciách na rozdiel od silnejších modelov?
13. Majme distribuovaný systém, ktorý podporuje replikáciu objektov, v ktorej sú všetky volania metód úplne usporiadané. Predpokladajme tiež, že vyvolanie objektu je atómické. Poskytuje takýto systém vstupnú (entry) konzistenciu? A čo sekvenčnú konzistenciu?
14. Predpokladajme, že by ste mohli použiť iba neblokujúce asynchrónne komunikačné operácie na posielanie a prijímanie správ. Ako by ste implementovali blokujúce synchronné komunikačné operácie pomocou týchto asynchrónnych operácií?
15. Súbor je replikovaný na 10 serveroch. Vymenujte všetky kombinácie kvóra na čítanie a kvóra na zápis, ktoré povoľuje hlasovací algoritmus replikačného protokolu založeného na hlasovacom kvóre.

---

## 6. Vysvetlite koncept Lamportových logických hodín a jeho využitie v úplne usporiadanom skupinovom vysielaní. Vysvetlite, ako umožňujú vektorové hodiny zachytiť kauzalitu medzi vysielanými správami.

`Lamportove logické hodiny` sú mechanizmus na `určenie poradia udalostí` v distribuovanom systéme bez globálneho fyzického času. 

**Každý proces si udržiava čítač, ktorý:**

- zvyšuje pri každej lokálnej udalosti,
- zvyšuje pri odoslaní správy,
- pri prijatí správy sa nastaví na maximum lokálneho času a času zo správy + 1.

Lamportove hodiny zabezpečujú, že ak udalosť A `kauzálne predchádza` udalosti B, potom jej časová značka je menšia. Používajú sa napríklad pri total order multicaste, kde sa správy triedia podľa časových značiek (a ID procesu pri rovnosti).

Nevýhodou je, že Lamportove hodiny `nevedia rozlíšiť, či dve udalosti spolu súvisia kauzálne alebo sú nezávislé`.

Tento problém riešia vektorové hodiny. Každý proces si udržiava vektor časov, kde každá položka reprezentuje známy stav ostatných procesov. 

**Vektorové hodiny umožňujú:**

- presne určiť kauzálny vzťah medzi udalosťami,
- zistiť, či sú udalosti `kauzálne závislé alebo súbežné (concurrent)`.

Nevýhodou vektorových hodín je ich `pamäťová a komunikačná náročnosť`, keďže veľkosť vektora rastie lineárne s počtom procesov.

---

## 7. Vysvetlite, čo je to konsenzus v skupine replikovaných procesov v distribuovanom systéme odolnom voči byzantským poruchám a aký je dôvod pre jeho zavedenie. Vysvetlite konsenzuálny protokol PBFT.

`Konsenzus` je problém, pri ktorom sa skupina replikovaných procesov musí `dohodnúť na jednej spoločnej hodnote alebo poradí operácií`, a to aj v prípade, že niektoré procesy zlyhajú alebo sa správajú chybne.

V prostredí s `byzantskými poruchami` môžu uzly:

- posielať nesprávne správy,
- správať sa nepredvídateľne,
- alebo úmyselne klamať.

Preto je konsenzus nevyhnutný na zachovanie `integrity dát a konzistencie systému`.

**PBFT (Practical Byzantine Fault Tolerance) je konsenzuálny protokol, ktorý:**

- toleruje až `f byzantských uzlov`, ak je v systéme aspoň `3f + 1 replík`,
- používa viacfázovú výmenu správ (pre-prepare, prepare, commit),
- zabezpečuje, že všetky korektné uzly sa dohodnú na rovnakom poradí operácií.

PBFT nevyžaduje náročné výpočty (na rozdiel od PoW) a je vhodný pre permissioned systémy, kde je počet uzlov obmedzený.

---

## 8. Presne opíšte, čo znamená pojem škálovateľný distribuovaný systém.

Distribuovaný systém je `škálovateľný`, ak dokáže `zvládať rast záťaže` (počtu používateľov, požiadaviek alebo uzlov) bez `výrazného zhoršenia výkonu`.

**Rozlišujeme tri základné dimenzie škálovateľnosti:**

1. `Škálovateľnosť veľkosti` – schopnosť systému rásť pridaním nových používateľov alebo uzlov.
2. `Geografická škálovateľnosť` – schopnosť fungovať efektívne aj pri fyzickom rozptýlení komponentov.
3. `Administratívna škálovateľnosť` – schopnosť systému fungovať naprieč viacerými nezávislými administratívnymi doménami.

Škálovateľný systém sa vyhýba centralizovaným službám, dátam a algoritmom, ktoré by sa stali úzkym miestom, a využíva techniky ako `asynchrónna komunikácia, replikácia, cachovanie a distribúcia záťaže`.

---

## 9. Nech klient volá asynchrónnym RPC server a následne čaká, kým server nevráti odpoveď pomocou iného asynchrónneho RPC volania. Vysvetlite, či je tento prístup rovnaký ako nechať klienta volať normálne RPC. Čo by sa stalo, ak nahradíme asynchrónne RPC volania jednosmernými (one-way) RPC volaniami?

`Pri normálnom (synchronnom) RPC` je klient po odoslaní požiadavky `blokovaný`, kým server nevráti odpoveď. Klient nemôže pokračovať v práci a počas čakania nevyužíva efektívne čas.

Pri `asynchrónnom RPC` klient odošle požiadavku a pokračuje `v ďalšej činnosti`. Odpoveď zo servera je doručená neskôr, napríklad pomocou `callbacku alebo samostatného asynchrónneho volania`. 

Ak klient po odoslaní asynchrónnej požiadavky aktívne čaká na odpoveď, správanie sa môže javiť podobne ako pri normálnom RPC, ale rozdiel je v tom, že:

- komunikačný kanál nie je blokovaný,
- klient môže medzičasom vykonávať inú prácu.

Ak by sme namiesto asynchrónnych RPC použili `jednosmerné (one-way) RPC`, klient by `nedostal žiadnu odpoveď`. 

**To znamená, že:**

- klient nevie, či server požiadavku prijal,
- nevie, či bola úspešne spracovaná,
- stráca sa možnosť detekcie chýb.

One-way RPC je preto vhodné len pre operácie, kde `nezáleží na výsledku` alebo kde je výsledok riešený iným mechanizmom.

---

## 10. Majme neblokujúci primary-backup protokol pre zabezpečenie sekvenčnej konzistencie v distribuovanom systéme. Poskytuje takýto distribuovaný systém vždy read-your-writes konzistenciu? Svoju odpoveď zdôvodnite.

`Primary-backup protokol` funguje tak, že:

- všetky zápisy sú vykonávané na primárnom uzle,
- zmeny sú následne replikované na záložné (backup) uzly.

Aj keď takýto systém zabezpečuje `sekvenčnú konzistenciu`, nezaručuje vždy `read-your-writes konzistenciu`.

**Problém nastáva v situácii, keď:**

- klient zapíše hodnotu na primárny uzol,
- následne číta hodnotu z backup uzla,
- ale replikačná aktualizácia sa ešte nestihla preniesť.

V takom prípade môže klient `prečítať starú hodnotu`, aj keď jeho zápis bol úspešný. To znamená, že vlastnosť `read-your-writes` nie je splnená.

**Read-your-writes konzistencia by bola zaručená iba vtedy, ak by klient:**

- vždy čítal z primárneho uzla,
- alebo systém zabezpečil synchronizáciu replík pred čítaním.

---

## 11. Vysvetlite koncept spoľahlivej skupinovej komunikácie medzi replikovanými procesmi a možnosti jej škálovania. Popíšte fungovanie atómovej skupinovej komunikácie.

**Spoľahlivá skupinová komunikácia zabezpečuje, že správa odoslaná do skupiny je:**

- doručená všetkým korektným členom skupiny, alebo
- nedoručená nikomu.

Tým sa zabezpečí konzistentný stav medzi replikovanými procesmi.

**Pre škálovanie skupinovej komunikácie sa používajú techniky ako:**

- hierarchické skupiny,
- multicastové stromy,
- zoskupovanie uzlov do menších podskupín.

`Atómová skupinová komunikácia` (atomic multicast) rozširuje spoľahlivosť o úplné usporiadanie správ. 

**To znamená, že:**

- všetky procesy prijmú správy,
- v rovnakom poradí.

**Atómová komunikácia je základným stavebným prvkom pre:**

- replikované databázy,
- stavové replikované služby,
- implementáciu konzistentných replikačných protokolov.

---

## 12. Vysvetlite problém konzistencie zameranej na údaje v distribuovanom systéme a uveďte konkrétne konzistenčné modely založené na usporadúvaní operácií. Aký je význam použitia modelu konečnej konzistencie (eventual consistency model) v praktických aplikáciách na rozdiel od silnejších modelov?

`Konzistencia zameraná na údaje (data-centric consistency)` rieši otázku, `ako a v akom poradí` sú `operácie nad dátami viditeľné` pre rôzne procesy v distribuovanom systéme.

**Medzi konzistenčné modely založené na usporadúvaní operácií patria:**

- `Sekvenčná konzistencia` – všetky procesy vidia operácie v rovnakom poradí.
- `Kauzálna konzistencia` – zachováva príčinné vzťahy medzi operáciami.
- `Silná (striktná) konzistencia` – každé čítanie vidí najnovší zápis.

Tieto silnejšie modely však obmedzujú výkon a škálovateľnosť systému.

**Eventual consistency povoľuje dočasné nekonzistencie medzi replikami, ale garantuje, že:**

- ak už nepribúdajú nové zápisy,
- všetky repliky sa časom zosynchronizujú.

**V praxi sa používa preto, že:**

- umožňuje vysokú dostupnosť,
- znižuje latenciu,
- je vhodná pre veľké distribuované systémy (napr. DNS, cloudové databázy).

---

## 13. Majme distribuovaný systém, ktorý podporuje replikáciu objektov, v ktorej sú všetky volania metód úplne usporiadané. Predpokladajme tiež, že vyvolanie objektu je atómické. Poskytuje takýto systém vstupnú (entry) konzistenciu? A čo sekvenčnú konzistenciu?

Ak sú `všetky volania metód úplne usporiadané (total order)`, znamená to, že `všetky procesy vidia volania v rovnakom poradí`. Ak je zároveň vyvolanie objektu `atómické`(napríklad vďaka automatickému uzamknutiu objektu pri volaní metódy), systém `poskytuje sekvenčnú konzistenciu`. Každý proces teda pozoruje rovnakú sekvenciu operácií nad objektmi.

Takýto systém však a`utomaticky neposkytuje vstupnú (entry) konzistenciu`. Entry konzistencia vyžaduje, aby bol prístup ku konkrétnej dátovej položke možný `až po explicitnej synchronizácii viazanej na túto položku (napríklad získaním zámku)`. Samotné úplné usporiadanie volaní metód nestačí – systém by musel explicitne riadiť, ku ktorým dátam sa synchronizácia viaže.

**➡️ Zhrnutie:**

- Sekvenčná konzistencia: ÁNO- 
- Entry konzistencia: NIE (bez dodatočných synchronizačných mechanizmov)

---

## 14. Predpokladajme, že by ste mohli použiť iba neblokujúce asynchrónne komunikačné operácie na posielanie a prijímanie správ. Ako by ste implementovali blokujúce synchronné komunikačné operácie pomocou týchto asynchrónnych operácií?

Blokujúcu synchronnú komunikáciu je možné implementovať nad neblokujúcimi asynchrónnymi operáciami tak, že po odoslaní správy `proces aktívne čaká na odpoveď`.

**Postup je nasledovný:**

1. Proces odošle správu pomocou neblokujúcej operácie send.

2. **Následne opakovane kontroluje, či odpoveď už dorazila, napríklad:**

  - pomocou slučky s neblokujúcim receive,
  - alebo pomocou callbacku, eventu či signalizačného mechanizmu.

3. Proces je zablokovaný až do momentu, keď odpoveď príde.

Z pohľadu aplikácie sa takáto komunikácia správa `ako synchronná`, aj keď je implementovaná pomocou asynchrónnych primitív. Efektívnejšie riešenia využívajú `udalosti alebo callbacky`, aby sa predišlo neefektívnemu aktívnemu čakaniu (polling).

---

## 15. Súbor je replikovaný na 10 serveroch. Vymenujte všetky kombinácie kvóra na čítanie a kvóra na zápis, ktoré povoľuje hlasovací algoritmus replikačného protokolu založeného na hlasovacom kvóre.

**Pri hlasovacom kvórovom replikačnom protokole musia byť splnené tieto podmienky:**

- `NR + NW > N`, aby sa čítanie a zápis vždy prekrývali,
- `NW > N / 2`, aby sa zápisy navzájom prekrývali.

**Pre N = 10 platí:**

- NW > 5 → minimálne NW = 6.

**Možné kombinácie (NR, NW) sú napríklad:**

- (1, 10)
- (2, 9)
- (3, 8)
- (4, 7)
- (5, 6)

**Všetky tieto kombinácie zabezpečujú, že:**

- čítanie vždy získa aspoň jednu aktuálnu repliku,
- zápisy sa nikdy navzájom „neprebijú“.
