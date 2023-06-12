#### Aktuel hovedansættelse
Den ansættelse som opfylder og sorterer højest på kriterierne (i nævnte rækkefølge): Er gældende dags dato; status 0, 1 eller 3; Månedslønnet; Fuldtid; Startdato. En ansat medarbejder har til alle tider en og kun en aktuel hovedansættelse. Dvs. en person kan have et timelønnet ansættelsesforhold som aktuel hovedansættelse, men kun hvis dette ikke overlapper i tid med et månedslønnet. På samme måde kan en deltidsstilling være en aktuel hovedansættelse, men kun hvis dette ikke overlapper en fuldtidsansættelse.
```
-- AktuelHovedansættelse, 07_FL_110_SD_DimAnsaettelse.sas
by cpr descending AktuelRække descending Ansat descending Månedslønnet descending Fuldtid descending start tjnr;
if first.cpr AND AktuelRække = 1 AND Ansat = 1 then AktuelHovedansættelse=1;
else AktuelHovedansættelse=0;
```
_Ikke at forveklsle med_ [**_aktuel ansættelse_**](#ansættelse-aktuel)

----------

#### Anciennitet
I SD har anciennitetsdato ikke en entydig betydning. Den kan betyde startdatoen i første ansættelse i regionen (ligesom _ansættelsesdato_), men den kan også være resultat af konverteret anciennitet fx ved skift fra deltids- til fuldtidsansættelse. Et bedre udtryk for en persons egentlige anciennitet i regionen er v_DimAnsættelse[_AnsLængdeCPR_]. 

----------

#### Anonymitetsgrænse
I alle beregninger, hvor der er risiko for at kunne identificere enkeltindivider i små populationer—og hvor dette ikke er tilladt—implementeres en anonymitetsgrænse. I praksis maskeres et resultat, hvis dette er fundet pba. et antal af individer lavere en anonymitetsgrænsen. 

> Vær opmærksom på, at anonymitetsgrænsen kan variere med tema.

----------

#### Ansættelse
Et ansættelsesforhold med status 'ansat uden løn' (0), 'ansat/genåbnet' (1) eller 'midlertidigt ude af løn' (3). Alle ansættelser er unikt kendetegnet ved en stillings-, tjeneste- og overenskomstkode, en lønklasse og afdeling. Ændring i én eller flere af disse forhold, medfører et nyt registreret ansættelsesforhold (nyt AnsættelsesID) men ikke nødvendigvis et nyt tjenestenummer. Ansættelsens varighed opgøres fra 1. dag (v_DimAnsættelse[Start]) til den sidste dag i pågældende ansættelse (v_DimAnsættelse[Slut]) begge dage inklusiv. 

----------

#### Ansættelse, aktuel
Med aktuel ansættelse henvises oftest til dét ansættelsesforhold, hvis start- og slutdato inkluderer dags dato OG har status ansat/genåbnet (1), ansat uden løn (0) eller midlertidigt ude af løn (3).
Vi vælger denne population med v_DimAnsættelse[Ansat]=J og v_DimAnsættelse[AktuelRække]=J. 
```
-- Aktuelrække, 07_FL_110_SD_DimAnsaettelse.sas
,(CASE
    WHEN today() BETWEEN START and SLUT THEN 1 ELSE 0 
  END) as AktuelRække length = 3,
```

```
-- Ansat, 07_FL_110_SD_DimAnsaettelse.sas
,(CASE  
    WHEN STAT IN ('0', '1', '3') THEN 1 ELSE 0 
  END) as Ansat length = 3,
```
_Ikke at forveksle med_ [**_AktuelHovedansættelse_**](#aktuel-hovedansættelse).

----------

#### Ansættelseslængde
I opgørelser om personalesammensætning henviser ansættelseslængde til perioden fra _ansættelsensdato_ i SD til dags dato.
```DAX
[Ansættelseslængde]=
VAR __AnsaettelsesDato =
    MAX ( 'v_DimAnsættelse'[Ansættelsesdato] )
VAR Result =
    IF (
        NOT ( ISBLANK ( __AnsaettelsesDato ) ),
        INT (
            DIVIDE (
                DATEDIFF (
                    IF ( __AnsaettelsesDato > TODAY (), TODAY (), __AnsaettelsesDato ),
                    TODAY (),
                    DAY
                ),
                365.25,
                0
            )
        )
    )
RETURN
    Result
```

----------

#### Beskæftigelsessum
Sum af ansattes beskæftigelsesdecimaler. Anvendes flere steder direkte oversat til årsværk. Vi bruger denne i beregning af sygefravær til at eliminere evt intervariabilitet mellem fuld- og deltidsansatte

----------

#### Beskæftigelsessum, gennemsnitlig
Gennemsnitlig beskæftigelsessum på udvalgte nedslagsdatoer—d. 1. i en måned. 
Muligheden for at ansatte til- og fratræder eller skifter fra fuld- til deltid midt i en måned introducerer dilemmaer, hvor vi må vælge i et kompromis imellem tunge og komplekse eller mere grovmaskede beregninger. Ét eksempel herpå er i beregning af det rullende gennemsnit af fuldtidsfraværsdage, hvor vi månedsvist d. 1. aggregerer indeværende månedens fravær relativt til beskæftigelsessum. Her antages, at beskæftigelsesdecimaler d. 1. er repræsentativ for hele perioden siden forrige nedslagsdato. 

----------

#### Deltidsansat
Alle personer i v_DimAnsættelse, som er månedslønnede og _ikke_ er fuldtidsansatte. Se også [**_fuldtidsansat_**](#fuldtidsansat).

----------

#### Ferie
Ferie er, som det præsenteres i dashboard, bredt defineret som den (rest)ferie, medarbejder har ret til at afholde. Indeholdt i beregningen er positive bidrag fra optjent feriesaldo og forventet tilskrivning samt negative bidrag fra anvendt og planlagt ferie. Se også [**_restferie_**](#restferie)

----------

#### Feriekategori
Feriekategori dækker begreberne feriesaldo, anvendt ferie, planlagt ferie og forventet tilskrivning.

----------

#### Ferietilskrivning
Forventet tilskrivning er det antalt ferietimer, som en person _forventes_ at have til afhold i hele afviklingsåret baseret på aktuel beskæftigelsesdecimal.

----------

#### Ferietimer
Registreret ved lønart 730 (ferietimer) og 752 (Ferietimer '6. uge')

----------

#### Ferietype
Med ferietype menes ordinær ferie (1. - 5. ferieuge) eller 6. ferieuge.

----------

#### Ferieår
Ferieåret opdeles i ordinær og 6. ferieuge med hver en **optjenings**- og en **afviklingsperiode**.

| **FerieType** | **Optjeningsperiode**     | **Afviklingsperiode**     |
|       -:      |             -             |             -             |
| Ordinær       | 01-09-yyyy — 31-08-yyyy+1 | 01-09-yyyy — 31-12-yyyy+1 |
| 6. ferieuge   | 01-01-yyyy — 31-12-yyyy   | 01-05-yyyy — 30-04-yyyy+1 |

----------

#### Fratrædelse
Kendetegnet ved et skift i ansættelsesstatus til enten emigreret/død (7), fratrådt (8) eller pensioneret (9) fra at have været enten ansat uden løn (0), ansat/genåbnet (1) eller midlertidigt ude af løn (3). Fratrædelsesdatoen er sidste dag i en ansættelsesperiode.

----------

#### Fravær
Fravær er defineret som registreret arbejdstid med én af lønarterne i v_DimLønartFravær[L2Code], således at 

$$ \frac{\text{antal fraværstimer}}{\text{antal planlagte timer}} \in \mathbb{R}_+ $$

I opgørelser af fravær skelner vi imellem tre kategorier: Sygefravær, barn syg og andet.

----------

#### Fraværsdag
En fraværsdag er defineret ved

$$ \frac{\text{antal fraværstimer}}{\text{antal planlagte timer}} = 1 $$

En fraværsdag er altså ikke i sig selv et udtryk for antal timers fravær, men er relativ den på dagen planlagte arbejdstid.
Se også [**_fuldtidsfraværsdag_**](#fuldtidsfraværsdag)

----------

#### Fuldtidsansat
Ansættelser kendetegnet ved
```
-- Fuldtid, 07_FL_110_SD_DimAnsaettelse.sas
,(CASE 
    WHEN BESKDEC >= 1 THEN 1 ELSE 0
  END) as Fuldtid length = 3,
```

----------

#### Fuldtidsfraværsdag
En fuldtidsfraværsdag er defineret ved sammenhængende 7,4 timers fravær svt. ét dagsværk. Vi bruger denne enhed til sammenligning på tværs i organisationen uagtet forskelle i enkeltindividers beskæftigelsesdecimal. Sygefravær på en hel 12-timersvagt vil således tælle som 
$$ \frac{ 12\text{timer} }{ 7,4\frac{\text{timer}}{\text{dag}} } \approx 1,6\text{dag}  $$

----------

#### Hændelse
Pr. 2023-01-06 defineret som  en af følgende:

| Fødselsdag | Hvert år |
| Jubilæum | Ved år: 1, 5, 10, 15, 20, 25, 30, 35 |
| Tiltræder | Når der skiftes til statuskode 0, 1, 3 efter ikke at have eksisteret eller været fratrådt |
| Fratræder | Når der skiftes til statuskode 7, 8, 9 efter at have været ansat |
| Skifter fra anden afdeling | Når der skiftes fremkommer både skifter til og fra. Der tjekkes på AfdFmt. Denne er lidt speciel, da Skifter til-hændelsen kun kan ses så længe medarbejderen fortsat er ansat på afgivende afsnit |
| Skifter til anden afdeling | Når der skiftes fremkommer både skifter til og fra. Der tjekkes på AfdFmt. Denne er lidt speciel, da Skifter til-hændelsen kun kan ses så længe medarbejderen fortsat er ansat på afgivende afsnit |
| Terminsdato | Alle terminsdatoer |
| Går på orlov | Når der skiftes til statuskode 0 eller 1 efter at have været i 3 eller omvendt for til |
| Tilbage fra orlov | Når der skiftes til statuskode 0 eller 1 efter at have været i 3 eller omvendt for til |

----------

#### Jubilæum
Alle jubilæumsdatoer i 5-årsintervaller (foruden étårsjubilæum) beregnes og betragtes som en hændelse.

----------

#### Måltal
Region H’s målsætning for fravær pr. 2023-01-20 er 11,7 dage/år.

----------

#### Månedslønnet
Ansættelser kendetegnet ved 
```
-- Månedslønnet, 07_FL_110_SD_DimAnsaettelse.sas
,(CASE 
    WHEN DEL IN ('2', '6') OR BESKDEC = 0 THEN 0 ELSE 1
  END) as Månedslønnet length = 3,
```

----------

#### Orlov
**Går på orlov**: Kendetegnet ved et skift i ansættelsesstatus _til_ midlertidigt ude af løn (3) efter at have været enten ansat/genåbnet (1) eller ansat uden løn (0).

**Tilbage fra orlov**: Kendetegnet ved et skift i ansættelsesstatus _fra_ midlertidigt ude af løn (3) til enten ansat/genåbnet (1) eller ansat uden løn (0). 

----------

#### Restferie
Til beregning af restferie—antal timers ferie til afholdelse, _der endnu ikke er planlagt_—summeres alle ferieelementer i v_FactFerie[FerieTimer] med og uden løn. Dvs. summen af feriesaldo og forventet tilskrivning fratrukket summen af anvendt og planlagt ferie

$$
\text{Restferie til afhold} = \sum_{\text{optj.start}}^{\text{i dag}} \text{feriesaldo} + \sum_{\text{i morgen}}^{\text{optj.slut}} \text{forv.tilskrivning} - \left( \sum_{\text{afv.start}}^{\text{i dag}} \text{anvendte timer} + \sum_{\text{i morgen}}^{\text{afv.slut}} \text{planlagte timer} \right)
$$

----------

#### Standardpopulation
I bredeste forstand forstås ved v_DimAnsættelse[Standardpopulation]=J, alle [**_månedslønnede_**](#månedslønnet) og ikke-eksternt finansierede ansættelser.
```
-- Standardpopulation, 07_FL_110_SD_DimAnsaettelse.sas
,(CASE  
    WHEN Månedslønnet = 0 THEN 0 
    WHEN EksterntFinansieret = 1 THEN 0 
    -- WHEN RelevantStilling = 0 THEN 0
    WHEN L1Code IN( '_S2_','0000','9007','9008') THEN 0
    ELSE 1 
  END) as Standardpopulation length = 3,
```
I praksis defineres populationer med filtre på faner evt. i kombination med filtre i beregninger (measures) og direkte på enkeltfigurer. Kriterier for at indgå i en given populationen varierer med temaet; den tidslige dimension af en given analyse; samt hvem analysen er rettet imod.

----------

#### Tiltrædelse
Kendetegnet ved et skift i ansættelsesstatus fra ukendt, emigreret/død (7), fratrådt (8) eller pensioneret (9) til enten ansat uden løn (0), ansat/genåbnet (1) eller midlertidigt ude af løn (3). Tiltrædelsesdatoen er første dag i det nye ansættelsesforhold.

----------

#### Timelønnet
Formelt defineret: "Hvis ikke månedslønnet, så timelønnet". Se også [**_månedslønnet_**](#månedslønnet).

----------

#### Årsværk
I beregninger anvendes

$$ 1924 \frac{\text{timer}}{\text{år}} = 52 \frac{\text{uger}}{\text{år}} \cdot 37 \frac{\text{timer}}{\text{uge}} = 260 \frac{\text{dag}}{\text{år}} \cdot 7,4 \frac{\text{timer}}{\text{dag}} $$

----------
