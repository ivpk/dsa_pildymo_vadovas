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


## ŠDSA ir jo skirtumas nuo DSA
ŠDSA turi šaltinio duomenis. Šie duomenys yra esminiai, kai spintos pagalba norima pasiekti duomenis, aprašytus šiame DSA. 

## DSA pildymas pagal automatiškai sugeneruotą ŠDSA

## URI pildymas ir žodynai
