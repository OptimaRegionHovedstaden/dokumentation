# Exitsurvey

Exit-undersøgelsesfanen i HR Strategisk Dashboard tager afsæt i Exitsurveyen, som automatisk udsendes til alle personer, der frivilligt fratræder. 

## Resume af tabeller

### v_DimExitSurveyRespondent

| **View** | **Baseret på** | 
| - | - |
| [chru_cube].[v_DimExitSurveyRespondent] | [DM_FL_HR].[SD_EXITSURVEY_RESPONSES] |



### v_FactExitSurvey

| **View** | **Baseret på** | 
| - | - |
| [chru_cube].[v_FactExitSurvey] | [DM_FL_HR].[SD_EXITSURVEY_RESPONSES] [DM_FL_HR].[SD_EXITSURVEY_STRUCTURE] [DM_FL_HR].[SD_EXITSURVEY_LABELS] |



### v_TallyAmbassadør

| **View** | **Baseret på** | 
| - | - |
| [chru_cube].[v_TallyAmbassadør] | - |
v_TallyAmbassadør er en hjælpetabel, som benyttes til at danne et ambassadørfilter i HR Strategisk Dashboard, som kan trækkes ned over visningerne. Tabellen indeholder to kolonner: ID og Ambassadørtype. I tabellen svarer ambassadørtypen "Ikke ambassadør" til ID=0, mens ambassadørtypen "Ambassadør" svarer til ID=1. Den enkelte respondent får tilddelt et ambassadørFilter-ID (0 eller 1) i viewet v_FactExitSurvey. 



### (v_DimOrgDrill)

| **View** | **Baseret på** | 
| - | - |
| [chru_cube].[DimOrgDrill] | [chru_cube].[v_DimOrganisation] |



## HR Strategisk dahboard
Exit-undersøgelsen indgår som en selvstændig fane/side i HR Strategisk Dashboard.


**Beregninger**


Kommer snart og tester

Tester lige lidt...
