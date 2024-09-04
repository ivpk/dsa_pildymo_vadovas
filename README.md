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

Iš šaltinio sugeneruoti modelių ir savybių pavadinimai gali būti neinformatyvūs, tai gali būti įvairūs trumpiniai ar panašiai. Pavyzdžiui, gali būti "Gyvenv",  "tr_pav". Tokius pavadinimus reikia pakeisti į pilnus žodžius, aiškiai atitinkančius tai, kas tai iš tikro yra. Pavyzdžiui, "Gyvenviete", "trumpas_pavadinimas"

Modelių pavadinimai turi prasidėti didžiąja raide. Jei modelio pavadinimas susideda iš kelių žodžių, visi žodžiai turi prasidėti didžiosiomis raidėmis ir tarp jų neturi būti tarpų. Pavyzdžiui MiestoGatve.

Modelio pavadinimas turi būti vienaskaita. Daugiskaita gali būti naudojama tik išskirtiniais atvejais, kai žodis neturi vienaskaitos, pavyzdžiui "Pajamos".

Savybių pavadinimai turi būti mažosiomis raidėmis. Jei savybė susideda iš kelių žodžių, jie atkiriami pabraukimu, pavyzdžiui "miesto_gatve".

Savybių pavadinimai rašomi vienaskaita, išskyrus šiuos atvejus:

- kai žodis neturi vienaskaitos, pavyzdžiui "pajamos"
- kai savybė nurodo masyvą. Tokiu atveju savybės prie savybės bus pridedami ir laužtiniai skliaustai, kurie ir pažymi, kad tai masyvas: `[]`. Pavyzdys: "pastatai[]".


### Modelių skaidymas esant poreikiui

Kartais šaltinyje duomenys gali būti denormalizuoti. Pavyzdžiui, pastato duomenys ir jo savininko duomenys gali būti laikomi toje pačioje lentelėje (ar kitoje duomenų struktūroje). Tokiais atvejais, automatiniu būdu sugeneravus ŠDSA, kai kuriuos modelius reikia išskaidyti į atskirus. 

Pavyzdys:

Pastatas
  adresas
  plotas
  spalva
  sklypo_plotas
  sklypo_numeris
  patalpu_skaicius
  savininko_vardas
  savininko_pavarde
  savininko_a_k

Kaip matom, šiuo atveju čia iš tikro aprašomi trys dalykai: pastatas, sklyoas ir savininkas. Tokiu būdu reikėtų šį modelį išskaidyti į tris modelius:

Pastatas
  - adresas
  - plotas
  - spalva
  - patalpu_skaicius
  - savininkas
  - savininkas.vardas
  - savininkas.pavarde
  - savininkas.asmens_kodas
  - sklypas
  - sklypas.plotas
  - sklypas.numeris

Sklypas
  - plotas
  - numeris

Savininkas
  - vardas
  - pavarde
  - asmens_kodas


### Master data ir pasikartojančių modelių aprašymas naudojant `base`

Vienas objektas (esybė) įvairiai būna aprašomas skirtingose sistemose. Bet siekiant unifikuoti Valstybės duomenų aprašymus, kiekvienas objektas turi turėti vieną pagrindinį aprašymą, kuris būtų naudojamas kitur. Pavyzdžiui, Asmuo, JuridinisAsmuo, Pastatas, TeisėsAktas, Igaliojimas ir pan.

Šiuo atveju, pavyzdžiui, Asmuo yra aprašomas Gyventojų registre, ir tai yra pirminis jo aprašymas. Bet, pavyzdžiui, Neklinojamojo turto registre gali būti aprašomas nekilnojamojo turto savininkas, kuris taip pat bus asmuo

Šiuo atveju prie Nekilnojamojo turto registre esančio modelio Savininkas turėtų būti nurodoma `base` Asmuo`. 

Pastatas
  - adresas
  - plotas
  - spalva
  - patalpu_skaicius
  - savininkas
  - savininkas.vardas
  - savininkas.pavarde
  - savininkas.asmens_kodas
  - sklypas
  - sklypas.plotas
  - sklypas.numeris

Sklypas
  - plotas
  - numeris

\gyventoju_registras\Asmuo
Savininkas
  - vardas
  - pavarde
  - asmens_kodas


### URI pildymas ir žodynai
