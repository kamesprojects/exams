# DSI – Poznámky (MD)

## Vypracované:

- [matej](matej/index.md)
- [kiko](kiko/index.md)

## Otázky:
1. Vysvetlite spôsob šírenia údajov v peer-to-peer systémoch pomocou klebetenia (gossiping). Ako nám tento spôsob môže pomôcť pri objavovaní konkrétnych služieb v neštruktúrovanom peer-to-peer systéme?
2. Popíšte problém dôvery (trust) v distribuovaných systémoch. Vysvetlite útok Sybil a možnosti ochrany voči nemu v decentralizovaných systémoch akými sú napr. blockchain.
3. Škálovateľnosť môže byť dosiahnutá aplikáciou rôznych techník. Uveďte tieto techniky a vysvetlite ich.
4. Načrtnite návrh viacvláknového servera, ktorý podporuje viacero aplikačných protokolov používajúc sockety ako rozhranie transportnej vrstvy nad operačným systémom.
5. Vysvetlite, prečo úplne usporiadaný multicast používajúci Lamportove logické hodiny nie je dobre škálovateľný.
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
16. Konzistenčné modely – ktorý model je najvhodnejší pre emailový systém?
17. Vysvetlite, čo je konsenzus v distribuovaných systémoch a opíšte, čo je protokol Raft.
18. Čo je middleware a aký má zmysel ho používať?
19. Máme synchronný blokujúci model komunikácie. Ako ho spraviť asynchrónnym, pričom synchronné rozhranie má tiež existovať?
20. Je potrebné odpovedať na každú správu pri Lamportovom čase, aby bol dosiahnutý total order multicast? Zdôvodnite.
21. Total ordering multicast – či je potrebné potvrdzovanie správ pomocou acknowledgements. Odpoveď zdôvodnite.
22. Time algorithm to check latency between systems“ – teda algoritmus na kontrolu latencie medzi systémami.
