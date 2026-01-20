# DSI – Poznámky (MD)/kiko

## Otázky:

11. Vysvetlite koncept spoľahlivej skupinovej komunikácie medzi replikovanými procesmi a možnosti jej škálovania. Popíšte fungovanie atómovej skupinovej komunikácie.
12. Vysvetlite problém konzistencie zameranej na údaje v distribuovanom systéme a uveďte konkrétne konzistenčné modely založené na usporadúvaní operácií. Aký je význam použitia modelu konečnej konzistencie (eventual consistency model) v praktických aplikáciách na rozdiel od silnejších modelov?
13. Majme distribuovaný systém, ktorý podporuje replikáciu objektov, v ktorej sú všetky volania metód úplne usporiadané. Predpokladajme tiež, že vyvolanie objektu je atómické. Poskytuje takýto systém vstupnú (entry) konzistenciu? A čo sekvenčnú konzistenciu?
14. Predpokladajme, že by ste mohli použiť iba neblokujúce asynchrónne komunikačné operácie na posielanie a prijímanie správ. Ako by ste implementovali blokujúce synchronné komunikačné operácie pomocou týchto asynchrónnych operácií?
15. Súbor je replikovaný na 10 serveroch. Vymenujte všetky kombinácie kvóra na čítanie a kvóra na zápis, ktoré povoľuje hlasovací algoritmus replikačného protokolu založeného na hlasovacom kvóre.

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

**1. Sekvenčná konzistencia: ÁNO**

Tento systém poskytuje sekvenčnú konzistenciu.

**Zdôvodnenie:**

- `Úplné usporiadanie:` Všetky uzly (repliky) vidia všetky volania metód (operácie zápisu aj čítania) v rovnakom poradí. 

- `Zachovanie lokálneho poradia:` Keďže ide o volania metód v distribuovanom systéme s úplným usporiadaním, operácie od jedného konkrétneho klienta sú do tohto globálneho poradia zaradené v poradí, v akom ich klient vydal.

**Splnenie definície:**

- Ak všetci vidia rovnaké globálne poradie a toto poradie rešpektuje lokálne poradie každého procesora, je definícia sekvenčnej konzistencie naplnená.

**2. Vstupná konzistencia (Entry Consistency):** ÁNO

Tento systém poskytuje (a v podstate prekračuje) vstupnú konzistenciu.

**Zdôvodnenie:**

- `Viazanie na zámky:` Vstupná konzistencia vyžaduje, aby boli dáta (objekt) konzistentné v momente, keď uzol získa zámok (lock) k tomuto objektu.

- `Automatické uzamykanie:` Tvoj systém garantuje, že každý objekt je pri volaní metódy automaticky uzamknutý. 

To znamená, že žiadne dve metódy nemôžu bežať naraz nad tým istým objektom (serializácia).

**Synchronizácia pred prístupom:** 

Keďže volania sú úplne usporiadané, pred vykonaním metódy nad uzamknutým objektom musí systém zabezpečiť, že tento objekt obsahuje všetky predchádzajúce zmeny z globálneho poradia. Porovnanie a jemný rozdielHoci systém poskytuje obidve, je dôležité vidieť rozdiel v ich "prísnosti":

- `Sekvenčná:` Vyžaduje, aby sme sa všetci zhodli na poradí operácií nad všetkými objektmi.
- `Vstupná:` Vyžaduje konzistenciu len pre konkrétny objekt, ku ktorému práve pristupujeme (máme zámok).

**Záver:** 

Keďže tvoj systém používa úplné usporiadanie (globálna zhoda na všetkom), poskytuje oveľa silnejšiu záruku, než by vstupná konzistencia striktne vyžadovala. Vstupná konzistencia je tu "zadarmo" vďaka tomu, že každé volanie metódy je atomické a chránené zámkom.

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
