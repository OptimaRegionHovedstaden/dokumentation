# CHRU | Optima - dette skrives i README.md-filen

Vi er en sektion under enheden **Data og Digitalisering** i **Center for HR og Uddannelse (CHRU)**. Sektionen udstiller data og leverer ledelsesinformation til regionens personaleledere og topledelser i form af Power BI Dashboards. Tilmed understøtter sektionen andre dele af CHRU med dataanvendelse (intern styring, indsigter, erkendelser, mv.). Sektionen varetager også *postkassehenvendelser* internt fra hele regionen og fra eksterne parter (spørgsmål og aktindsigter fra politikere, og journalister). 
Sektionen har hovedsageligt tekniske medarbejdere med kompetencer i dataudtræk og datafremstilling og økonomimedarbejdere, samt ledelsesmedarbejdere til at understøtte disse.
<br>

<!-- PowerPoint: "Introduktion og onboarding til D&R"  -->
<center>
<iframe src="https://regionh-my.sharepoint.com/personal/stefan_sajin-henningsen_regionh_dk/_layouts/15/Doc.aspx?sourcedoc={9400f055-6ddb-4862-aaa8-e3b2389a9bad}&amp;action=embedview&amp;wdAr=1.7777777777777777" height="587" width="1000" frameborder="0"></iframe>
</center>
<br>



# Introduktion til CHRU_HRKube

## ***Kuben***
I dit arbejde får du brug for at kende og kunne arbejde med data i "**kuben**" (med kuben menes—indtil videre—CHRU_HRKube). 

I kuben processeres data fra mange forskellige kilder til en række forskellige formål. Kuben er datamodel i bl.a. 
<a href="https://flis.regionh.top.local:444/PBIReports/powerbi/L%C3%B8n%20og%20HR/HR%20Lederdashboard/HR%20Lederdashboard?RC:Toolbar=False" target="_blank">___HR Lederdashboard___</a> 
og 
<a href="https://flis.regionh.top.local:444/PBIReports/powerbi/L%C3%B8n%20og%20HR/HR%20Strategisk%20Dashboard/HR%20Strategisk%20Dashboard?RC:Toolbar=False" target="_blank">___HR Strategisk Dashboard___</a>. 
I disse implementeres vores standardiserede beregningsmetoder indenfor temaer som sygefravær, ferieafholdelse, personalesammensætning, løn, vagtplan m.fl. 
Flere temaer tilføjes løbende i takt med efterspørgsel og tilgængelige datakilder, hvorfor vi altid bestræber os på, at kuben skal være en adaptiv størrelse. Hér er din indsigt i både muligheder og begrænsninger med den nuværende model værdifuld, da vi altid gerne vil kunne tilføje nye temaer *og* samtidig bevare muligheden for at foretage vores nuværende beregninger.

På produktions- og udviklingsserverne findes data under skemaet, **chru_cube**. I Tabular Editor findes kuben under navnet **CHRU_HRKube**.

<details><summary markdown="span">Kuben pr. 2023-01-30</summary>
 Dette er er overbliksbillede på dagen over tabeller inkludert i kuben. Det er ikke fyldestgørende, men giver en ide om, hvordan tabeller tilføjes temavis i takt med, at vi løbende inkluderer flere datakilder.
 <center>
  <img src="Images/erd/erd_pbi_chru_hrkube_labels.png" height="480" width="800" onmouseover="CHRU_HRKube, 2023-01-30" style="vertical-align:middle"/>
 </center>
</details>
<br> 

Som introduktion til kuben kan anbefales at gennemgå materialet hér på siden ét tema ad gangen. Husk dog, at denne data er processeret til brug i datamodellen, hvorfor det er en nødvendighed, at du også har indblik i rådata fra fx Silkeborg Data (**SD**). 
Du kan med fordel prøve at bygge din egen version af kuben i Power BI; tabel for tabel; measure for measure; figur for figur. 

Til hvert tema findes små **øvelser**, hvor du kan testen din viden. Du vil herigennem få lidt erfaring med datatræk fra både rådata og kuben og få indblik i nogle af de datatransformationer, som må foretages, før vi kan foretage beregninger og analyser.
<br>



### Tabeller

I grove træk falder al data i kuben indenfor kategorierne

| **Grunddata** | **Temaespecifik data** | **Hjælpetabeller** | **Infotabeller** |
 
- Med **grunddata** menes den data, som er fællesmængde på tværs af temaer, uanset om der beregnes på sygefravær, ferieafholdelse eller andet. I grunddata indgår:
  - **Stamdata** er personaledata, organisations-, stillings- og lønarthieraki, tidstabel mm. 
  - **Brugerstyring** er data om personales brugerroller, som er bestemmende for hvilke data, brugere af vores produkter må se. Det er essentielt at forstå, [hvordan brugerstyring er implementeret](./data_brugerstyring) for at sikre, at denne også virker på tilføjelser i kuben. 
