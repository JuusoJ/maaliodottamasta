# xG-simulaattori itse rakennettuna

*Maaliodottaman pohtiminen ja tarkempi ennustaminen voidaan kääntää fysiikan mallinrakennustehtäväksi. Tämä avaa mahdollisuuden jalkapallon seuraajien fysiikan oppimiselle.*

Juuso Jaakola, 2026

Interaktiivinen simulaattori ja blogikirjoitus, joka rakentaa jalkapallon maaliodottaman (xG) fysiikasta: kulmasta, pallon lentoajasta, maalivahdin ulottuvuudesta, puolustajien varjoista, pallon kaaresta ja pompusta sekä sattumasta. Malli on sovitettu 38 318 oikeaan laukaukseen (StatsBomb Open Data, kausi 2015/16). Se selittää dataa yhtä hyvin kuin StatsBombin oma koneoppimismalli, mutta jokainen sen luku tarkoittaa jotain fysikaalista.

Sivulla on kolme välilehteä: **Kirjoitus** (malli ja sen sovitus), **Kvanttilaukaus** (virukset potkivat fullereeneja kahden aukon läpi: miten klassinen laukaus eroaa kvanttilaukauksesta) ja **Käsitteet**. Tämän ohjeen käsitteet on koottu kohtaan [11. Käsitteet](#11-käsitteet).

---

## 1. Mikä tämä on

Tavallinen xG kertoo, kuinka usein samasta paikasta ammuttu laukaus menee keskimäärin sisään. Keskiarvo kätkee yksilöt: sama veto on eri asia Rayaa kuin divarijoukkueen varamaalivahtia vastaan.

Projekti on mallinrakennusharjoitus teoreettisen fysiikan hengessä:

1. rakennetaan mekanismi (pallo lentää, maalivahti reagoi ja syöksyy, puolustaja peittää)
2. sovitetaan muutama vakio dataan
3. katsotaan, mitä malli ennustaa ja mitä se jättää selittämättä.

Kirjoituksessa on kolme tasoa: data ruudukkona, yksinkertainen perusfunktio ja fysikaalinen malli simulaattorina. Kvanttilaukaus-välilehti käyttää maaliodottamaa vertailukohtana: xG:n todennäköisyys on tietämättömyyttä yksityiskohdista (Gibbsin joukko, sään ensemble-ennusteet), kun taas fullereenien kaksoisrakokokeessa amplitudit summautuvat ja toisen raon avaaminen voi vähentää osumia maaliin. Välilehti käsittelee Ballentinen ensemble-tulkintaa, piilomuuttujien ansaa, Bellin ja Kochenin–Speckerin tuloksia sekä sitä, mitä mikromaailmasta voi kokea arjessa.

## 2. Tiedostot ja käyttö

| Tiedosto | Sisältö |
|---|---|
| `index.html` | Koko sivu: teksti, simulaattori, malli ja ruudukon data yhdessä tiedostossa |
| `README.md` | Tämä ohje |
| `analyysi/` | Skriptit, joilla luvut voi toistaa: datan haku, piirteet, malli, sovitus, pystysuunta, arviointi ja bootstrap (kohta 12) |
| `muistio.tex` | Tukijoiden muistio LaTeX-lähdekoodina (Overleaf, pdfLaTeX); vastike, ei jaeta sivulla |
| `maaliodottama-muistio.pdf` | Muistion käännetty versio |
| `tutkimus_ja_suunnittelu.tex` | Tutkimus- ja julkaisusuunnitelma: tutkimuskysymykset, julkaisukanavat, levitys, jatkokehitys ja aikataulu |

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

**5.3 Vuoto.** `ε = ε_max · e^(−m/τ)`. Palloon ehtiminen ei ole torjunta: vuoto ε on todennäköisyys, että pallo menee maaliin, vaikka maalivahti ehtii siihen. Mitä pienempi aikamarginaali *m*, sitä suurempi vuoto. Lähellä maaliviivaa osittainen torjunta jatkaa helpommin maaliin, ja ulos tulleen maalivahdin ohi pääsee läheltä myös jalkojen välistä.

**5.4 Puolustajien varjot ja paine.** `α_d = arctan(r_d / s_d)`, `σ_p → σ_p·g(r)`, `g(r) = 1 + k_i·1,87·(e^(−r/0,6 m) − e^(−2,7 m/0,6 m))`, `k_i = 1 − 0,5·(i_p − 0,35)`, `r = min(r_vapaa, lähin puolustaja)`, `r_vapaa = max(5 m·(1 − paine), 0,1 m)`. Jokainen puolustaja peittää laukojan silmin kulmavälin, josta hän pysäyttää osuuden *q*_d. Lähellä oleva puolustaja peittää suuren kulman, ja laukoja tähtää varjojen ohi. Paine on lähimmän vastustajan etäisyys *r*: kyljessä kiinni (0,1 m) keskitasoisen laukojan hajonta kasvaa 2,6-kertaiseksi, puolen metrin päästä 1,8-kertaiseksi ja yli kahden metrin päässä vaikutus on pieni. Sijoitusäly ei muuta vapaata tilaa vaan pienentää paineen haittaa kertoimella *k*_i (arvio).

**5.5 Tähtäys ja hajonta.** `P_laukaus = V · Σᵢ εᵢ · [Φ((bᵢ − μ)/σ_tot) − Φ((aᵢ − μ)/σ_tot)]`. Maalin näkökulma jakautuu väleihin: vapaa maali, maalivahdin vyöhykkeet ja puolustajien varjot. Laukoja valitsee suunnan μ, joka tekee summasta suurimman. Toteutunut suunta vaihtelee normaalijakauman mukaan (suuntahajonta σ_p), ja *V* on todennäköisyys alittaa rima suoraan tai pompun kautta (5.6).

**5.6 Korkeus: kaari, pomppu ja rima.**

```
sin β = (z − r + g·t_f²/2) / (v₀·t_f),   β ~ N(β_a, σ_β)
z_a = max(r, 0,175 m + 0,18·(d − 16 m)),   σ_β = √((k_v·σ)² + (σ_z / (v₀·t_f))²)
V = (1 − q(d)) · Φ((β_H − β_a) / σ_β),   q(d) = 0,0017 + 0,135·e^(−d/8 m)
v_z → −e·v_z maahan osuessa,   e = 0,6
```

Jalka osuu palloon keskeltä tai alta, joten pallo lähtee lähes aina ylöspäin. Rata on paraabeli, jonka lentoaika *t*_f tulee ilmanvastuksesta (5.2). Kulma β, jolla pallon keskipiste (säde *r* = 0,11 m) on maaliviivalla korkeudella *z*, saadaan heittoliikkeestä. Maahan osuva pallo pomppaa: pystynopeus kääntyy ja kertautuu restituutiolla *e* = 0,6 (FIFAn tekonurmivaatimus: kahdesta metristä pudotettu pallo nousee 0,60–0,85 m, joten *e* = √(*h*/2 m) ≈ 0,55–0,65). Alaspäin potkaistu pallo kimpoaa heti jalan juuressa. Pompun jälkeen pallo jää matalaksi (25 metristä maaliviivalla enintään noin puoli metriä), joten pomppulaukaus alittaa riman aina ja *V* saadaan suljetussa muodossa. Osuus *q*(*d*) epäonnistuu ja lentää korkealle, useimmin läheltä.

Kuusi pystysuunnan vakiota on sovitettu 21 548 jalkalaukauksen loppukorkeuteen (StatsBombin `end_location`-korkeus viidessä luokassa, skripti `analyysi/pysty.py`): tähtäyskorkeus *z*_a (maata pitkin alle 16 metristä, sitten +0,18 m metriä kohti), pystyhajonnan suhde vaakahajontaan *k*_v = 0,45, lisähajonta σ_z = 0,58 m ja taivaalle lähtevien osuus *q*(*d*). Tähtäys maalin puoliväliin (1,22 m) kaikilta etäisyyksiltä hylättiin: häviö 1,554 vastaan 1,514 (vertailuna pelkkä korkeusluokkien jakauma 1,541). Data vahvistaa epäsymmetrian: 22–27 metristä riman yli 34 % ja maata pitkin (alle 0,3 m) 21 %, mutta 11–14 metristä 17 % ja 34 %. Kuva 3 näyttää saman 25 metrin laukauksen kolmesta suunnasta. Päätyrajan pystytaso on mittausseinä ja samalla kuvataso, joten seinän pisteet ovat samat mistä tahansa katsottuna; maa ja radat piirretään perspektiivissä silmästä, joka on 10 m laukojan takana ja 5 m korkealla. 3.1: seinän pisteet, pomppukohdat maassa ja hajontaellipsien jatke maassa litistyneenä viuhkana (viimeiset 10 m ennen päätyrajaa näkyvät 2 m korkuisena kaistana). 3.2: idealisoidut radat janoina, laukaisupiste → mittauspiste tai laukaisupiste → pomppu → mittauspiste. Ilman kierrettä rata kulkee ylhäältä katsottuna sektoriviivaa, joten vinoon lähtenyt pallo pomppaa myös vinoon; laukojan omasta silmästä tätä ei näkisi, koska rata on silmän kautta kulkevassa pystytasossa. 3.3: samat janat ja ensimmäiset maakosketukset ylhäältä. Pompun jälkeen pallo nousee noin puoleen peilikuvan korkeudesta, ja aikaisin pompannut vierii (lähes kolmannes pomppulaukauksista). Kuva 4 piirtää samat laukaukset todellisemmin: paraabeli, pomput, kierre (Magnus-voima) ja kimmoke puolustajasta, ja janat edelleen katkoviivoina. Kierre, lepatus ja kimmokkeet ovat mallissa karkeistettuja: ne näkyvät hajontoina σ_p ja σ_z, blokin varmuutena q_d ja sattumien pohjana p₀. 25 metristä 45 % lentää riman yli, 20 % alittaa riman suoraan ja 35 % pomppaa ennen päätyrajaa.

Aiempi versio laski pompun peilikuvamenetelmällä. Se oli väärin: peilikuvassa pallo suuntautui maahan yhtä usein kuin ylös, painovoima vetää palloa alas myös pompun jälkeen, ja pompussa katoaa energiaa. Puskuille *V* on edelleen kulmasääntö `Φ(0,6·arctan(H/d)/(0,7σ))`.

**5.7 Vippaus (lob).** Pallo nostetaan kaarella ulos tulleen maalivahdin yli. Vippaus onnistuu, jos maalivahti ei ehdi perääntyä viivalle ennen kuin pallo putoaa. Kierrettä malli ei tunne.

**5.8 Tyhjä maali, laukauksen kolmio ja käsisääntö.** `P_laukaus = w·P_maalivahti + (1 − w)·P_tyhjä`, `w = max(0, 1 − s⊥/4 m)`. Maalivahdin vaikutus hiipuu neljän metrin matkalla laukauksen kolmion ulkopuolella ja katoaa pallon takana. Yli puoli metriä rangaistusalueen ulkopuolella maalivahti on kenttäpelaaja ilman käsiä.

**5.9 Sattuma ja kantama.** `p₀ = 0,051 · e^(−d/11,0 m) · e^(−(Δy/15 m)²) · Φ((R_max − d)/5 m)`, `R_max = L·ln(1 + (0,85·v_p)²/(gL))`. Kimmokkeet ja virheet antavat pienen pohjan, joka on suurin maalin edessä. Kantama katkaisee kaukaiset vedot: keskitasoisella laukojalla (28 m/s) se on 43 m.

**Tilannevalinnat** kytkeytyvät samoihin suureisiin. Esimerkiksi pusku kasvattaa hajontaa, hidastaa palloa ja lyhentää kantaman 14,0 metriin. Vapaapotku poistaa puolustajat vetolinjalta mutta lisää muurin. Paineen säädin asettaa vapaan tilan viidestä metristä 0,1 metriin.

## 6. Sovitus ja arviointi

Vakiot on sovitettu **suurimman uskottavuuden menetelmällä**. Jokaiselle laukaukselle lasketaan mallin todennäköisyys oikeilla maalivahdin ja puolustajien paikoilla ja lähimmän vastustajan etäisyydellä, ja vakiot valitaan niin, että toteutuneet maalit ja ohilaukaukset ovat mahdollisimman todennäköisiä. Optimointiin käytettiin Nelder–Mead-menetelmää, ja vakiot pidettiin fysikaalisissa rajoissa logit-muunnoksella.

| Sovitettu vakio | Arvo | Merkitys |
|---|---|---|
| ε_max | 0,485 | vuodon yläraja (keskitasolla 0,39) |
| P0 | 0,051 | sattumien taso maalin edessä |
| P0L | 11,0 m | sattumien vaimenemismatka |
| puskun hajonta | × 1,93 | puskun suuntahajonta suhteessa jalkaan |
| puskun kantama | 14,0 m | kuinka kauas pusku kantaa |
| tyhjän maalin hajonta | × 0,83 | rauhallinen sijoitus tyhjään maaliin |
| r_d | 0,63 m | puolustajan varjon puolileveys |
| q_d | 0,72 | blokin varmuus varjossa |
| ohitus läheltä | 0,99 | ulos tulleen maalivahdin läpimeno (sallitun välin rajalla) |
| vapaapotkun hajonta | × 0,46 | vapaapotkun tarkkuus |
| paineen voimakkuus | 1,87 | kuinka paljon lähellä oleva vastustaja kasvattaa hajontaa |

**Epävarmuus (bootstrap).** Sovitus toistettiin 40 kertaa aineistoilla, joissa ottelut arvottiin takaisinpanolla (`boot_par.sh`, yhteenveto `boot_summary.py`). Välit ovat 2,5 %:n ja 97,5 %:n persentiilit. Ne ovat suuntaa antavia, koska jokainen toisto lähti koko aineiston sovituksesta ja käytti 250 Nelder–Mead-askelta. Sallitun välin rajalla oleva ohitustermi ei juuri liiku.

| Vakio | Sovitus | 95 %:n väli |
|---|---|---|
| ε_max | 0,485 | 0,393–0,522 |
| P0 | 0,051 | 0,040–0,081 |
| P0L | 11,0 m | 7,2–17,0 m |
| puskun hajonta | × 1,93 | 1,82–2,18 |
| puskun kantama | 14,0 m | 12,5–20,8 m |
| tyhjän maalin hajonta | × 0,83 | 0,64–0,93 |
| r_d | 0,63 m | 0,55–0,76 m |
| q_d | 0,72 | 0,64–0,79 |
| vapaapotkun hajonta | × 0,46 | 0,34–0,56 |
| paineen voimakkuus | 1,87 | 1,41–2,40 |

Tiukimmin data määrää puolustajan varjon, blokin varmuuden ja puskun hajonnan. Paineen voimakkuus on selvästi nollasta poikkeava, mutta sen suuruus on epävarma. Puskun kantama ja sattumien vaimenemismatka ovat löyhästi määrättyjä, koska kaukaa ammuttuja puskuja ja maaleja on vähän.

Pystysuunnan vakiot on sovitettu erikseen loppukorkeuksiin (5.6):

| Sovitettu vakio | Arvo | Merkitys |
|---|---|---|
| ZA | 0,175 m | tähtäyskorkeus 16 metristä |
| ZB | 0,180 | tähtäyskorkeuden kasvu metriä kohti |
| KV | 0,449 | pystyhajonnan suhde vaakahajontaan |
| SZ | 0,579 m | korkeuden lisähajonta (kierre, lepatus, kimmokkeet, kirjausvirhe) |
| SK0, SK1 | 0,0017, 0,135 | taivaalle lähtevien osuus q(d) = SK0 + SK1·e^(−d/8 m) |

Kokeilin myös yhteissovitusta, jossa pystysuunnan vakiot sovitettiin maaleihin yhdessä xG-vakioiden kanssa. Tähtäyskorkeuden kasvu muuttui negatiiviseksi, mikä on epäfysikaalista, joten pystysuunta sovitetaan korkeuksiin, joista se on suoraan mitattu.

Käsin on asetettu keskitasoisen laukojan arvot (σ_p = 21°, *v*_p = 28 m/s, sijoitusäly 0,35), torjunnan aikavakio τ = 1,0 s, paineen vaimenemismatka 0,6 m ja neutraali etäisyys 2,7 m. Data ei erottele niitä muista vakioista (katso *degeneraatio* kohdassa 11). Reaktioaika, syöksynopeus, restituutio ja ilmanvastus ovat fysikaalisia arvioita. Rangaistuspotkun hajonta on kalibroitu niin, että xG on 0,75 (kerroin 0,174).

**Arviointi logaritmisella häviöllä.** Parannus kertoo, kuinka paljon malli pienentää häviötä verrattuna siihen, että jokainen laukaus saa arvon 0,095.

| Malli | Parannus |
|---|---|
| Etäisyys | 10,9 % |
| Kulma | 10,4 % |
| Perusfunktio | 11,8 % |
| Simulaattori, pelkkä paikka ja laukaisutapa | 12,0 % |
| Simulaattori, todelliset maalivahdin ja puolustajien paikat | 21,1 % |
| StatsBombin xG | 21,0 % |

**Kalibrointi ryhmittäin** (toteutunut / malli):

| Ryhmä | Toteutunut | Malli |
|---|---|---|
| Puskut | 10,7 % | 10,6 % |
| Vapaapotkut | 6,4 % | 6,1 % |
| Volleyt | 10,5 % | 11,0 % |
| 16,5–22 m | 4,8 % | 4,7 % |
| Ei puolustajia lähellä | 26,4 % | 24,5 % |
| 2 puolustajaa | 6,6 % | 7,1 % |


### 6.1 Ulkoinen testi

Malli ajettiin sellaisenaan, ilman uudelleensovitusta, kuuteen turnaukseen, joita sovituksessa ei käytetty: MM 2018 ja 2022, EM 2020 ja 2024, Copa América 2024 ja Afrikan mestaruuskilpailut 2023. Niissä on 314 ottelua ja 7 509 laukausta ilman rangaistuspotkuja, ja maaliin meni 8,9 %. Etäisyys- ja kulmamallit on sovitettu vain opetusaineistoon, ja vertailukohta on vakio 0,095. Välit ovat 95 %:n bootstrap-välejä: turnausten otteluita poimittiin takaisin 1 000 kertaa, ja mallit pysyivät kiinteinä.

| Malli | Sovitusaineisto | Turnaukset | 95 %:n väli |
|---|---|---|---|
| Etäisyys | 10,9 % | 8,5 % | 6,5–10,9 % |
| Kulma | 10,4 % | 8,2 % | 5,9–10,6 % |
| Perusfunktio | 11,8 % | 9,4 % | 7,5–12,0 % |
| Simulaattori, pelkkä paikka ja laukaisutapa | 12,0 % | 10,0 % | 7,5–13,7 % |
| Simulaattori, todelliset paikat | 21,1 % | 17,8 % | 14,7–20,8 % |
| StatsBombin xG | 21,0 % | 18,7 % | 16,1–21,6 % |

Fysiikkamalli on perusfunktiota 8,4 prosenttiyksikköä parempi (väli 5,8–9,7), ja StatsBomb on fysiikkamallia 0,9 yksikköä edellä (väli 0,0–2,0). StatsBombin malli ei välttämättä ole aidosti ulkopuolinen, koska sen opetusaineistoa ei ole julkaistu.

| Turnaus | Laukauksia | Maaleja | Perusfunktio | Simulaattori | StatsBomb |
|---|---|---|---|---|---|
| MM 2018 | 1638 | 8,2 % | 10,6 % | 14,6 % | 16,9 % |
| MM 2022 | 1430 | 10,6 % | 12,5 % | 22,1 % | 21,5 % |
| EM 2020 | 1234 | 9,9 % | 10,0 % | 19,4 % | 22,3 % |
| EM 2024 | 1304 | 7,5 % | 6,8 % | 15,8 % | 16,4 % |
| Copa América 2024 | 741 | 8,5 % | 5,1 % | 16,8 % | 17,5 % |
| Afrikan MM 2023 | 1162 | 8,4 % | 7,8 % | 17,1 % | 16,2 % |

**Kalibrointi turnauksissa** (simulaattori todellisilla paikoilla):

| Ryhmä | Laukauksia | Toteutunut | Malli | StatsBomb |
|---|---|---|---|---|
| Puskut | 1370 | 10,0 % | 10,3 % | 11,1 % |
| Vapaapotkut | 319 | 4,4 % | 6,1 % | 3,9 % |
| Volleyt | 1413 | 9,3 % | 11,3 % | 10,6 % |
| Alle 11 m | 2125 | 17,6 % | 19,3 % | 18,0 % |
| 11–16,5 m | 1835 | 9,6 % | 10,2 % | 10,0 % |
| 16,5–22 m | 1716 | 4,2 % | 4,4 % | 4,7 % |
| Yli 22 m | 1833 | 2,6 % | 2,3 % | 2,2 % |
| Ei puolustajia lähellä | 969 | 23,7 % | 23,6 % | 22,9 % |
| 2 puolustajaa | 1869 | 6,8 % | 7,6 % | 7,1 % |
| Lähin vastustaja alle 1 m | 1283 | 9,2 % | 9,9 % | 10,8 % |

Vapaapotkuissa malli on liian optimistinen (ero noin 1,3 keskihajontaa). Kymmenyksittäin ennuste ja toteuma eroavat yhdeksässä ryhmässä enintään 1,7 prosenttiyksikköä, mutta ylimmässä kymmenyksessä malli antaa 39,6 % ja toteuma on 36,5 %. Sama näkyy alle 11 metrin ja volleylaukauksissa: uusi pystymalli päästää matalat lähilaukaukset riman alle varmemmin kuin vanha kulmasääntö, ja turnauksissa se on hieman liian optimistinen.

## 7. Keskeiset tulokset

- **Paine riippuu siitä, miten se mitataan.** Kyllä tai ei -merkintänä paineen oma vaikutus katoaa, kun puolustajien paikat otetaan mukaan. Lähimmän vastustajan etäisyytenä mitattuna se palaa, mutta vain lähellä: kyljessä kiinni oleva vastustaja kasvattaa hajonnan 2,6-kertaiseksi ja pudottaa maaliodottamaa 59 %, mutta kahden metrin jälkeen vaikutus on pieni.
- **Puolustaja on 1,3 metrin varjo**, joka pysäyttää lähes kolme neljästä siihen osuvasta laukauksesta. Rangaistusalueen rajalta keskeltä veto on ilman puolustajia 0,108 ja yhden puolustajan kanssa 0,057.
- **Paras maalivahdin paikka on 0,7–1,0 metriä viivan edessä** keskeltä ammuttuja 11–16,5 metrin vetoja vastaan. Kauempaa ammuttua vetoa vastaan kannattaa tulla pidemmälle.
- **Yksilöt ratkaisevat.** Samasta paikasta veto on Rayaa vastaan 0,048 ja divarin varamaalivahtia vastaan 0,095.
- **Tyhjä maali ei ole varma.** Datassa 55 % laukauksista, joissa maalivahti oli yli kolme metriä pallon takana, meni sisään.
- **Kaukolaukauksista yli kolmannes on mallissa sattumaa.** 25 metristä 0,005 kokonaisarvosta 0,014 tulee sattumien pohjasta.
- **Kaukaa pallo nousee, läheltä se tulee maata pitkin.** 22–27 metristä 34 % laukauksista ylittää riman ja 21 % tulee maata pitkin, 11–14 metristä 17 % ja 34 %. Pompun jälkeen pallo jää matalaksi, joten ilmassa päätyrajan ylittää 25 metristä 65 % ja ennen sitä pomppaa 35 %.
- **Syöttö kannattaa useammin kuin luulisi.** Rangaistusalueen rajalta (0,057) kannattaa syöttää kuuden metrin päähän vapaalle kaverille, jos syöttö onnistuu yli 15 %:ssa.
- **Tulos kestää uuden aineiston.** Kuudessa turnauksessa, joita sovituksessa ei käytetty, fysiikkamalli pienensi häviötä 17,8 %, perusfunktio 9,4 % ja StatsBomb 18,7 %.
- **Hyvä sovitus ei todista mekanismia.** Tarkempi laukoja ja vuotavampi maalivahti selittävät samat maalit lähes yhtä hyvin.

## 8. Rajoitukset

- Vakiot on sovitettu yhteen seurakauteen. Ulkoinen testi on tehty turnauksilla, jotka ovat pieniä ja erilaisia kuin sarjaottelut. Toista seurakautta malli ei ole vielä kohdannut.
- Vapaapotkuissa malli oli turnauksissa liian optimistinen (6,1 % vastaan toteutunut 4,4 %), ja parhaiden paikkojen kymmenyksessä 39,6 % vastaan 36,5 %.
- Korkeus on mukana vain rimaehtona: maalivahti torjuu yhtä hyvin ylä- ja alakulmaan, tähtäyskorkeus on sovitettu suora viiva (noin 29 metristä alkaen riman yläpuolella) ja lähtökulma normaalijakautunut. Kierrettä ja tuulta ei ole, ja pompussa vaakanopeus säilyy.
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

1. **Erillinen testiaineisto.** Turnaustesti on tehty (kohta 6.1). Seuraava askel: sovita malli kolmeen sarjaan ja testaa neljännellä, tai käytä ristiinvalidointia. Jaa aineisto otteluittain, ei laukauksittain, koska saman ottelun laukaukset riippuvat toisistaan. *Mittari:* testiaineiston parannus verrattuna 21,1 %:iin.
2. **Epävarmuus näkyviin.** Ensimmäiset 40 bootstrap-toistoa on tehty (kohta 6). Arvo otteluita takaisinpoiminnalla satoja kertoja ja aloita jokainen sovitus eri lähtöarvoista. Anna jokaiselle vakiolle ja parannukselle 95 %:n luottamusväli. Piirrä häviö aikavakion τ ja paineen vaimenemismatkan funktiona (profiiliuskottavuus). *Mittari:* kuinka leveitä välit ovat ja mitkä vakiot data todella määrää.
3. **Kalibrointi ja jäännöskartta.** Piirrä luotettavuuskäyrä: jaa laukaukset kymmeneen ryhmään ennusteen mukaan ja vertaa ennustetta toteutuneeseen. Laske jokaiseen ruutuun standardoitu jäännös (havaittu − malli) / √(n·p·(1 − p)). *Mittari:* missä ruuduissa jäännös on yli 2, eli missä fysiikka puuttuu.
4. **Kaksiulotteinen maalivahti.** Pystysuunta on nyt mukana rimaehtona (5.6). Seuraava askel: anna maalivahdin ulottuvuuden riippua korkeudesta (yläkulmat vaikeampia kuin alakulmat) ja anna laukojan valita tähtäyskorkeus tilanteen mukaan. Kokeile myös vinoa lähtökulman jakaumaa. *Mittari:* korjaantuuko ylimmän kymmenyksen ja lähilaukausten ylioptimismi, ja pieneneekö ylärajalle asettuneen ohitustermin tarve?
5. **Pelaajakohtaiset arvot.** Kerää useampi kausi ja sovita jokaiselle laukojalle oma σ_p hierarkkisella bayesiläisellä mallilla, joka kutistaa vähäisten havaintojen arvot kohti keskiarvoa. *Mittari:* kuinka monta laukausta tarvitaan, jotta huippulaukojan hajonta erottuu keskitasosta, ja vastaavatko sivun pelaajaprofiilit dataa?
6. **Maalivahtien torjuntakyky.** Sovita ε_max maalivahtikohtaisesti niistä laukauksista, jotka menivät kohti maalia. Vertaa laukauksen jälkeiseen xG:hen (*post-shot xG*). *Mittari:* toistuuko maalivahdin ero kaudesta toiseen, vai onko se satunnaisvaihtelua?
7. **Kimmokemalli sattuman tilalle.** Mallinna, kuinka suuri osa puolustajan varjoon osuneista laukauksista kimpoaa maaliin. Käytä StatsBombin blokkausmerkintöjä. *Mittari:* pieneneekö sattumien pohja *p*₀, ja saavatko kaukolaukaukset fysikaalisen selityksen?
8. **Mallivertailu.** Poista vippaus, maaliviivan läpimeno ja ohitus läheltä yksi kerrallaan ja sovita malli uudelleen. Vertaa uskottavuusosamäärätestillä tai informaatiokriteereillä (AIC, BIC). *Mittari:* mitkä termit ansaitsevat paikkansa, kun parametrien määrästä rangaistaan?
9. **Liikkuvat pelaajat.** Käytä StatsBomb 360 -aineistoa tai seurantadataa, jossa näkyy pelaajien liike. Anna puolustajan varjon kasvaa ajan myötä ja maalivahdin asettua todelliseen paikkaansa. *Mittari:* toistuuko tulos, että paine vaikuttaa vain alle kahden metrin päästä, ja riippuuko vaikutus painostajan suunnasta?
10. **Ennakkoon kirjatut ennusteet ja toisto.** Kirjaa hypoteesit ennen uuden datan katsomista: paras syvyys 0,7–1,0 m, paineen vaikutus vain alle kahden metrin päästä, varjon leveys noin 1,3 m, tähtäyskorkeus maata pitkin alle 16 metristä. Testaa ne uudella kaudella tai sarjalla, kirjoita lyhyt raportti (menetelmät, tulokset, rajoitukset) ja julkaise koodi. *Mittari:* säilyvätkö tulokset aineistossa, jota ei käytetty mallin rakentamiseen?
11. **Kierre.** Lisää potkutekniikkaan kaartokyky: laukoja valitsee suoran tai kaartuvan radan, joka kiertää puolustajan varjon tai muurin mutta hidastaa palloa ja kasvattaa hajontaa. *Mittari:* korjaantuuko vapaapotkujen ylioptimismi?

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
- **Restituutiokerroin:** osuus pystynopeudesta, joka säilyy pompussa. Kun *e* = 0,6, pallo nousee 36 % pudotuskorkeudesta.
- **Peilikuvamenetelmä:** rajapinnan vaikutus korvataan peilikuvalla. Aiempi versio laski pompun näin, mutta painovoiman ja energiahäviön takia se ei ole pompulle tarkka. Kuvassa 3 pomppukohdat on piirretty maan alle renkaina, ja viiva näyttää, kuinka paljon peilikuvaa matalammalle pallo todella nousee.
- **Vuoto:** todennäköisyys, että pallo menee maaliin, vaikka maalivahti ehtii siihen.
- **Amplitudi ja Bornin sääntö:** kvanttimekaniikassa reitillä on kompleksinen amplitudi, ja todennäköisyys on amplitudien summan itseisarvon neliö.
- **Hilbertin avaruus:** vektoriavaruus, jonka alkiot ovat kvanttitiloja.
- **Interferenssi ja dekoherenssi:** amplitudit voivat vahvistaa tai kumota toisensa. Kun reittitieto karkaa ympäristöön, interferenssi katoaa (dekoherenssi).
- **Ensemble-tulkinta:** Ballentinen muotoilema tulkinta, jonka mukaan kvanttitila kuvaa samoin valmisteltujen järjestelmien joukkoa. Minimaalinen versio (Home ja Whitaker 1992) ei väitä, että yksittäisellä hiukkasella olisi valmiiksi määrätty rata. Se muistuttaa xG:n logiikkaa, mutta joukon todennäköisyyksiä ei voi selittää paikallisilla tuntemattomilla yksityiskohdilla.
- **Piilomuuttuja, Bellin epäyhtälö ja kontekstuaalisuus:** piilomuuttuja olisi tuntematon tekijä, joka ratkaisee tuloksen etukäteen. Bellin epäyhtälöitä rikkovat kokeet sulkevat pois paikalliset piilomuuttujat, ja Kochenin–Speckerin lause osoittaa, ettei arvoja voi antaa mittausyhteydestä riippumatta. Epälokaalit piilomuuttujat (Bohmin mekaniikka) ovat mahdollisia.

## 12. Toistettavuus

Kansiossa `analyysi/` ovat skriptit, joilla kirjoituksen luvut voi laskea alusta. Ne vaativat Python 3:n ja Node.js:n. Pystysuunnan sovitus tarvitsee lisäksi numpy- ja scipy-kirjastot.

| Tiedosto | Tehtävä |
|---|---|
| `fetch.py` | Hakee yhden kilpailun laukaukset tilannekuvineen StatsBomb Open Datasta |
| `features.py` | Laskee mallin piirteet: paikka metreinä, maalivahti, puolustajat, lähin vastustaja |
| `model.js` | Malli, sama kuin sivun simulaattorissa |
| `fit.js` | Sovittaa 11 vakiota (Nelder–Mead), valinnaisesti bootstrap-otokseen |
| `pysty.py` | Sovittaa pystysuunnan kuusi vakiota loppukorkeuksiin ja tulostaa korkeusluokat etäisyyksittäin |
| `evaluate.js` | Arvioi mallit opetus- ja testiaineistossa sekä laskee kalibroinnin ja bootstrap-välit |
| `boot.sh`, `boot_par.sh` | Toistaa sovituksen otteluittain takaisinpoimituilla aineistoilla (peräkkäin tai rinnakkain) |
| `boot_summary.py`, `boot_summary.json` | Bootstrap-toistojen yhteenveto: vakioiden 95 %:n välit |
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
- FIFA (2006). *FIFA Quality Concept: Handbook of Requirements for Football Turf*. Zürich: FIFA. (Pystysuuntainen pomppu kentällä 0,60–0,85 m.)
- FIFA (2015). *FIFA Quality Programme for Football Turf: Handbook of Test Methods*. Zürich: FIFA. (Pudotuskorkeus 2,00 m.)
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

- **29.9.2026 (2):** kuva 3 kolmena näkymänä perspektiivissä (mittausseinä ja maa, radat janoina, ylhäältä) ja uusi kuva 4 todellisemmista radoista (kierre, pomput, kimmoke) sekä kritiikkikappale; pelaajaprofiileja tarkistettu (Messi, Mbappé, Palmer, Haaland, Emiliano Martínez); esimerkkilaskun kehys Arsenal–Liverpool 6.2.2027.

- **29.9.2026:** pystysuunnan fysiikka: lähtökulma, paraabelirata, pomppu restituutiolla 0,6 ja rimaehto suljetussa muodossa; kuusi pystyvakiota sovitettu 21 548 loppukorkeuteen ja xG-vakiot sovitettu uudelleen (sovitusaineistossa 21,1 %, turnauksissa 17,8 %); uusi kuva 3 (maan alle jatkuvat litistyneet hajontaellipsit, viiva pomppukohdasta pallon korkeuteen, lähikuva ja lintuperspektiivi); peilikuvamenetelmä poistettu laskusta; *torjunnan pettäminen* on nyt *vuoto*; uusi kysymys 2 (laukaista vai syöttää); kvanttivälilehden mitat nanometreinä, muuri nuhavirusten torneista; muistio LaTeX-lähdekoodina ja tutkimus- ja julkaisusuunnitelma.

- **28.9.2026 (3):** oikeiden laukausten pelitilanteet tapahtumadatasta, pelaajaprofiilit (osa valittavissa), seitsemäs laukaus (Lautaro Martínezin ohilaukaus), syöttövaihtoehto *Syöttö jalkaan*; kvanttivälilehdelle tarina virusten mikrostadionista, kuvat K1 (muuri kahdella aukolla) ja K2 (päätyraja laukojan silmin neljässä tilanteessa) sekä virusten xG-simulaattori.

- **28.9.2026 (2):** ulkoinen testi kuudella turnauksella (17,8 % vs. StatsBomb 18,7 %); jaettava tilannelinkki; kuusi finaalilaukausta simulaattoriin; analyysiskriptit kansioon `analyysi/`.

- **28.9.2026:** uusi otsikko ja kirjoittaja; välilehdet Kirjoitus, Kvanttilaukaus ja Käsitteet; lihavoidut käsitelinkit ja paluupainike; kuva 3 (laukojan näkymä päätyrajalle, pomput peilikuvamenetelmällä); kuva K1 (kvanttilaukaus kahden raon läpi); paineen säädin 0,1 metriin asti ja sijoitusälyn kerroin *k*_i; arvuutusmuotoiset kysymykset; läpinäkyvyyshuomio ja lähdeluettelot.
