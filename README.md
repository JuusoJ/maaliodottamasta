# Maaliodottama kulmasta käsin

Interaktiivinen simulaattori ja blogikirjoitus, joka rakentaa jalkapallon maaliodottaman (xG) fysiikasta: kulmasta, pallon lentoajasta, maalivahdin ulottuvuudesta, puolustajien varjoista ja sattumasta. Malli on sovitettu 38 318 oikeaan laukaukseen (StatsBomb Open Data, kausi 2015/16). Se selittää dataa lähes yhtä hyvin kuin StatsBombin oma koneoppimismalli, mutta jokainen sen luku tarkoittaa jotain fysikaalista.

Vaativimmat käsitteet on selitetty kohdassa [11. Käsitteet](#11-käsitteet).

---

## 1. Mikä tämä on

Tavallinen xG kertoo, kuinka usein samasta paikasta ammuttu laukaus menee keskimäärin sisään. Keskiarvo kätkee yksilöt: sama veto on eri asia Rayaa kuin divarijoukkueen varamaalivahtia vastaan.

Projekti on mallinrakennusharjoitus teoreettisen fysiikan hengessä:

1. rakennetaan mekanismi (pallo lentää, maalivahti reagoi ja syöksyy, puolustaja peittää)
2. sovitetaan muutama vakio dataan
3. katsotaan, mitä malli ennustaa ja mitä se jättää selittämättä.

Sivulla on kolme tasoa: data ruudukkona, yksinkertainen perusfunktio ja fysikaalinen malli simulaattorina.

## 2. Tiedostot ja käyttö

| Tiedosto | Sisältö |
|---|---|
| `index.html` | Koko sivu: teksti, simulaattori, malli ja ruudukon data yhdessä tiedostossa |
| `README.md` | Tämä ohje |

Sivu toimii avaamalla `index.html` selaimessa. Asennuksia tai käännösvaihetta ei tarvita. Fontit ladataan Google Fontsista, mutta sivu toimii ilmankin.

**GitHub Pages:** vie tiedostot repositorioon ja valitse *Settings → Pages → Deploy from a branch → main / (root)*.

**Muuta ennen julkaisua** (hae tiedostosta hakusanalla):

- `KAYTTAJANIMI`: oma Buy Me a Coffee -osoite
- `TUKIJASEINA`: tukijaseinän osoite
- `VASTIKE`: teksti siitä, mitä ostaja todella saa (katso kohta *Tukeminen ja laki* alempana)
- `Kirjoittaja`: nimesi otsikon alla.

**Simulaattorin käyttö**

- Vedä tai napauta palloa. Kartta näyttää maaliodottaman jokaisesta laukaisupisteestä.
- Vedä maalivahtia tai punaisia puolustajia. Silloin ne jäävät paikoilleen. *Automaattiset* palauttaa maalivahdin parhaaseen paikkaan ja puolustajat oletusmuodostelmaan.
- Pelaajapainikkeet asettavat laukojan ja maalivahdin arvot. Arvot ovat havainnollistavia arvioita, eivät mittauksia.
- *Näytä ero keskitasoon* värittää kartan erotuksena keskitasosta. *Esimerkkitilanne* palauttaa kirjoituksen lopun esimerkin.
- Syvyyskäyrä näyttää, miten maaliodottama muuttuu maalivahdin etäisyyden mukana. Käyrää napauttamalla maalivahti siirtyy.

## 3. Data

StatsBombin avoimessa aineistossa ovat kauden 2015/16 Valioliiga, La Liga ja Serie A kokonaan, Ligue 1 lähes kokonaan (377 ottelua) sekä 34 Bundesliga-ottelua. Laukauksia on 38 318 ilman rangaistuspotkuja, ja niistä 3 651 eli 9,5 % päätyi maaliin. Rangaistuspotkuja on 410, ja niistä 75,1 % meni sisään.

Jokaisesta laukauksesta tunnetaan paikka, lopputulos, laukaisutapa (jalka, pusku, volley, suoraan syötöstä), pelitilanne, paine kyllä tai ei -tietona sekä **tilannekuva** (*freeze frame*). Tilannekuvassa näkyvät laukaisuhetken pelaajien paikat. Niistä on poimittu maalivahdin paikka ja kaikki puolustajat, jotka ovat laukauksen kolmiossa tai alle 2,5 metrin päässä siitä. Tällaisia puolustajia on keskimäärin 2,3 laukausta kohden.

Sivun ruudukossa vasemman ja oikean puolen peilikuvaruudut on yhdistetty laukausmäärillä painottaen, koska maali on symmetrinen.

StatsBomb edellyttää, että aineisto mainitaan lähteenä. Tarkista ajantasaiset käyttöehdot [aineiston sivulta](https://github.com/statsbomb/open-data).

## 4. Perusfunktio

Yksinkertaisin hyvä malli on logistinen regressio kulmasta θ ja etäisyydestä *d*:

```
xG₀ = p∞ + (1 − p∞) · Φ((R − d) / 5 m) / (1 + e^−(−1,687 + 1,216·θ − 0,0862·d))
```

Kolme lukua eksponentissa toistavat ruudukon suuret linjat. Kantamatermi (*R* = 54 m) sammuttaa hännän sieltä, mistä dataa ei ole. Pohja *p*∞ = 0,0005 on asetettu käsin, jotta todennäköisyys ei koskaan putoa nollaan. Perusfunktio ei tiedä mitään pelaajista eikä puolustajista.

## 5. Fysikaalinen malli

```
xG = p₀ + (1 − p₀) · max(P_laukaus, P_vippaus)
```

Maaliin on kolme reittiä: sattuma *p*₀, laukaus maalivahdin ja puolustajien ohi tai vippaus maalivahdin yli. Merkinnät: alaindeksi *p* on laukoja, *k* maalivahti ja *d* puolustaja.

**5.1 Kulma.** `θ = atan2(w·x, x² + y² − (w/2)²)`. Kehäkulmalauseen takia samanarvoiset vyöhykkeet ovat kaaria tolpalta tolpalle.

**5.2 Aika ja ulottuvuus.** `t_f = (L/v₀)(e^(s/L) − 1)`, `Δt = t_f − t_k`, `R = r₀ + v_k·Δt`. Ilmanvastus (vaimennusmatka *L* = 80 m) pidentää lentoaikaa. Maalivahti reagoi ajassa *t*_k ja syöksyy sen jälkeen nopeudella *v*_k. Laukojan silmin hän peittää kulman ±arctan(*R*/*s*).

**5.3 Torjunnan pettäminen.** `ε = ε_max · e^(−m/τ)`. Palloon ehtiminen ei ole torjunta: mitä pienempi aikamarginaali *m*, sitä useammin torjunta pettää. Lähellä maaliviivaa osittainen torjunta jatkaa helpommin maaliin, ja ulos tulleen maalivahdin ohi pääsee läheltä myös jalkojen välistä.

**5.4 Puolustajien varjot.** `α_d = arctan(r_d / s_d)`. Jokainen puolustaja peittää laukojan silmin kulmavälin, josta hän pysäyttää osuuden *q*_d. Lähellä oleva puolustaja peittää suuren kulman, ja laukoja tähtää varjojen ohi.

**5.5 Tähtäys ja hajonta.** `P_laukaus = V · Σᵢ εᵢ · [Φ((bᵢ − μ)/σ_tot) − Φ((aᵢ − μ)/σ_tot)]`. Maalin näkökulma jakautuu väleihin: vapaa maali, maalivahdin vyöhykkeet ja puolustajien varjot. Laukoja valitsee suunnan μ, joka tekee summasta suurimman. Toteutunut suunta vaihtelee normaalijakauman mukaan (suuntahajonta σ_p), ja *V* on todennäköisyys pysyä riman alla.

**5.6 Vippaus (lob).** Pallo nostetaan kaarella ulos tulleen maalivahdin yli. Vippaus onnistuu, jos maalivahti ei ehdi perääntyä viivalle ennen kuin pallo putoaa. Kierrettä malli ei tunne.

**5.7 Tyhjä maali, laukauksen kolmio ja käsisääntö.** `P_laukaus = w·P_maalivahti + (1 − w)·P_tyhjä`, `w = max(0, 1 − s⊥/4 m)`. Maalivahdin vaikutus hiipuu neljän metrin matkalla laukauksen kolmion ulkopuolella ja katoaa pallon takana. Yli puoli metriä rangaistusalueen ulkopuolella maalivahti on kenttäpelaaja ilman käsiä.

**5.8 Sattuma ja kantama.** `p₀ = 0,055 · e^(−d/12 m) · e^(−(Δy/15 m)²) · Φ((R_max − d)/5 m)`, `R_max = L·ln(1 + (0,85·v_p)²/(gL))`. Kimmokkeet ja virheet antavat pienen pohjan, joka on suurin maalin edessä. Kantama katkaisee kaukaiset vedot: keskitasoisella laukojalla (28 m/s) se on 43 m.

**Tilannevalinnat** kytkeytyvät samoihin suureisiin. Esimerkiksi pusku kasvattaa hajontaa, hidastaa palloa ja lyhentää kantaman 13,9 metriin. Vapaapotku poistaa puolustajat vetolinjalta mutta lisää muurin. Paine siirtää ensimmäistä puolustajaa lähemmäs laukojaa.

## 6. Sovitus ja arviointi

Vakiot on sovitettu **suurimman uskottavuuden menetelmällä**. Jokaiselle laukaukselle lasketaan mallin todennäköisyys oikeilla maalivahdin ja puolustajien paikoilla, ja vakiot valitaan niin, että toteutuneet maalit ja ohilaukaukset ovat mahdollisimman todennäköisiä. Optimointiin käytettiin Nelder–Mead-menetelmää, ja vakiot pidettiin fysikaalisissa rajoissa logit-muunnoksella.

| Sovitettu vakio | Arvo | Merkitys |
|---|---|---|
| ε_max | 0,457 | torjunnan pettämisen yläraja (keskitasolla 0,36) |
| P0 | 0,055 | sattumien taso maalin edessä |
| P0L | 12 m | sattumien vaimenemismatka |
| puskun hajonta | × 2,52 | puskun suuntahajonta suhteessa jalkaan |
| puskun kantama | 13,9 m | kuinka kauas pusku kantaa |
| tyhjän maalin hajonta | × 0,84 | rauhallinen sijoitus tyhjään maaliin |
| r_d | 0,63 m | puolustajan varjon puolileveys |
| q_d | 0,74 | blokin varmuus varjossa |
| ohitus läheltä | 0,99 | ulos tulleen maalivahdin läpimeno (sallitun välin rajalla) |
| vapaapotkun hajonta | × 0,42 | vapaapotkun tarkkuus |

Käsin on asetettu keskitasoisen laukojan arvot (σ_p = 21°, *v*_p = 28 m/s, sijoitusäly 0,35) ja torjunnan aikavakio τ = 1,0 s. Data ei erottele niitä muista vakioista (katso *degeneraatio* kohdassa 11). Reaktioaika, syöksynopeus, rimaehto ja ilmanvastus ovat fysikaalisia arvioita. Rangaistuspotkun hajonta on kalibroitu niin, että xG on 0,75.

**Arviointi logaritmisella häviöllä.** Parannus kertoo, kuinka paljon malli pienentää häviötä verrattuna siihen, että jokainen laukaus saa arvon 0,095.

| Malli | Parannus |
|---|---|
| Etäisyys | 10,9 % |
| Kulma | 10,4 % |
| Perusfunktio | 11,8 % |
| Simulaattori, pelkkä paikka ja laukaisutapa | 11,4 % |
| Simulaattori, todelliset maalivahdin ja puolustajien paikat | 20,8 % |
| StatsBombin xG | 21,0 % |

**Kalibrointi ryhmittäin** (toteutunut / malli):

| Ryhmä | Toteutunut | Malli |
|---|---|---|
| Puskut | 10,7 % | 10,6 % |
| Vapaapotkut | 6,4 % | 6,6 % |
| Volleyt | 10,5 % | 10,7 % |
| 16,5–22 m | 4,8 % | 4,6 % |
| Ei puolustajia lähellä | 26,4 % | 23,5 % |
| 2 puolustajaa | 6,6 % | 7,0 % |

## 7. Keskeiset tulokset

- **Paine on efektiivinen parametri.** Ilman puolustajien paikkoja paine kasvattaa laukojan hajontaa selvästi. Kun paikat ovat mukana, paineen oma vaikutus putoaa nollaan: paine on käytännössä lähellä oleva puolustaja.
- **Puolustaja on 1,3 metrin varjo**, joka pysäyttää kolme neljästä siihen osuvasta laukauksesta. Rangaistusalueen rajalta keskeltä veto on ilman puolustajia 0,090 ja yhden puolustajan kanssa 0,049.
- **Paras maalivahdin paikka on 0,7–1,0 metriä viivan edessä** keskeltä ammuttuja 11–16,5 metrin vetoja vastaan. Kauempaa ammuttua vetoa vastaan kannattaa tulla pidemmälle.
- **Yksilöt ratkaisevat.** Samasta paikasta veto on Rayaa vastaan 0,042 ja divarin varamaalivahtia vastaan 0,082.
- **Tyhjä maali ei ole varma.** Datassa 55 % laukauksista, joissa maalivahti oli yli kolme metriä pallon takana, meni sisään.
- **Kaukolaukauksista puolet on mallissa sattumaa.** 25 metristä 0,007 kokonaisarvosta 0,015 tulee sattumien pohjasta.
- **Hyvä sovitus ei todista mekanismia.** Tarkempi laukoja ja vuotavampi maalivahti selittävät samat maalit lähes yhtä hyvin.

## 8. Rajoitukset

- Malli arvioitiin samalla datalla, johon se sovitettiin, ja data on yhdeltä kaudelta.
- Maali on yksiulotteinen: korkeus näkyy vain rimaehtona, vippauksena ja sylivälin vaikutuksena.
- Puolustajat ovat samanlevyisiä kiekkoja, jotka eivät liiku. Paine on datassa pelkkä kyllä tai ei -tieto.
- Osa termeistä on muodoltaan arvauksia: vippaus, maaliviivan läpimeno ja ohitus läheltä. Ohituksen kerroin asettui sallitun välin rajalle, mikä viittaa puuttuvaan rakenteeseen.
- Pelaajaprofiilit, henkinen paine, maalivahdin häirintä ja syötön tyyppi ovat arvioita ilman dataa.
- Kartan maalivahti on aina optimaalinen ja puolustaja suoraan vetolinjalla, joten kartan luvut ovat alarajoja.

## 9. Mitä mallin rakentamisesta opittiin

1. **Käsin viritetty malli oli kaksi kertaa liian optimistinen.** Ensimmäinen versio antoi keskimäärin 0,17, kun data antaa 0,095. Sovitus dataan on välttämätön, vaikka mekanismi tuntuisi oikealta.
2. **Vapaasti sovitetut vakiot karkaavat epäfysikaalisiin arvoihin.** Osa vakioista kannattaa lukita fysikaalisiin arvioihin ja sovittaa vain ne, joista data todella kertoo.
3. **Data kumosi intuitioita.** Tyhjä maali rangaistusalueen rajalta ei ole 0,75, eikä jalkoihin sukeltava maalivahti romahduta todennäköisyyttä nollaan.
4. **Uusi tieto voi poistaa vanhan selittäjän.** Paineen katoaminen puolustajien paikkojen myötä on mallin kiinnostavin löytö.
5. **Epäfysikaalisuudet kannattaa kirjata näkyviin.** Ne ovat seuraavan version tehtävälista.

## 10. Harjoitustehtävät

Tehtävät vievät mallia kohti tutkimustasoa. Jokaisessa on tavoite, toimenpide ja mittari, jolla onnistumista arvioidaan.

1. **Erillinen testiaineisto.** Sovita malli kolmeen sarjaan ja testaa neljännellä, tai käytä ristiinvalidointia. Jaa aineisto otteluittain, ei laukauksittain, koska saman ottelun laukaukset riippuvat toisistaan. *Mittari:* testiaineiston parannus verrattuna 20,8 %:iin.
2. **Epävarmuus näkyviin.** Arvo otteluita takaisinpoiminnalla (bootstrap) ja sovita malli uudelleen satoja kertoja. Anna jokaiselle vakiolle ja parannukselle 95 %:n luottamusväli. Piirrä häviö aikavakion τ funktiona (profiiliuskottavuus). *Mittari:* kuinka leveitä välit ovat ja mitkä vakiot data todella määrää.
3. **Kalibrointi ja jäännöskartta.** Piirrä luotettavuuskäyrä: jaa laukaukset kymmeneen ryhmään ennusteen mukaan ja vertaa ennustetta toteutuneeseen. Laske jokaiseen ruutuun standardoitu jäännös (havaittu − malli) / √(n·p·(1 − p)). *Mittari:* missä ruuduissa jäännös on yli 2, eli missä fysiikka puuttuu.
4. **Kaksiulotteinen maali.** StatsBombin aineistossa on laukauksen loppupiste korkeuksineen. Sovita suuntahajonta erikseen vaaka- ja pystysuunnassa ja korvaa rimaehto *V* todellisella korkeusjakaumalla. *Mittari:* paraneeko häviö, ja pieneneekö ylärajalle asettuneen ohitustermin tarve?
5. **Pelaajakohtaiset arvot.** Kerää useampi kausi ja sovita jokaiselle laukojalle oma σ_p hierarkkisella bayesiläisellä mallilla, joka kutistaa vähäisten havaintojen arvot kohti keskiarvoa. *Mittari:* kuinka monta laukausta tarvitaan, jotta huippulaukojan hajonta erottuu keskitasosta, ja vastaavatko sivun pelaajaprofiilit dataa?
6. **Maalivahtien torjuntakyky.** Sovita ε_max maalivahtikohtaisesti niistä laukauksista, jotka menivät kohti maalia. Vertaa laukauksen jälkeiseen xG:hen (*post-shot xG*). *Mittari:* toistuuko maalivahdin ero kaudesta toiseen, vai onko se satunnaisvaihtelua?
7. **Kimmokemalli sattuman tilalle.** Mallinna, kuinka suuri osa puolustajan varjoon osuneista laukauksista kimpoaa maaliin. Käytä StatsBombin blokkausmerkintöjä. *Mittari:* pieneneekö sattumien pohja *p*₀, ja saavatko kaukolaukaukset fysikaalisen selityksen?
8. **Mallivertailu.** Poista vippaus, maaliviivan läpimeno ja ohitus läheltä yksi kerrallaan ja sovita malli uudelleen. Vertaa uskottavuusosamäärätestillä tai informaatiokriteereillä (AIC, BIC). *Mittari:* mitkä termit ansaitsevat paikkansa, kun parametrien määrästä rangaistaan?
9. **Liikkuvat pelaajat.** Käytä StatsBomb 360 -aineistoa tai seurantadataa, jossa näkyy pelaajien liike. Anna puolustajan varjon kasvaa ajan myötä ja maalivahdin asettua todelliseen paikkaansa. *Mittari:* toistuuko tulos, että paineen oma vaikutus katoaa?
10. **Ennakkoon kirjatut ennusteet ja toisto.** Kirjaa hypoteesit ennen uuden datan katsomista: paras syvyys 0,7–1,0 m, paineen oma vaikutus lähellä nollaa, varjon leveys noin 1,3 m. Testaa ne uudella kaudella tai sarjalla, kirjoita lyhyt raportti (menetelmät, tulokset, rajoitukset) ja julkaise koodi. *Mittari:* säilyvätkö tulokset aineistossa, jota ei käytetty mallin rakentamiseen?

## 11. Käsitteet

- **Maaliodottama (xG):** todennäköisyys, että laukaus menee maaliin. Arvo 0,10 tarkoittaa, että sadasta samanlaisesta laukauksesta noin kymmenen menee sisään.
- **Malli:** laskusääntö, joka tuottaa luvun tilanteen tiedoista. Fysikaalinen malli rakennetaan siitä, miten asiat tapahtuvat. Tilastollinen malli rakennetaan siitä, miten luvut ovat datassa riippuneet toisistaan.
- **Vakio ja sovitus:** mallin tuntemattomat luvut valitaan niin, että malli selittää havainnot mahdollisimman hyvin.
- **Suurimman uskottavuuden menetelmä:** sovitustapa, jossa vakiot valitaan niin, että toteutunut data olisi mallin mukaan mahdollisimman todennäköinen.
- **Nelder–Mead:** optimointimenetelmä, joka etsii parhaat vakiot kokeilemalla ja siirtämällä pistejoukkoa askel kerrallaan ilman derivaattoja.
- **Logit-muunnos:** laskutemppu, jolla vakio pidetään sovituksen aikana sallituissa rajoissa.
- **Logistinen regressio:** tilastollinen perusmalli kyllä tai ei -tapahtumille. Se muuttaa selittäjien painotetun summan todennäköisyydeksi S-käyrällä.
- **Logaritminen häviö:** mittari ennusteiden osuvuudelle. Se rankaisee erityisesti varmoista virheistä. Pienempi on parempi.
- **Kalibrointi ja luotettavuuskäyrä:** malli on hyvin kalibroitu, jos sen luvut pitävät keskimäärin paikkansa. Luotettavuuskäyrä vertaa ennusteita toteutuneisiin ryhmittäin.
- **Jäännös:** havainnon ja mallin ennusteen erotus. Standardoitu jäännös suhteuttaa sen satunnaisvaihteluun: yli kahden suuruinen jäännös on jo epäilyttävä.
- **Ylisovitus, testiaineisto ja ristiinvalidointi:** mallia arvioitaessa samalla datalla, johon se sovitettiin, se näyttää liian hyvältä. Testiaineisto on dataa, jota malli ei ole nähnyt. Ristiinvalidoinnissa jokainen osa toimii vuorollaan testiaineistona.
- **Bootstrap ja luottamusväli:** takaisinpoiminnassa aineistosta arvotaan uusia samankokoisia otoksia ja sovitus toistetaan. Tulosten vaihtelu kertoo epävarmuuden, ja 95 %:n luottamusväli on se väli, johon vakio osuu 95 %:ssa toistoista.
- **Profiiliuskottavuus:** yhden vakion arvoa muutetaan askel kerrallaan ja muut sovitetaan joka kerta uudelleen. Tasainen käyrä kertoo, ettei data määrää vakiota.
- **Degeneraatio:** kaksi vakiota voi korvata toisensa niin, että malli sopii dataan yhtä hyvin.
- **Efektiivinen parametri:** luku, joka näyttää kuvaavan omaa ilmiötään, mutta onkin tiivistelmä hienommista yksityiskohdista. Paine oli sellainen.
- **AIC ja BIC:** informaatiokriteerit, jotka palkitsevat hyvästä sovituksesta ja rankaisevat ylimääräisistä vakioista.
- **Uskottavuusosamäärätesti:** tilastollinen testi siitä, parantaako lisätermi sovitusta enemmän kuin sattuma selittäisi.
- **Hierarkkinen bayesiläinen malli:** malli, jossa yksilöiden arvot oletetaan saman jakauman jäseniksi. Vähäisten havaintojen yksilöt vedetään kohti keskiarvoa (*kutistus*), mikä estää yksittäisiä onnenpotkuja näyttämästä taidolta.
- **Laukauksen jälkeinen xG (post-shot xG):** maaliodottama, joka lasketaan vasta, kun tiedetään, mihin kohtaan maalia laukaus suuntautui. Sillä mitataan maalivahtien torjuntaa.
- **Normaalijakauma ja keskihajonta:** kellokäyrä, jota satunnaiset virheet usein noudattavat. Noin 68 % arvoista on yhden ja 95 % kahden keskihajonnan päässä keskiarvosta.
- **Kertymäfunktio Φ:** kertoo, kuinka suuri osa normaalijakaumasta jää tietyn rajan alle.
- **Radiaani:** kulman yksikkö. Yksi radiaani on noin 57°.
- **Kehäkulmalause:** kaikki pisteet, joista jana näkyy samassa kulmassa, ovat samalla ympyränkaarella.
- **Eksponentiaalinen vaimeneminen:** suure pienenee samassa suhteessa jokaisella matkan tai ajan yksiköllä.
- **Tilannekuva (freeze frame):** laukaisuhetken kuva pelaajien paikoista.
- **Tila:** fysiikassa kaikki, mitä järjestelmästä tiedetään ja mistä sen käyttäytyminen lasketaan.
- **Ensemble-tulkinta:** kvanttimekaniikan tulkinta, jonka mukaan aaltofunktio kuvaa samalla tavalla valmisteltujen järjestelmien joukkoa. Samoin xG kuvaa samanlaisten laukausten joukkoa.
- **Piilomuuttuja ja Bellin epäyhtälö:** piilomuuttuja olisi tuntematon tekijä, joka ratkaisee tuloksen etukäteen. Bellin epäyhtälöitä rikkovat kokeet osoittavat, ettei kvanttimekaniikan satunnaisuutta voi selittää paikallisilla piilomuuttujilla.
- **Interferenssi:** aaltojen yhteisvaikutus, jossa ne vahvistavat tai kumoavat toisiaan.

---

## Tukeminen ja laki

Sivun lopussa on Buy Me a Coffee -painike. Suomen rahankeräyslain mukaan yksityishenkilö ei saa kerätä yleisöltä rahaa vastikkeetta. Siksi painike on muotoiltu ostoksi, jossa ostaja saa todellisen vastikkeen. Pelkkää nimen mainitsemista tukijaseinällä ei välttämättä pidetä riittävänä vastikkeena. Tulot ilmoitetaan verotuksessa tavalliseen tapaan. Tarkista ajantasaiset säännöt Poliisihallitukselta ja Verohallinnosta ennen julkaisua.

## Lähteet

- Data: [StatsBomb Open Data](https://github.com/statsbomb/open-data), kausi 2015/16.
- Muuttujaluettelo ja rangaistuspotkun 0,79: [Opta Analyst, What Is Expected Goals (xG)?](https://theanalyst.com/articles/what-is-expected-goals-xg)
