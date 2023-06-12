# Dokumentering

For at dokumentationen kan vedligeholdes og bruges i vores daglige arbejde, skal den have en veldefineret struktur og et klart formål. Denne side beskriver dokumentationens formål og struktur. Dette skal ses som en guide til hvordan man dokumenterer dashboards, kuber og databaser.


# Formål med dokumentation og GitHub

- Primære formål:
  - Give **overblik og indsigt** i vores dashboards, kuber og databaser. Dokumentationen skal kunne bruges i vores daglige arbejde og til besvarelser af postkassehenvendelser.
  - Gøre os opmærksomme på **fejl og uhensigtsmæssigheder** i opbygningen af vores dashboards, kuber og databaser.
  - Dokumentere **tankegangen** bag vigtige og komplekse beslutninger, så ræsonnement ikke bliver glemt eller går tabt.
  - Give os en **konsistent** måde at dokumentere og arbejde med dashboards, kuber og databaser.
  
- Sekundære formål:
  - Hjælpe **andre i Region Hovedstaden** med at forstå opbygningen af vores kuber og dashboards.

# Hvor, hvordan og hvornår dokumenterer vi?
Alle ændringer som laves i dashboards, *CHRU_HRKube*, views samt de tabeller som kuben bygger på skal dokumenteres. Dette gælder både når man tilføjer nye temaer og når man ændrer på allerede eksisterende. Vi dokumenterer vores arbejde følgende steder.
## Power BI-filer
Dashboards og de tilhørende infobokse skal **give et overblik** over hvad der vises på en given figur, samt hvilke measures den bygger på og hvilke filtre der er blevet brugt på figuren/siden. **Når man bygger dashboardet kommer alt dette naturligt med**.

## Kode-filer (DAX, SQL, Python osv.)
I koden indsætter man **korte kommentarer** som beskriver hvad bestemte linjer eller dele af koden gør. Beskriv som udgangspunkt **hvad koden gør** (f.eks. "Tæl antal ansatte") , ikke hvordan den gør det (dette beskriver koden ofte fint selv). Ved særligt komplekse udtryk kan en mere beskrivende tekst dog være nødvendig. De mere tekniske forklaringer skal så vidt muligt inkluderes som kommentarer i koden, og ikke på wiki-siden eller andre steder. Kommentarer i koden giver et bedre overblik og gør det lettere at genbruge dele af koden på et senere tidspunkt. **Man kommenterer normalt koden samtidigt med at man skriver den.**

## Tabular model (descriptions)
Alle measures, tabeller og kolonner skal have **en kort beskrivelse**. Denne "description" kan tilføjes i Tabluar Editor og bliver en del af den semantiske model. Dette betyder at man kan se beskrivelserne når man f.eks. arbejder i PowerBI. Beskrivelserne bliver også automatisk tilgængelige på vores wiki-side, hvor de er med til at give et overblik over kuben. Beskrivelsen skal som udgangspunkt **ikke være mere end 100 tegn, og den skal slutte med "*[værdi a, værdi b, ...]*"** som angiver et par eksempler på de værdier kolonnen eller measuret returnerer. **Man skriver normalt descriptions ind samtidigt med at man definerer measures, tabeller og kolonner i kuben**.

## Diskussionsforum og Issues
Her kan man skrive **spørgsmål eller ændringsforslag** ind. Dette sikrer dels at ændringsforslag ikke bliver glemt eller går tabt, samt at det ræsonnement som ligger til grund for beslutninger vedr. dashboards, kuben og databasen bliver gemt. Ofte giver det god mening at **konvertere et ændringsforslag til et Issue**, da dette bringer flere funktionaliteter med sig. Bl.a. er det muligt at kommentere på Issues og knytte "Pull requests" op på et Issue. På denne måde får man hele historikken med, og kan let se det ræsonnement som ligger til grund for ændringer i kuben, views og wiki-siden. OBS: vær opmærksom på at **Issues der oprettes i offentlige repositories som f.eks. "dokumentation" vil være offentligt tilgængelige**.

## Versionsstyring
Alle **ændringer i CHRU_HRKube** i udvikling og produktion skal ske gennem GitHub. Dette er med til at sikre vi har et sikkert og stabilt miljø hvor flere kan arbejde samtidigt. Alle **views som har skema-navnet "*chru_cube*"** og dermed ligger til grund for vores *CHRU_HRKube* skal også versionsstyres via. GitHub. Man kan læse mere om dette under [***versionsstyring***](./internt_versionsstyring). **Versionsstyringen kan ske sideløbende med at man skriver sin kode, eller når man er klar til at implementere sine ændringer i vores fælles kuber**.

