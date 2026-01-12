# PGI

Prehľad predmetu PGI.

- [Poznámky (<file>.md)](md/index.md)
- [PDF](pdf/index.md)

# Otázky z PGI 2025 skúška

---

## Priestor, svetlo a farby:

---

1. Používanie a spracovanie farieb v rámci počítačovej grafiky, základné atribúty svetla, farebný priestor, gamut
2. Chromatický diagram, typy, odtieň a saturácia
3. Farebné modely RGB a RGBA.
4. Farebné modely CMY a CMYK.
5. Farebný model HSB.
6. Farebný model HLS.
7. Gama korekcia a alfa-miešanie.
8. Problematika ľudského vizuálneho vnemu a jeho spracovania v relácii s počítačovou grafikou.
9. Miešania a rozptyľovania farieb (prevod do šedej škály, halftoning, dithering) v rámci počítačovej grafiky.
10. Ergonómia a symbolika farieb, použitie farieb v počítačovej grafike.
11. Dimenzia priestoru a dimenzia objektu, štruktúra dimenzie.
12. Priestor a jeho súradnicová sústava, stupeň voľnosti
13. Vrstvy vizualizačného procesu.

---

## Grafická informácia a jej spracovanie

---

14. Grafická informácia po objektovej aj typovej stránke.
15. Základné 2D grafické primitíva a ich atribúty.
16. Spracovanie bodu a sledu bodov v rámci počítačovej grafiky,
17. DDA algoritmus.
18. Bresenhamov algoritmus.
19. Spracovanie kružnice a elipsy v rámci počítačovej grafiky a základné metódy ich generovania.
20. Antialiasing.
21. Filtrovacie a rozptyľovacie metódy, medián filter, poltónovanie, dithering, distribúcia chyby pri
rozptyľovaní.

---

## Grafický priestor a objekty

---

22. Popis a reprezentácia objektov v počítačovej grafike, priestor a jeho parametre.
23. Hraničná reprezentácia.
24. Konštruktívna geometria telies.
25. Súradnicová sústava priestoru, súradnicové sústavy používané v počítačovej grafike, súradnicový reťazec.

---

## Transformácie v počítačovej grafike

---

26. Transformácie a transformačné zobrazovacie reťazce v rámci počítačovej grafiky.
27. Transformácie v rámci zobrazovacích reťazcov (medzisústavové transformácie)), transformačné matice a
homogénne súradnice, afinné transformácie.
28. Transformácia zrkadlenia.
29. Transformácia posunutia.
30. Transformácia zmeny mierky, zväčšenie/zmenšenie rastrového objektu
31. Transformácia skosenia, skosenie rastrového objektu
32. Transformácia otočenia
33. Otáčanie okolo všeobecnej priamky využitím Eulerových uhlov, gimbal lock, quaternióny
34. Transformácia otočenia rastrového objektu
35. Morphing, warping

---

## Projekčné a zobrazovacie transformácie

---

36. 2D premietacie transformácie používané v počítačovej grafike, logická a fyzická pracovná oblasť, otáčanie
kamery na báze Eulerových uhlov.
37. Orezávacie algoritmy, Cohen-Sutherlandovho algoritmu.
38. Kolmá (ortografická) projekcia, Mongeova projekcia
39. Axonometria.
2
40. Perspektíva.
41. Nelineárne premietacie transformácie, distorzia obrazu, rybie oko.

---

## Krivky a plochy v počítačovej grafike

---

42. Krivky používané v počítačovej grafike, spôsob využitia, 1D krivkové útvary.
43. Fergusonova krivku.
44. Bézierove krivky.
45. Spline, Catmul-Rom spline a B-spline krivka.
46. NURBS krivky.
47. Plochy používané v počítačovej grafike, 2D plošné útvary, modifikovateľnosť plôch.
48. Coonsovu bilineárna plochu.
49. Bézierová bikubická plocha.

---

## Riešenie viditeľnosti v počítačovej grafike

---

50. Problém riešenia viditeľnosti a jeho kategorizácia v rámci počítačovej grafiky.
51. Algoritmu plávajúceho horizontu.
52. Maliarov algoritmus riešenia viditeľnosti.
53. Freeman-Lotrelov algoritmus riešenia viditeľnosti.
54. Algoritmus pamäte hĺbky (Z-buffer).
55. Metóda BSP stromov pri riešení viditeľnosti v rámci počítačovej grafiky, tvorba a prechod BSP stromom.
56. Metóda oktantových stromov pri riešení viditeľnosti v rámci počítačovej grafiky.
57. Urýchľovacie metódy pre riešenie viditeľnosti v počítačovej grafike, FV (BC) algoritmus
58. Orezávania na zorný ihlan pri riešení viditeľnosti v rámci počítačovej grafiky.
59. Ohraničujúce objekty, sektorovanie a potenciál viditeľnosti pri urýchľovaní riešenia viditeľnosti v rámci
počítačovej grafiky.
60. S-buffer pri riešení viditeľnosti v počítačovej grafike.

---

## Vyplňovanie oblastí a textúrovanie

---

61. Vyplňovanie oblastí používané v počítačovej grafike.
62. Algoritmus riadkového rozkladu pri vyplňovaní oblastí.
63. Vyplňovanie spektrom.
64. Inverzné a plotové vyplňovanie.
65. Rekurzívne aj nerekurzívne semienkové vyplňovanie.
66. Textúrovanie a jeho vzťah k zobrazovacím reťazcom
67. Bilineárne textúrovanie, bump-map textúrovací procees a technológia „pečenia“ textúr.
68. LOD technológie v rámci počítačovej grafiky.

---

## Tieňovanie, osvetľovanie a fotorealistické zobrazovanie

---

69. Konštantné (flat) tieňovanie v rámci počítačovej grafiky.
70. Tieňovanie interpoláciou farby (Gourard) v rámci počítačovej grafiky.
71. Tieňovanie interpoláciou normály (Phong) v rámci počítačovej grafiky.
72. Osvetľovanie a osvetľovacie modely, svetelné zdroje
73. Lambertov osvetľovací model
74. Phongov osvetľovací model.
75. Osvetľovacie mapy a zrkadlá
76. Realistické zobrazovanie a globálne osvetľovacie techniky v rámci počítačovej grafiky, metódy vychádzajúce
od pozorovateľa a od svetelného zdroja.
77. Algoritmy fotorealistických metód a metóda raytracing.

---

## Fraktály, časticové systémy, virtuálna realita a XR

---

78. Fraktály a časticové systémy.
79. Virtuálna realita, základné pojmy, kategorizácia, podsystémy VR systémov.
80. XR (eXtended Reality) a jej zložky, kolaboratívna VR, systémy interakcie a používateľské rozhrania na báze
XR.
