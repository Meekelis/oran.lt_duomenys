ORAN JSON DUOMENŲ GIDAS
=======================

Perskaitykite šį trumpą gidą nuosekliai, kadangi informacija apie vieną iš bylų gali būti pritaikoma kitoms. ORAN duomenys nėra skirti pradedaniesiems arba galiniam vartotojui (nors, žinoma, mes neturime prieštaravimų bet kokiam jų naudojimui). Duomenis integruojant savo projekte Jums reiks pasikliauti sveika nuožiūra, geru geografinių duomenų ir minimaliu JSON technologijos suvokimu. Jeigu perskaitę šį gidą vis dar turite klausimų, galite atidaryti "issue" viršuje, tačiau klausimai aptarti šiame gide nebus papildomai atsakomi.

Šioje repozitorijoje rasite penkias bylas:
- `db.geo.json` (duomenų bazė, kurią ORAN naudojo sistemos viduje. Šioje byloje koordinatės yra pateikiamos taip, kaip jos atrodo LR. teisės aktuose);
- `data.js` (ypač suspausta duomenų bazė, kuri buvo perduodama ORAN klientams, kai jie apsilankydavo svetainėje. Šie duomenys buvo dinamiškai iššifruojami naršyklės pagal poreikį. Jie vis dar naudoja unikalų ORAN formatą, tačiau mūsų sistema kompiliuojant juos jau ištaisė tam tikras klaidas, esančias teisės aktuose, naudojant automatines heuristikas);
- `db.geo.wgs84_compiled.json` (ši duomenų bazė yra pagaminta specialiai trečiųjų šalių naudojimui. Joje duomenys yra savaime suprantami ir atitinka WGS84 Lat Long DD standartą);
- `LICENSE` (duomenų naudojimo licenzija);
- `README.MD` (šis dokumentas).

## db.geo.json
Šioje byloje didelė dalis duomenų yra pateikiami tekstiniu formatu, kadangi tai yra duomenys nukopijuoti iš LR. teisės aktų. Čia sutiksite atstumus kilometrais, metrais, ir jūrmylėmis. Koordinatės bus pateiktos įvairiais formatais, ir kartais ilguma ir platuma bus sukeistos vietomis. LR kariuomenė kai kuriuose savo dokumentuose naudojo koordinačių notaciją, kuri nėra standartinė. ORAN sistema buvo sukurta interpretuoti visus šiuos duomenų tipus, bet Jums nerekomenduojame bandyti duomenų interpretuoti patiems. Vietoje to, naudokite vieną iš sekančių bylų. Ši čia yra tik todėl, kad galėtumėte patikrinti ir detaliau išstudijuoti neaiškias reikšmes kituose duomenų bazės pateikimuose.

## data.js
Ši byla yra sunkiausiai iššifruojama. Tačiau, jei pageidaujate iššifruoti koordinates joje, kiekvieną koordinatės sveikąjį skaičių reikia padalinti iš 100 000 (šimto tūkstančių) ir pridėti prie žemėlapio centro „floor“ funkcijos rezultato. Pavyzdžiui, koordinatė [68583,351302] nurodytų tašką [55+0.68583,23+3.51302] WGS84 Lat Lng Decimal Degrees sistemoje.

`data.js` byloje dalis dažnai pasikartojančių tekstų taip pat yra pakeistos vietažymėmis (panašu į žodyninę kompresiją). Vietažymės yra matomos `"prefabs"` JSON skirsnyje. 

Nerekomenduojame pradėti naudoti šių duomenų, tačiau jie yra tie duomenys, kurie paskelbimo metu buvo naudojami oran.lt. Jeigu kitose bylose egzistuoja kokia nors klaida, tuomet verta patikrinti duomenis `data.js`. Galbūt čia šios klaidos nebus.

## db.geo.wgs84_compiled.json
Šioje byloje koordinatės yra pateiktos WGS84 Lat Lng Decimal Degrees sistemoje. Jų niekaip perskaičiuoti nereikia. Taip pat, šioje byloje vietų aprašai pateikti be žodyninės kompresijos aplikacijos ir UTF-8 rašmenimis. Kitaip tariant, šią duomenų bazę turėtumėte galėti panaudoti lengvai.

Kai kurie vietų parametrai gali būti savaime neaiškūs, pavyzdžiui `"rank"`. Šis parametras nurodo objektų svarbą, kur objektai su verte 1 yra svarbiausi, o turintys didesnes reikšmes - mažiau svarbūs. Iš tiesų, ši reikšmė yra suskaičiuota pagal perimetrą. Jos paskirtis žemėlapio piešimo metu yra išdėstyti mažesnius elementus ant didesnių, kad visi būtų pasiekiami be "click-through" aplikacijų. Kitas nebūtinai iš karto aiškus parametras yra `"radius"`. Jis nurodo apskritimų spindulį *metrais*. Tačiau šie metrai yra pritaikyti `Leaflet JS` žemėlapio atvaizdavimo priemonei, kuri savaip susitvarko su žemės gaublio projekcijos iškreipimais ("Projection Distortion") ir gali neatitikti Jūsų projekcijos nuokrypių apskaičiavimo sprendimo. Jeigu pageidautumėte apskritimų spindulio duomenų tiesiai iš teisės aktų (jie bus pateikti metrais, kilometrais arba jūrmylėmis), tuomet originalų formatą galite rasti byloje `db.geo.json`.

## Duomenų licenzija
Visus duomenis atiduodame CC0 licenzijos pagrindu - https://creativecommons.org/publicdomain/zero/1.0/. Kitaip tariant, galite naudoti, kaip pageidaujate. Ir mes nereikalaujame nurodyti jų šaltinio.

## Duomenų tikslumas
ORAN duomenų bazėse `data.js` ir `db.geo.wgs84_compiled.json` toleruojamas reprezentuojamų duomenų tikslumo nuokrypis - iki 50cm.

Garantijos duomenų tikslumui neduodame, ir netgi pranešame, kad jie yra šiek tiek pasenę. Konkrečiai, naujausias ANS oro erdvės atvaizdavimo modelis (https://www.ans.lt/lt/oni/oro-erdvs-atvaizdavimo-modelis/) į duomenis nėra integruotas. 

Ačiū,
Kazimieras
