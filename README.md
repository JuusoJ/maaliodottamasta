# xG-simulaattori itse rakennettuna

*Maaliodottaman pohtiminen ja tarkempi ennustaminen voidaan kääntää fysiikan mallinrakennustehtäväksi. Tämä avaa mahdollisuuden jalkapallon seuraajien fysiikan oppimiselle.*

Juuso Jaakola, 2026

Interaktiivinen simulaattori ja blogikirjoitus, joka rakentaa jalkapallon maaliodottaman (xG) fysiikasta: kulmasta, pallon lentoajasta, maalivahdin ulottuvuudesta, puolustajien varjoista ja sattumasta. Malli on sovitettu 38 318 oikeaan laukaukseen (StatsBomb Open Data, kausi 2015/16). Se selittää dataa lähes yhtä hyvin kuin StatsBombin oma koneoppimismalli, mutta jokainen sen luku tarkoittaa jotain fysikaalista.

Sivulla on kolme välilehteä: **Kirjoitus** (malli ja sen sovitus), **Kvanttilaukaus** (miten klassinen laukaus eroaa elektronien laukauksista laboratorion varjostimelle) ja **Käsitteet**. Tämän ohjeen käsitteet on koottu kohtaan [11. Käsitteet](#11-käsitteet).

---

## 1. Mikä tämä on

Tavallinen xG kertoo, kuinka usein samasta paikasta ammuttu laukaus menee keskimäärin sisään. Keskiarvo kätkee yksilöt: sama veto on eri asia Rayaa kuin divarijoukkueen varamaalivahtia vastaan.

Projekti on mallinrakennusharjoitus teoreettisen fysiikan hengessä:

1. rakennetaan mekanismi (pallo lentää, maalivahti reagoi ja syöksyy, puolustaja peittää)
2. sovitetaan muutama vakio dataan
3. katsotaan, mitä malli ennustaa ja mitä se jättää selittämättä.

Kirjoituksessa on kolme tasoa: data ruudukkona, yksinkertainen perusfunktio ja fysikaalinen malli simulaattorina. Kvanttilaukaus-välilehti käyttää maaliodottamaa vertailukohtana: xG:n todennäköisyys on tietämättömyyttä yksityiskohdista (Gibbsin joukko, sään ensemble-ennusteet), kun taas elektronien kaksoisrakokokeessa amplitudit summautuvat ja toisen raon avaaminen voi vähentää osumia maaliin. Välilehti käsittelee Ballentinen ensemble-tulkintaa, piilomuuttujien ansaa, Bellin ja Kochenin–Speckerin tuloksia sekä sitä, mitä mikromaailmasta voi kokea arjessa.

## 2. Tiedostot ja käyttö

| Tiedosto | Sisältö |
|---|---|
| `index.html` | Koko sivu: teksti, simulaattori, malli ja ruudukon data yhdessä tiedostossa |
| `README.md` | Tämä ohje |
| `analyysi/` | Skriptit, joilla luvut voi toistaa: datan haku, piirteet, malli, sovitus, arviointi ja bootstrap (kohta 12) |
| `maaliodottama-muistio.pdf` | Tukijoiden kaksisivuinen muistio ja vastaukset kahteen kysymykseen (vastike, ei jaeta sivulla) |

Sivu toimii avaamalla `index.html` selaimessa. Asennuksia tai käännösvaihetta ei tarvita. Fontit ladataan Google Fontsista, mutta sivu toimii ilmankin.

**GitHub Pages:** vie tiedostot repositorioon ja valitse *Settings → Pages → Deploy from a branch → main / (root)*.

**Muuta ennen julkaisua** (hae tiedostosta hakusanalla):

- `KAYTTAJANIMI`: oma Buy Me a Coffee -osoite
- `TUKIJASEINA`: tukijaseinän osoite
- `VASTIKE`: teksti siitä, mitä ostaja todella saa (katso kohta *Tukeminen ja laki* alempana)
- Kohta *Tekijästä ja tekoälyn käytöstä* kirjoituksen lopussa: tarkista, että muotoilu vastaa omaa käsitystäsi.

**Simulaattorin käyttö**

- Vedä tai napauta palloa. Kartta näyttää maaliodottaman jokaisesta laukaisupisteestä.
- Vedä maalivahtia tai punaisia puolustajia. Silloin ne jäävät paikoilleen. *Automaattiset* palauttaa maalivahdin parhaaseen paikkaan ja puolustajat oletusmuodostelmaan.
- Pelaajapainikkeet asettavat laukojan ja maalivahdin arvot. Arvot ovat havainnollistavia arvioita, eivät mittauksia.
- *Näytä ero keskitasoon* värittää kartan erotuksena keskitasosta. *Esimerkkitilanne* palauttaa kirjoituksen lopun esimerkin.
- *Kopioi linkki tilanteeseen* tekee linkin, joka avaa simulaattorin juuri samaan tilanteeseen: pallo, säätimet, valinnat, näkymä sekä vedetyt maalivahti ja puolustajat. Tila on osoitteen kyselyosassa (`?s=…&p=…&g=…&k=…&d=…`).
- *Oikeat laukaukset* lataa seitsemän finaalilaukausta (MM 2022, EM 2024) tilannekuvineen: viisi maalia, yksi torjunta ja yksi ohilaukaus. Pelitilanne, syötön tyyppi ja laukaisutapa on poimittu StatsBombin tapahtumadatasta, laukoja ja maalivahti saavat karkeasti arvioidut profiilit, ja henkinen paine on finaalissa 0,6 ja jatkoajalla 0,8. Ruudulla näkyy mallin arvo keskitason pelaajilla (sama kuin arvioinnissa), arvo profiileilla ja pelitilanteella, StatsBombin xG ja lopputulos. Osa profiileista (Messi, Mbappé, Emiliano Martínez, Pickford) on valittavissa myös pelaajapainikkeista.
- *Syöttö jalkaan* on tavallinen syöttö. Sen kertoimet ovat samat kuin omalla kuljetuksella, mutta se kuvaa tilannetta oikein.
- Kvanttilaukaus-välilehdellä on *virusten xG-simulaattori*: kaksoisrakokoe fullereeneilla mikrostadionilla (mittakaava 1 : 220 000 000). Potkun nopeus ja aukkojen väli muuttavat juovien väliä Λ = hL/(mvd), ja maaliodottama heiluu, kun juovat liukuvat maalin yli.
- Syvyyskäyrä näyttää, miten maaliodottama muuttuu maalivahdin etäisyyden mukana. Käyrää napauttamalla maalivahti siirtyy.
- Välilehdet ovat simulaattorin alla ja pysyvät näkyvissä vieritettäessä. Jokainen välilehti muistaa oman vierityskohtansa. Lihavoitu käsite vie Käsitteet-välilehdelle, ja *Palaa tekstiin* palauttaa samaan kohtaan. Välilehdille voi linkittää suoraan: `index.html#kvantti` ja `index.html#kasitteet`.

## 3. Data

StatsBombin avoimessa aineistossa ovat kauden 2015/16 Valioliiga, La Liga ja Serie A kokonaan, Ligue 1 lähes kokonaan (377 ottelua) sekä 34 Bundesliga-ottelua. Laukauksia on 38 318 ilman rangaistuspotkuja, ja niistä 3 651 eli 9,5 % päätyi maaliin. Rangaistuspotkuja on 410, ja niistä 75,1 % meni sisään.

Jokaisesta laukauksesta tunnetaan paikka, lopputulos, laukaisutapa (jalka, pusku, volley, suoraan syötöstä), pelitilanne, paine kyllä tai ei -tietona sekä **tilannekuva** (*freeze frame*). Tilannekuvassa näkyvät laukaisuhetken pelaajien paikat. Niistä on poimittu maalivahdin paikka ja kaikki puolustajat, jotka ovat laukauksen kolmiossa tai alle 2,5 metrin päässä siitä. Tällaisia puolustajia on keskimäärin 2,3 laukausta kohden. Lisäksi jokaisesta laukauksesta on laskettu lähimmän vastustajan etäisyys, joka on keskimäärin 2,65 m.

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

**5.4 Puolustajien varjot ja paine.** `α_d = arctan(r_d / s_d)`, `σ_p → σ_p·g(r)`, `g(r) = 1 + k_i·1,16·(e^(−r/0,6 m) − e^(−2,7 m/0,6 m))`, `k_i = 1 − 0,5·(i_p − 0,35)`, `r = min(r_vapaa, lähin puolustaja)`, `r_vapaa = max(5 m·(1 − paine), 0,1 m)`. Jokainen puolustaja peittää laukojan silmin kulmavälin, josta hän pysäyttää osuuden *q*_d. Lähellä oleva puolustaja peittää suuren kulman, ja laukoja tähtää varjojen ohi. Paine on lähimmän vastustajan etäisyys *r*: kyljessä kiinni (0,1 m) keskitasoisen laukojan hajonta kaksinkertaistuu (×2,0), puolen metrin päästä se kasvaa 1,5-kertaiseksi ja yli kahden metrin päässä vaikutus on lähes nolla. Sijoitusäly ei muuta vapaata tilaa vaan pienentää paineen haittaa kertoimella *k*_i (arvio).

**5.5 Tähtäys ja hajonta.** `P_laukaus = V · Σᵢ εᵢ · [Φ((bᵢ − μ)/σ_tot) − Φ((aᵢ − μ)/σ_tot)]`. Maalin näkökulma jakautuu väleihin: vapaa maali, maalivahdin vyöhykkeet ja puolustajien varjot. Laukoja valitsee suunnan μ, joka tekee summasta suurimman. Toteutunut suunta vaihtelee normaalijakauman mukaan (suuntahajonta σ_p), ja *V* on todennäköisyys pysyä riman alla. Kirjoituksen kuva 3 näyttää laukauksen laukojan silmin matemaattisella päätyrajalla: maahan suuntautuvat laukaukset pomppaavat, ja pomppu lasketaan peilikuvamenetelmällä. Kun pystyhajonta on 2,9 m, pomput mukaan lukien riman alle jää 59 % laukauksista, saman verran kuin *V* antaa 25 metristä. Tulkinta on jälkikäteinen.

**5.6 Vippaus (lob).** Pallo nostetaan kaarella ulos tulleen maalivahdin yli. Vippaus onnistuu, jos maalivahti ei ehdi perääntyä viivalle ennen kuin pallo putoaa. Kierrettä malli ei tunne.

**5.7 Tyhjä maali, laukauksen kolmio ja käsisääntö.** `P_laukaus = w·P_maalivahti + (1 − w)·P_tyhjä`, `w = max(0, 1 − s⊥/4 m)`. Maalivahdin vaikutus hiipuu neljän metrin matkalla laukauksen kolmion ulkopuolella ja katoaa pallon takana. Yli puoli metriä rangaistusalueen ulkopuolella maalivahti on kenttäpelaaja ilman käsiä.

**5.8 Sattuma ja kantama.** `p₀ = 0,065 · e^(−d/10,7 m) · e^(−(Δy/15 m)²) · Φ((R_max − d)/5 m)`, `R_max = L·ln(1 + (0,85·v_p)²/(gL))`. Kimmokkeet ja virheet antavat pienen pohjan, joka on suurin maalin edessä. Kantama katkaisee kaukaiset vedot: keskitasoisella laukojalla (28 m/s) se on 43 m.

**Tilannevalinnat** kytkeytyvät samoihin suureisiin. Esimerkiksi pusku kasvattaa hajontaa, hidastaa palloa ja lyhentää kantaman 13,6 metriin. Vapaapotku poistaa puolustajat vetolinjalta mutta lisää muurin. Paineen säädin asettaa vapaan tilan viidestä metristä 0,1 metriin.

## 6. Sovitus ja arviointi

Vakiot on sovitettu **suurimman uskottavuuden menetelmällä**. Jokaiselle laukaukselle lasketaan mallin todennäköisyys oikeilla maalivahdin ja puolustajien paikoilla ja lähimmän vastustajan etäisyydellä, ja vakiot valitaan niin, että toteutuneet maalit ja ohilaukaukset ovat mahdollisimman todennäköisiä. Optimointiin käytettiin Nelder–Mead-menetelmää, ja vakiot pidettiin fysikaalisissa rajoissa logit-muunnoksella.

| Sovitettu vakio | Arvo | Merkitys |
|---|---|---|
| ε_max | 0,462 | torjunnan pettämisen yläraja (keskitasolla 0,36) |
| P0 | 0,065 | sattumien taso maalin edessä |
| P0L | 10,7 m | sattumien vaimenemismatka |
| puskun hajonta | × 2,18 | puskun suuntahajonta suhteessa jalkaan |
| puskun kantama | 13,6 m | kuinka kauas pusku kantaa |
| tyhjän maalin hajonta | × 0,85 | rauhallinen sijoitus tyhjään maaliin |
| r_d | 0,57 m | puolustajan varjon puolileveys |
| q_d | 0,75 | blokin varmuus varjossa |
| ohitus läheltä | 0,99 | ulos tulleen maalivahdin läpimeno (sallitun välin rajalla) |
| vapaapotkun hajonta | × 0,43 | vapaapotkun tarkkuus |
| paineen voimakkuus | 1,16 | kuinka paljon lähellä oleva vastustaja kasvattaa hajontaa |

Käsin on asetettu keskitasoisen laukojan arvot (σ_p = 21°, *v*_p = 28 m/s, sijoitusäly 0,35), torjunnan aikavakio τ = 1,0 s, paineen vaimenemismatka 0,6 m ja neutraali etäisyys 2,7 m. Data ei erottele niitä muista vakioista (katso *degeneraatio* kohdassa 11). Reaktioaika, syöksynopeus, rimaehto ja ilmanvastus ovat fysikaalisia arvioita. Rangaistuspotkun hajonta on kalibroitu niin, että xG on 0,75.

**Arviointi logaritmisella häviöllä.** Parannus kertoo, kuinka paljon malli pienentää häviötä verrattuna siihen, että jokainen laukaus saa arvon 0,095.

| Malli | Parannus |
|---|---|
| Etäisyys | 10,9 % |
| Kulma | 10,4 % |
| Perusfunktio | 11,8 % |
| Simulaattori, pelkkä paikka ja laukaisutapa | 11,9 % |
| Simulaattori, todelliset maalivahdin ja puolustajien paikat | 20,9 % |
| StatsBombin xG | 21,0 % |

**Kalibrointi ryhmittäin** (toteutunut / malli):

| Ryhmä | Toteutunut | Malli |
|---|---|---|
| Puskut | 10,7 % | 10,7 % |
| Vapaapotkut | 6,4 % | 6,6 % |
| Volleyt | 10,5 % | 10,4 % |
| 16,5–22 m | 4,8 % | 4,6 % |
| Ei puolustajia lähellä | 26,4 % | 22,6 % |
| 2 puolustajaa | 6,6 % | 6,9 % |


### 6.1 Ulkoinen testi

Malli ajettiin sellaisenaan, ilman uudelleensovitusta, kuuteen turnaukseen, joita sovituksessa ei käytetty: MM 2018 ja 2022, EM 2020 ja 2024, Copa América 2024 ja Afrikan mestaruuskilpailut 2023. Niissä on 314 ottelua ja 7 509 laukausta ilman rangaistuspotkuja, ja maaliin meni 8,9 %. Etäisyys- ja kulmamallit on sovitettu vain opetusaineistoon, ja vertailukohta on vakio 0,095. Välit ovat 95 %:n bootstrap-välejä: turnausten otteluita poimittiin takaisin 1 000 kertaa, ja mallit pysyivät kiinteinä.

| Malli | Sovitusaineisto | Turnaukset | 95 %:n väli |
|---|---|---|---|
| Etäisyys | 10,9 % | 8,5 % | 6,5–10,9 % |
| Kulma | 10,4 % | 8,2 % | 5,9–10,6 % |
| Perusfunktio | 11,8 % | 9,4 % | 7,5–12,0 % |
| Simulaattori, pelkkä paikka ja laukaisutapa | 11,9 % | 10,2 % | 7,6–13,6 % |
| Simulaattori, todelliset paikat | 20,9 % | 17,8 % | 14,8–20,6 % |
| StatsBombin xG | 21,0 % | 18,7 % | 16,1–21,6 % |

Fysiikkamalli on perusfunktiota 8,4 prosenttiyksikköä parempi (väli 5,9–9,6), ja StatsBomb on fysiikkamallia 0,9 yksikköä edellä (väli 0,0–1,9). StatsBombin malli ei välttämättä ole aidosti ulkopuolinen, koska sen opetusaineistoa ei ole julkaistu.

| Turnaus | Laukauksia | Maaleja | Perusfunktio | Simulaattori | StatsBomb |
|---|---|---|---|---|---|
| MM 2018 | 1638 | 8,2 % | 10,6 % | 14,9 % | 16,9 % |
| MM 2022 | 1430 | 10,6 % | 12,5 % | 21,8 % | 21,5 % |
| EM 2020 | 1234 | 9,9 % | 10,0 % | 19,1 % | 22,3 % |
| EM 2024 | 1304 | 7,5 % | 6,8 % | 15,6 % | 16,4 % |
| Copa América 2024 | 741 | 8,5 % | 5,1 % | 16,6 % | 17,5 % |
| Afrikan MM 2023 | 1162 | 8,4 % | 7,8 % | 17,6 % | 16,2 % |

**Kalibrointi turnauksissa** (simulaattori todellisilla paikoilla):

| Ryhmä | Laukauksia | Toteutunut | Malli | StatsBomb |
|---|---|---|---|---|
| Puskut | 1370 | 10,0 % | 10,5 % | 11,1 % |
| Vapaapotkut | 319 | 4,4 % | 6,6 % | 3,9 % |
| Volleyt | 1413 | 9,3 % | 10,6 % | 10,6 % |
| Alle 11 m | 2125 | 17,6 % | 18,6 % | 18,0 % |
| 11–16,5 m | 1835 | 9,6 % | 9,2 % | 10,0 % |
| 16,5–22 m | 1716 | 4,2 % | 4,3 % | 4,7 % |
| Yli 22 m | 1833 | 2,6 % | 2,5 % | 2,2 % |
| Ei puolustajia lähellä | 969 | 23,7 % | 21,8 % | 22,9 % |
| 2 puolustajaa | 1869 | 6,8 % | 7,4 % | 7,1 % |
| Lähin vastustaja alle 1 m | 1283 | 9,2 % | 10,4 % | 10,8 % |

Vapaapotkuissa malli on liian optimistinen (ero noin 1,6 keskihajontaa). Kymmenyksittäin ennuste ja toteuma eroavat enintään 1,3 prosenttiyksikköä.

## 7. Keskeiset tulokset

- **Paine riippuu siitä, miten se mitataan.** Kyllä tai ei -merkintänä paineen oma vaikutus katoaa, kun puolustajien paikat otetaan mukaan. Lähimmän vastustajan etäisyytenä mitattuna se palaa, mutta vain lähellä: kyljessä kiinni oleva vastustaja kaksinkertaistaa hajonnan ja pudottaa maaliodottamaa yli 40 %, mutta kahden metrin jälkeen vaikutus on lähes nolla.
- **Puolustaja on 1,1 metrin varjo**, joka pysäyttää kolme neljästä siihen osuvasta laukauksesta. Rangaistusalueen rajalta keskeltä veto on ilman puolustajia 0,091 ja yhden puolustajan kanssa 0,054.
- **Paras maalivahdin paikka on 0,8–1,0 metriä viivan edessä** keskeltä ammuttuja 11–16,5 metrin vetoja vastaan. Kauempaa ammuttua vetoa vastaan kannattaa tulla pidemmälle.
- **Yksilöt ratkaisevat.** Samasta paikasta veto on Rayaa vastaan 0,047 ja divarin varamaalivahtia vastaan 0,089.
- **Tyhjä maali ei ole varma.** Datassa 55 % laukauksista, joissa maalivahti oli yli kolme metriä pallon takana, meni sisään.
- **Kaukolaukauksista lähes puolet on mallissa sattumaa.** 25 metristä 0,006 kokonaisarvosta 0,014 tulee sattumien pohjasta.
- **Tulos kestää uuden aineiston.** Kuudessa turnauksessa, joita sovituksessa ei käytetty, fysiikkamalli pienensi häviötä 17,8 %, perusfunktio 9,4 % ja StatsBomb 18,7 %.
- **Hyvä sovitus ei todista mekanismia.** Tarkempi laukoja ja vuotavampi maalivahti selittävät samat maalit lähes yhtä hyvin.

## 8. Rajoitukset

- Vakiot on sovitettu yhteen seurakauteen. Ulkoinen testi on tehty turnauksilla, jotka ovat pieniä ja erilaisia kuin sarjaottelut. Toista seurakautta malli ei ole vielä kohdannut.
- Vapaapotkuissa malli oli turnauksissa liian optimistinen (6,6 % vastaan toteutunut 4,4 %).
- Maali on yksiulotteinen: korkeus näkyy vain rimaehtona, vippauksena ja sylivälin vaikutuksena. Pomppu on mukana vain rimaehdon tulkintana (kuva 3).
- Puolustajat ovat samanlevyisiä kiekkoja, jotka eivät liiku. Paine on pelkkä etäisyys: malli ei tiedä, onko painostaja edessä, sivulla vai takana.
- Osa termeistä on muodoltaan arvauksia: vippaus, maaliviivan läpimeno ja ohitus läheltä. Ohituksen kerroin asettui sallitun välin rajalle, mikä viittaa puuttuvaan rakenteeseen.
- Pelaajaprofiilit, henkinen paine, maalivahdin häirintä ja syötön tyyppi ovat arvioita ilman dataa.
- Kartan maalivahti on aina optimaalinen ja puolustaja suoraan vetolinjalla, joten kartan luvut ovat alarajoja.

## 9. Mitä mallin rakentamisesta opittiin

1. **Käsin viritetty malli oli kaksi kertaa liian optimistinen.** Ensimmäinen versio antoi keskimäärin 0,17, kun data antaa 0,095. Sovitus dataan on välttämätön, vaikka mekanismi tuntuisi oikealta.
2. **Vapaasti sovitetut vakiot karkaavat epäfysikaalisiin arvoihin.** Osa vakioista kannattaa lukita fysikaalisiin arvioihin ja sovittaa vain ne, joista data todella kertoo.
3. **Data kumosi intuitioita.** Tyhjä maali rangaistusalueen rajalta ei ole 0,75, eikä jalkoihin sukeltava maalivahti romahduta todennäköisyyttä nollaan.
4. **Mittaustapa ratkaisee.** Paine katosi, kun se oli kyllä tai ei -merkintä, ja palasi, kun se mitattiin etäisyytenä. Tämä on mallin kiinnostavin löytö.
5. **Epäfysikaalisuudet kannattaa kirjata näkyviin.** Ne ovat seuraavan version tehtävälista.

## 10. Harjoitustehtävät

Tehtävät vievät mallia kohti tutkimustasoa. Jokaisessa on tavoite, toimenpide ja mittari, jolla onnistumista arvioidaan.

1. **Erillinen testiaineisto.** Turnaustesti on tehty (kohta 6.1). Seuraava askel: sovita malli kolmeen sarjaan ja testaa neljännellä, tai käytä ristiinvalidointia. Jaa aineisto otteluittain, ei laukauksittain, koska saman ottelun laukaukset riippuvat toisistaan. *Mittari:* testiaineiston parannus verrattuna 20,9 %:iin.
2. **Epävarmuus näkyviin.** Arvo otteluita takaisinpoiminnalla (bootstrap) ja sovita malli uudelleen satoja kertoja. Anna jokaiselle vakiolle ja parannukselle 95 %:n luottamusväli. Piirrä häviö aikavakion τ ja paineen vaimenemismatkan funktiona (profiiliuskottavuus). *Mittari:* kuinka leveitä välit ovat ja mitkä vakiot data todella määrää.
3. **Kalibrointi ja jäännöskartta.** Piirrä luotettavuuskäyrä: jaa laukaukset kymmeneen ryhmään ennusteen mukaan ja vertaa ennustetta toteutuneeseen. Laske jokaiseen ruutuun standardoitu jäännös (havaittu − malli) / √(n·p·(1 − p)). *Mittari:* missä ruuduissa jäännös on yli 2, eli missä fysiikka puuttuu.
4. **Kaksiulotteinen maali.** StatsBombin aineistossa on laukauksen loppupiste korkeuksineen. Sovita suuntahajonta erikseen vaaka- ja pystysuunnassa ja korvaa rimaehto *V* todellisella korkeusjakaumalla. *Mittari:* paraneeko häviö, ja pieneneekö ylärajalle asettuneen ohitustermin tarve?
5. **Pelaajakohtaiset arvot.** Kerää useampi kausi ja sovita jokaiselle laukojalle oma σ_p hierarkkisella bayesiläisellä mallilla, joka kutistaa vähäisten havaintojen arvot kohti keskiarvoa. *Mittari:* kuinka monta laukausta tarvitaan, jotta huippulaukojan hajonta erottuu keskitasosta, ja vastaavatko sivun pelaajaprofiilit dataa?
6. **Maalivahtien torjuntakyky.** Sovita ε_max maalivahtikohtaisesti niistä laukauksista, jotka menivät kohti maalia. Vertaa laukauksen jälkeiseen xG:hen (*post-shot xG*). *Mittari:* toistuuko maalivahdin ero kaudesta toiseen, vai onko se satunnaisvaihtelua?
7. **Kimmokemalli sattuman tilalle.** Mallinna, kuinka suuri osa puolustajan varjoon osuneista laukauksista kimpoaa maaliin. Käytä StatsBombin blokkausmerkintöjä. *Mittari:* pieneneekö sattumien pohja *p*₀, ja saavatko kaukolaukaukset fysikaalisen selityksen?
8. **Mallivertailu.** Poista vippaus, maaliviivan läpimeno ja ohitus läheltä yksi kerrallaan ja sovita malli uudelleen. Vertaa uskottavuusosamäärätestillä tai informaatiokriteereillä (AIC, BIC). *Mittari:* mitkä termit ansaitsevat paikkansa, kun parametrien määrästä rangaistaan?
9. **Liikkuvat pelaajat.** Käytä StatsBomb 360 -aineistoa tai seurantadataa, jossa näkyy pelaajien liike. Anna puolustajan varjon kasvaa ajan myötä ja maalivahdin asettua todelliseen paikkaansa. *Mittari:* toistuuko tulos, että paine vaikuttaa vain alle kahden metrin päästä, ja riippuuko vaikutus painostajan suunnasta?
10. **Ennakkoon kirjatut ennusteet ja toisto.** Kirjaa hypoteesit ennen uuden datan katsomista: paras syvyys 0,8–1,0 m, paineen vaikutus vain alle kahden metrin päästä, varjon leveys noin 1,1 m. Testaa ne uudella kaudella tai sarjalla, kirjoita lyhyt raportti (menetelmät, tulokset, rajoitukset) ja julkaise koodi. *Mittari:* säilyvätkö tulokset aineistossa, jota ei käytetty mallin rakentamiseen?

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
- **Efektiivinen parametri:** luku, joka näyttää kuvaavan omaa ilmiötään, mutta onkin tiivistelmä hienommista yksityiskohdista. Kyllä tai ei -merkintänä mitattu paine oli sellainen.
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
- **Tila ja karkeistettu tila:** fysiikassa tila on kaikki, mitä järjestelmästä tiedetään ja mistä sen käyttäytyminen lasketaan. Karkeistettu tila kertoo vain olennaisimmat suureet, kuten lämpötila molekyylien liikkeestä tai xG laukauksesta.
- **Gibbsin joukko ja ensemble-ennuste:** ajateltu joukko kopioita samasta makroskooppisesta tilasta (Gibbs 1902). Sääennusteissa malli ajetaan monta kertaa hieman eri alkutiloista.
- **Peilikuvamenetelmä:** rajapinnan vaikutus korvataan peilikuvalla. Kuvassa 3 maahan suuntautuva laukaus peilataan maan pinnan yläpuolelle.
- **Amplitudi ja Bornin sääntö:** kvanttimekaniikassa reitillä on kompleksinen amplitudi, ja todennäköisyys on amplitudien summan itseisarvon neliö.
- **Hilbertin avaruus:** vektoriavaruus, jonka alkiot ovat kvanttitiloja.
- **Interferenssi ja dekoherenssi:** amplitudit voivat vahvistaa tai kumota toisensa. Kun reittitieto karkaa ympäristöön, interferenssi katoaa (dekoherenssi).
- **Ensemble-tulkinta:** Ballentinen muotoilema tulkinta, jonka mukaan kvanttitila kuvaa samoin valmisteltujen järjestelmien joukkoa. Minimaalinen versio (Home ja Whitaker 1992) ei väitä, että yksittäisellä hiukkasella olisi valmiiksi määrätty rata. Se muistuttaa xG:n logiikkaa, mutta joukon todennäköisyyksiä ei voi selittää paikallisilla tuntemattomilla yksityiskohdilla.
- **Piilomuuttuja, Bellin epäyhtälö ja kontekstuaalisuus:** piilomuuttuja olisi tuntematon tekijä, joka ratkaisee tuloksen etukäteen. Bellin epäyhtälöitä rikkovat kokeet sulkevat pois paikalliset piilomuuttujat, ja Kochenin–Speckerin lause osoittaa, ettei arvoja voi antaa mittausyhteydestä riippumatta. Epälokaalit piilomuuttujat (Bohmin mekaniikka) ovat mahdollisia.

## 12. Toistettavuus

Kansiossa `analyysi/` ovat skriptit, joilla kirjoituksen luvut voi laskea alusta. Ne vaativat Python 3:n ja Node.js:n, mutta eivät muita kirjastoja.

| Tiedosto | Tehtävä |
|---|---|
| `fetch.py` | Hakee yhden kilpailun laukaukset tilannekuvineen StatsBomb Open Datasta |
| `features.py` | Laskee mallin piirteet: paikka metreinä, maalivahti, puolustajat, lähin vastustaja |
| `model.js` | Malli, sama kuin sivun simulaattorissa |
| `fit.js` | Sovittaa 11 vakiota (Nelder–Mead), valinnaisesti bootstrap-otokseen |
| `evaluate.js` | Arvioi mallit opetus- ja testiaineistossa sekä laskee kalibroinnin ja bootstrap-välit |
| `boot.sh` | Toistaa sovituksen otteluittain takaisinpoimituilla aineistoilla |
| `run_all.sh` | Ajaa koko ketjun: data, piirteet ja arviointi |
| `ext_results.json` | Arvioinnin tulokset |

Aja `./run_all.sh`. Datan haku kestää muutaman minuutin ja tuottaa noin 110 Mt laukaustiedostoja, joita ei ole mukana. Kun `features.py` ajetaan kauden 2015/16 tiedostoille, se tuottaa samat piirteet kuin sovituksessa käytetyt, laukaus laukaukselta. Pysyvän DOI:n saa viemällä repositorion Zenodoon.

---

## Tukeminen ja laki

Sivun lopussa on vaatimaton Buy Me a Coffee -painike. Vastikkeena on kaksisivuinen PDF-muistio (`maaliodottama-muistio.pdf`), jota ei jaeta sivulla. Suomen rahankeräyslain mukaan yksityishenkilö ei saa kerätä yleisöltä rahaa vastikkeetta. Siksi painike on muotoiltu ostoksi, jossa ostaja saa todellisen vastikkeen. Pelkkää nimen mainitsemista tukijaseinällä ei välttämättä pidetä riittävänä vastikkeena. Tulot ilmoitetaan verotuksessa tavalliseen tapaan. Tarkista ajantasaiset säännöt Poliisihallitukselta ja Verohallinnosta ennen julkaisua.

## Tekijä ja tekoälyn käyttö

Idea, mallin rakenne ja muuttujien valinta ovat kirjoittajan (Juuso Jaakola). Tekoälyä (Anthropicin Claude) käytettiin työn kaikissa vaiheissa: mallin sovittamisessa dataan, ohjelmoinnissa, kuvissa, lähteiden etsinnässä ja tekstin muotoilussa. Kirjoittaja ohjasi työtä, kyseenalaisti tulokset ja teki lopulliset valinnat.

## Lähteet

- Data: [StatsBomb Open Data](https://github.com/statsbomb/open-data), kausi 2015/16 sekä testinä MM 2018 ja 2022, EM 2020 ja 2024, Copa América 2024 ja Afrikan mestaruuskilpailut 2023.
- Muuttujaluettelo ja rangaistuspotkun 0,79: [Opta Analyst, What Is Expected Goals (xG)?](https://theanalyst.com/articles/what-is-expected-goals-xg)
- Box, G. E. P. (1976). Science and statistics. *Journal of the American Statistical Association*, 71(356), 791–799.
- Gibbs, J. W. (1902). *Elementary Principles in Statistical Mechanics*. New York: Scribner’s.
- Jordet, G., Hartman, E., Visscher, C. & Lemmink, K. A. P. M. (2007). Kicks from the penalty mark in soccer. *Journal of Sports Sciences*, 25(2), 121–129.
- Leutbecher, M. & Palmer, T. N. (2008). Ensemble forecasting. *Journal of Computational Physics*, 227(7), 3515–3539.
- Ballentine, L. E. (1970). The statistical interpretation of quantum mechanics. *Reviews of Modern Physics*, 42(4), 358–381.
- Ballentine, L. E. (1998). *Quantum Mechanics: A Modern Development*. Singapore: World Scientific.
- Home, D. & Whitaker, M. A. B. (1992). Ensemble interpretations of quantum mechanics: A modern perspective. *Physics Reports*, 210(4), 223–317.
- Bell, J. S. (1964). On the Einstein Podolsky Rosen paradox. *Physics Physique Fizika*, 1(3), 195–200.
- Hensen, B. ym. (2015). Loophole-free Bell inequality violation using electron spins separated by 1.3 kilometres. *Nature*, 526, 682–686.
- Kochen, S. & Specker, E. P. (1967). The problem of hidden variables in quantum mechanics. *Journal of Mathematics and Mechanics*, 17(1), 59–87.
- Tonomura, A. ym. (1989). Demonstration of single-electron buildup of an interference pattern. *American Journal of Physics*, 57(2), 117–120.
- Bach, R., Pope, D., Liou, S.-H. & Batelaan, H. (2013). Controlled double-slit electron diffraction. *New Journal of Physics*, 15, 033018.
- Gibney, E. (2025). Physicists disagree wildly on what quantum mechanics says about reality, Nature survey shows. *Nature*, 643, 1175.
- Kvanttivälilehden täydellinen lähdeluettelo on sivulla.

## Versiohistoria

- **28.9.2026 (3):** oikeiden laukausten pelitilanteet tapahtumadatasta, pelaajaprofiilit (osa valittavissa), seitsemäs laukaus (Lautaro Martínezin ohilaukaus), syöttövaihtoehto *Syöttö jalkaan*; kvanttivälilehdelle tarina virusten mikrostadionista, kuvat K1 (muuri kahdella aukolla) ja K2 (päätyraja laukojan silmin neljässä tilanteessa) sekä virusten xG-simulaattori.

- **28.9.2026 (2):** ulkoinen testi kuudella turnauksella (17,8 % vs. StatsBomb 18,7 %); jaettava tilannelinkki; kuusi finaalilaukausta simulaattoriin; analyysiskriptit kansioon `analyysi/`.

- **28.9.2026:** uusi otsikko ja kirjoittaja; välilehdet Kirjoitus, Kvanttilaukaus ja Käsitteet; lihavoidut käsitelinkit ja paluupainike; kuva 3 (laukojan näkymä päätyrajalle, pomput peilikuvamenetelmällä); kuva K1 (kvanttilaukaus kahden raon läpi); paineen säädin 0,1 metriin asti ja sijoitusälyn kerroin *k*_i; arvuutusmuotoiset kysymykset; läpinäkyvyyshuomio ja lähdeluettelot.