- **Temaspecifik data** anvendes specifikt til beregning på fx sygefravær, ferieafholdelse eller personalesammensætning. Af screenshottet herover ses, hvordan vores data groft er grupperet i temaer.

Derudover findes en række øvrige tabeller, herunder:
- Hjælpetabeller er **tally**- og **slicer**-tabeller. Disse bruges til definereing af intervaller (fx aldersintervaller), grupperings-, sorterings- og filtreringsmuligheder
- Info er data som fx dato på **dataleverancer** og **servicemeddelelser** til brugere af dashboard om nye opdateringer eller tilføjelser
<br>



### Measures
Via measures implementeres vores standardiserede beregningsmetoder. De er grupperet temavis. I gruppen \__Diverse_ indgår beregninger på stamdata og dette kan være et godt sted at starte med at skabe overblik over kuben. Foruden indblik i de mere centrale tabeller vil du hér se eksempler på, hvordan viden om stamdata er essentielt for at kunne definere fx hvilken personalegruppe, der skal indgå i en given beregning; hvordan dette kan variere fra tema til tema; hvordan antallet af personer, der indgår i en beregning, er afgørende for, om et resultat nødvendigvis skal anonymiseres mm.

Andre measures—lokaliseret i mapperne, \__Farver_ og \__Tekster_—bruges til kontrol af layout på dashboards; Farvetemaer, dynamiske akselængder og tekstetiketter, meddelelser, kolonnebredder mm. 



# Software
Følgende software er en forudsætning og kan findes i <a href="https://softwarecentral.regionh.top.local/Shop" target="_blank">Softwareshoppen</a>. 

Hav altid seneste version af Power BI Desktop installeret for at sikre nyeste og kompatibel funktionalitet med rapportserver. For versioner af øvrig software spørg en kollega, hvad de bruger.

- Microsoft SQL Server Management Studio
- Power BI desktop
- SQL Server Data Tools Bundle
  - Dax Studio
  - Tabular Editor
<br>



# Data

<!-- PowerPoint: "Data.pptx"  -->
<center>
<iframe src="https://regionh-my.sharepoint.com/personal/stefan_sajin-henningsen_regionh_dk/_layouts/15/Doc.aspx?sourcedoc={1eabb8b8-ee27-4f6b-a998-091ce9ca0872}&amp;action=embedview&amp;wdAr=1.7777777777777777" height="587" width="1000" frameborder="0"></iframe>
</center>


<!-- Embed iFrame. word-doc: "Guide til bestilling af adgange.docx" på OneDrive-->
{::options parse_block_html="true" /}
<details><summary markdown="span">Guide til bestilling af dataadgange</summary>
<center>
<iframe src="https://regionh-my.sharepoint.com/personal/stefan_sajin-henningsen_regionh_dk/_layouts/15/Doc.aspx?sourcedoc={c652f92d-8025-4f11-9b4c-3e0f0e0dadba}&amp;action=embedview&amp;wdEmbedCode=0&amp;wdPrint=0&wdToolbar=FALSE" height="730" width="1000" frameborder="0" seamless="yes"></iframe>
</center>
</details>
{::options parse_block_html="false" /}
<br>



<!-- Embed iFrame. PowerPoint: "SQL-kursus.pptx" på OneDrive-->
{::options parse_block_html="true" /}
<details><summary markdown="span">Slides til SQL-kursus</summary>
<center>
<iframe src="https://regionh-my.sharepoint.com/personal/stefan_sajin-henningsen_regionh_dk/_layouts/15/Doc.aspx?sourcedoc={ee7ec7a1-d13c-4855-a459-c1717f9aa646}&amp;action=embedview&amp;wdEmbedCode=0&amp;wdPrint=0&wdToolbar=FALSE" height="587" width="1000" frameborder="0" seamless="yes"></iframe>
</center>
</details>
{::options parse_block_html="false" /}
<br>


<!-- ØVELSE -->
{::options parse_block_html="true" /}
<details><summary markdown="span">**ØVELSE - KONTROL AF DATAADGANGE** <img src="Images/icons_ref/icon_git.png" height="35" width="35"></summary>

> - Følg <a href="https://github.com/DataOgDigitalisering/FortroligInformation/blob/main/Exercises/ex_dataadgange.sql" target="_blank">**dette link til SQL-script**</a>.
> - Åbn og eksekver scriptet i SQL Server Management Studio. Kørslen kan tage >20 minutter og returnerer en tabel, der beskriver dine adgange. Spørg en kollega om du har de adgange, du har brug for.

</details>
{::options parse_block_html="false" /}