## Wiki-siden
Wiki-siden samler al vores dokumentation og giver et overblik over vores miljøer og arbejdsgange. Alle ændringer i vores dashboards, kuber og datamodel kræver at man opdaterer wiki-siden så den ikke bliver uddateret. Her er en liste over hvad der skal dokumenteres på wiki-siden, samt hvornår i arbejdsprocessen man skal gøre det.
- Beskrivelse af alle **faner og figurer** i HR Strategisk Dashboard og HR Lederdashboard. Her er information om hvad figurerne viser samt hvilke definitioner og antagelser de bygger på. Alle measures som figuren bygger på og hele filterkonteksten er også beskrevet her. Dette kan bruges til at forstå hvordan figuren er bygget op og til besvarelse af postkassehenvendelser. **Denne dokumentation laves sideløbende med at man udvikler dashboardet, eller umiddelbart efter dashboardet er færdigudviklet**.
- Beskrivelse af **"*CHRU_HRKube*" i produktion**. Dette giver et overblik over alle measures, tabeller, relationer i kuben. **Denne dokumentation skrives sideløbende med at man arbejder i kuben, eller umiddelbart efter man har færdigudviklet det givne tema**.
- Beskrivelse af **views på i produktion** med skema-navn "*chru_cube*". **Denne dokumentation skrives sideløbende med at man arbejder i kuben, eller umiddelbart efter man har færdigudviklet det givne tema**.
- Beskrivelse af tabeller og vores database. Dette giver en indsigt i hvordan tabeller er defineret og hvordan vores miljø er bygget op. **Denne dokumentation skrives sideløbende med at man tilføjer nye tabeller eller laver andre ændringer på vores database i produktion**.
- Beskrivelse af vores **arbejdsprocesser og de værktøjer** som vi bruger. Dette gælder dels brug at GitHub, wiki-siden, dokumentering og versionsstyring, men også hvordan man udvikler og arbejder med dashboards, kuber, views og tabeller. Dette er med til at sikre vi har en konsistent måde at arbejde på i alt fra navngivning af kolonner til opsætning af bogmærker i Power BI. **Denne dokumentation skrives løbende**.

# Skabeloner til dokumentation - under udvikling
Følgende skabeloner angiver hvordan dokumentationen af measures og tabeller er bygget op. Man kan tage udgangspunkt i disse når man skal skrive dokumentation ind på wiki-siden.
## Dashboards - skabelon

- Dashboards
- Skal dokumentere filtre og figurer (klar struktur, overvej vedligeholdelse + hvor der skal dokumenteres)
- FAQ ved siden af?


## Measures - skabelon
Den skal angive hvordan de bruges, hvad de returnerer/viser og beskrive vigtige overvejelser/antagelser/definitioner man skal være opmærksom på når man bruger kuben og trækker tal.
- Measures
  - Liste over alle measures indenfor temaet – ligesom for tabellerne
  - Measurenavn, returnType, Beskrivelse af measure (ikke mere end 100 tegn) med eksempel på returnValue.
  - Beskrivelse skal ind som ”description” i TabularEditor – dvs. listen kan stort set autogenereres.
  - Beskrivelse/Resume af hvert measure:
  - Vigtige informationer om measure’et. Hvad er dens funktion, hvordan bruges den, vigtige tanker/overvejelser ved opbygning/afgrænsninger i measure, eventuelle corner-cases osv.
  - Oversigt over hvor measures indgår/relaterer til hinanden.
  - Dette skal suppleres af et repository i GitHub med hele kuben og alle measures som man kan linke til. Det skal måske også suppelers med ExcelFil over hvordan measures bygger på hinanden/hvor de bruges i dashboards/hvilke der ikke bruges i dashboards.

## Tabeller - skabelon
- Tabeller
  - Beskrivelse af selve tabellen (ikke mere end 100 tegn).
  - Liste over alle kolonner (minder om SD’s dokumentation):
  - Key, Kolonnenavn, Datatype, Len, Null’s, Beskrivelse af hvad kolonnen viser (ikke mere end 100 tegn) med eksempel på værdi
  - Beskrivelse skal ind som ”description” i TabularEditor – dvs. listen kan stort set autogenereres…
  - Beskrivelse/Resume af hver tabel:
  - Vigtige informationer om given tabel. Hvad er dens funktion, hvordan bruges den, vigtige tanker/overvejelser ved dannelsen af kolonner/afgrænsning af data. Hvornår opdateres den?
  - Billede af datamodel og liste over relationer.
  - Dette skal suppleres af SQL og SAS-kode som skal være i sit eget repository på GitHub – gerne linket direkte til det her.


