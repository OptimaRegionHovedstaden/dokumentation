# Generelt

##	Nomenklatur
Om konventioner for navngivning af tabeller og measures. 


### Tabeller
- Navngives som fx v_DimAnsættelse
- Skabelon: [tabeltype]+[\_]+[Formål]+[BeskrivendeNavn]
- **Views** indledes med __v\___ 
  - Alt *efterfølgende* skrives i camelCase (**S**tort**B**egyndelsesbogstav)
  - **Formål**: Dim, Fact, Security, Info, Slicer, Tally.
  - **Beskrivende navn** er entydig(e) og letforståelig(e) *substantiv(er)*. (Gerne noget der minder om rådatatabellens oprindelige navn hvis viewet er baseret på en sådan). Sammensatte ord skrives i camelCase

- **Tabeller** navngives som views. [Formål]+[**B**eskrivende**N**avn]. Fx DimLønart
  - __v\___ udelades

- **Kolonnenavne** er entydige og letforståelige *substantiver*
  - camelCase
  - Disse felter udfyldes i Tabular Editor, hvis ikke de er pre-udfyldt:
    - Data Type
    - Description
    - Key


### Calculated columns
  - Undgå så vidt muligt datatransformation i Tabular Editor. Det giver bedre overblik at have samlet i SQL.
    - (Flyt evt nedenstående til views og brug en mere robust metode til anonymisering:)
      - v_DimAnsættelse[TjnrAnonymiseret]
      - v_DimPerson[NavnAnonymiseret]   


### Stored procedures
  - Navngives kort og præcist beskrivende fx 'DanskeHelligdage'
  - Brug så vidt muligt verber til at beskrive procedurens *funktion*
  - camelCase

- æ, ø, å tilladt


### Measures
- Navngives fx [Fravær - vægtede fuldtidsfraværsdage]. 
- Skabelon: [tema - beskrivende og letforståelig tekst]
  - (ikke nødvendigvis camelCase)
- Measures grupperes i temaspecifikke mapper
  - Enkelte basis-measures placeres i mappen _Diverse_, hvis de bruges på tværs af temaer. Fx [Antal fuldtidsansatte] og [FilterSlicer]
- æ ø å tilladt
- Ikke alle measures er navngivet efter denne konvention. Ved tvivl se mappen _Sygefravær_
- Disse felter udfyldes i Tabular Editor, hvis ikke de er pre-udfyldt:
  - Description
<br>



# Power BI

## Generelt
- Om brug af bookmarks. Navngivning, sektioner, grupperinger, lag mm. 
  - Farvetema (brug af measures). Hvor?
  - Conditional formatting
  - Akser. Min/max-værdier vha measures. Hvor?
  - Kolonnebredde=0
  - Covers. Hvor og hvorfor?
- Link til tabs. Ikke faner. (I lederdashboard). Begrund.


## Farvetema
<!-- Embed iFrame. PowerPoint: "One pager - Design guidelines til rapporter i FLIS" på OneDrive-->
{::options parse_block_html="true" /}
<details><summary markdown="span">One pager — Design guidelines til rapporter i FLIS</summary>
<center>
<iframe src="https://regionh-my.sharepoint.com/personal/stefan_sajin-henningsen_regionh_dk/_layouts/15/Doc.aspx?sourcedoc={89bc13a3-2f00-4dec-a49c-49033d194d1a}&amp;action=embedview&amp;wdAr=1.7777777&showNavigation=FALSE&wdStart=18&wdEnd=21" width="1000" height="588" frameborder="0" seamless="TRUE" start="18" end="21"></iframe>
</center>  
<br>
</details>
{::options parse_block_html="false" /}




#	Opgaver og ansvar

**Aftaler for ændringer i CHRU_HRKube:**
- Roller. Hvem gør/har ansvar for hvad?
  - SQL, Dax, Git, dok
  - Intervaller
 

**Kontrol-scripts:**
- Til hvad? Afdæk behov


**Oprydning:**
- Hvordan implementerer vi vedtaget nomenklatur?
- Prioriter. Hvad kan vi leve med?
  - performance vs æstetik
  - slette ubrugte tabeller/kolonner vs ændre æ ø å 




# Gamle noter som gemmes til senere
- Overvej hvor/hvad vi kan trække ift. versionsstyring/vedligeholdelse:
- SSMS: 
  - Database: view-definitioner, oversigt over tabeller og views, hvor de bruges osv.
  - Kuben: billede af model og relationer – Nicolai viste dette
- Tabular Editor
  - Hvordan tabeller og measures bygger på hinanden – Nicolai viste Excel-dok
- Power BI
  - Hvor measures bruges, hvilke der ikke bruges osv. – Nicolai nævnte kort at dette (måske…) var en mulighed



- Vigtigt med afsnit om hvordan man bygger nye temaer op, så vi navngiver konsistent osv.
- Vigtigt at have et sted hvor man beskriver hvordan man filtrerer på stilling og DimOrganisation (til folk som skal bygge nye dashboards f.eks.)

