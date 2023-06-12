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

# Brugerstyring

<!-- Embed iFrame. pptx: ERD_Brugerstyring" på OneDrive-->
<details><summary markdown="span">Datamodel</summary>
<center>
<iframe src="https://regionh-my.sharepoint.com/personal/stefan_sajin-henningsen_regionh_dk/_layouts/15/Doc.aspx?sourcedoc={643396fc-99fc-401a-ac2e-c6378e2a7317}&amp;action=embedview&amp;wdAr=1.7777777&showNavigation=FALSE&wdStart=18&wdEnd=21" height="474" width="800"  frameborder="0" seamless="TRUE"></iframe>
</center>
</details>  
<br>



<!-- Embed iFrame. word-doc: Brugerstyring.docx" på OneDrive-->
<center>
<iframe src="https://regionh-my.sharepoint.com/personal/stefan_sajin-henningsen_regionh_dk/_layouts/15/Doc.aspx?sourcedoc={0e624a26-13b0-4f1c-8729-b16bf20cb610}&amp;action=embedview&amp;wdEmbedCode=0&amp;wdPrint=0&wdToolbar=FALSE" height="1120" width="800" frameborder="0" seamless="yes"></iframe>
</center>
<br>



<!-- ØVELSE -->
{::options parse_block_html="true" /}
<details><summary markdown="span">**ØVELSE - BRUGERSTYRING** <img src="Images/icons_ref/icon_git.png" height="35" width="35"></summary>

> - Hvem er din sektionsleder og hvilke(n) rolle(r) er denne tildelt i SD? 
> - På hvilket organisatorisk niveau (NY-niveau) er disse gældende?
> - Hvilke SD-rolle har du selv?
> - Givet at du ikke er leder, hvorfor kan du se data i HR Lederdashboardet?
> - Hvad skal vi ændre, hvis flere SD-grupper skal kunne anvende HR Lederdashboardet?
>  
> Se <a href="https://github.com/DataOgDigitalisering/FortroligInformation/blob/main/Exercises/ex_brugerstyring.sql" target="_blank">**løsningsforslag**</a>.

</details>
{::options parse_block_html="false" /}

