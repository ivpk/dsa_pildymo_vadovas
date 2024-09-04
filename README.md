# DSA pildymo vadovas

> [!Warning]
> Dokumentas šiuo metu rengiamas

DSA aprašymą galite rasti čia: [Duomanų struktūros aprašas](https://ivpk.github.io/dsa/index.html)

## Bendra DSA struktūra

DSA pildomas lentelės formatu, įprastai Excel lentelėje. [DSA lentelės formatas](https://ivpk.github.io/dsa/formatas.html#lenteles-formatas)

### Dataset

Stambiausias DSA vienetas yra duomenų rinkinys - [Dataset](https://ivpk.github.io/dsa/formatas.html#dataset).

Duomenų rinkinys turi pavadinimą, tipą bei kitą informaciją. [Daugiau apie duomenų rinkinį.](https://ivpk.github.io/dsa/dimensijos.html#dataset)

### Resource

Duomenų rinkinys gali tur4ti vien1 ar kelis resursus. Tai - fizinės duomenų saugojimo vietos, pavyzdžiui, duomenų bazės, aprašymas.

### Modeliai

Kiekvienas duomenų rinkinys gali turėti vieną ar daugiau modelių. Modelis atitinka vieną realaus gyvenimo [objektą](https://ivpk.github.io/dsa/modelis.html#objektas). Tai, pavyzdžiui, gali būti Gyvenvietė.

Kiekvienas modelis turi pavadinimą, taip pat gali turėti aprašymą bei kitą informaciją. Kokią informaciją gali turėti modelis, rasite [čia](https://ivpk.github.io/dsa/dimensijos.html#model)

Modelio pavadinimas įrašomas į stulpelį "model". Jei jis turi unikalų raktą, šio unikalaus rakto pavadinimas rašomas į stulpelį "ref". 

### Savybės (properties)

Savybės yra kiekvieno modelio aprašomosios dalys. Kiekviena savybė aprašo kokį nors objekto požymį. Pavyzdžiui, Gyvenvietė gali turėti pavadinimą, kodą, plotą. Daugiau apie savybes [čia](https://ivpk.github.io/dsa/dimensijos.html#property)

## ŠDSA ir jo skirtumas nuo DSA

ŠDSA turi šaltinio duomenis. Šie duomenys yra svarbūs, kai spintos pagalba norima pasiekti duomenis, aprašytus šiame DSA. 
Pavyzdžiui, jei duomenys laikomi SQL duomenų bazėje, tai `source` aprašys duomenų bazės lenteles (modeliams) bei laukus (savybėmns). Jei tai XML, source bus XPATH, kuriuo gali būti pasiekiamas elementas, atitinkantis modelį ar savybę. 

## DSA pildymas pagal automatiškai sugeneruotą ŠDSA

Naudodamiesi įrankiu `spinta` galim suformuoti pradinį ŠDSA, kurį vėliau papildysim kita, pradiniame šaltinyje nesama informacija, bei, esant poreikiui, pertvarkysim. 

Turėdami duomenų aprašą XSD formatu, mes galim sugeneruoti pirminį ŠDSA tokia `spinta` komanda:

`spinta copy registras.xsd registras_dsa.xlsx` 

Čia `duomenys.xsd` - mūsų duomenų aprašymas XSD formatu, o `dsa.xlsx` - iš jų sugeneruotas pirminis ŠDSA failas.

Turėdami šį pradinį failą, mes galim toliau rankiniu būdu papildyti reikiama informacija, ir, jei yra poreikis, pertvarkyti jame esančius modelius.

### Modelių ir savybių pavadinimai




### Modelių skaidymas esant poreikiui

### Master data ir pasikartojančių modelių aprašymas naudojant `base`

### URI pildymas ir žodynai
