# Mortality in the Mediterranean
Project analyzing mortality in Mediterranean Migration

*Sarah Klem, MPH, and Kathryne Tenney, MPH, in affliation with the FXB Center for Health and Human Rights at the Harvard T.H. Chan School of Public Health*

## Introduction

### Research Question
European governments have gone to extraordinary efforts to harden European borders and prevent Mediterranean crossing. By combining publicly available data sets, we are seeking to explore the trends in arrivals and mortality in the Mediterranean. We hypothesize that deterrence efforts have decreased arrivals but, by pushing migrants to more dangerous routes, have increased the mortality rate of Mediterranean crossings. 

### Why is this important?
Migration in the Mediterranean is continuing, with hundreds arriving into Europe every day. These migration patterns have been around for millenia and will continue to be migration pathways in the future. European governments have a legal obligation (under maritime law) to rescue all who are in danger in their waters and transport them to a safe port. The challenges surrounding search and rescue in the Mediterran will continue to increase, especially as climate change forces new volumes of migration globally. 


## Data Sources

### IOM's Missing Migrants Project
**[About](https://missingmigrants.iom.int/about)**: "IOM's Missing Migrants Project tracks deaths of migrants, including refugees and asylum-seekers, who have gone missing along mixed migration routes worldwide. The research behind this project began with the October 2013 tragedies, when at least 368 individuals died in two shipwrecks near the Italian island of Lampedusa. Since then, Missing Migrants Project has developed into an important hub and advocacy source of information that media, researchers, and the general public access for the latest information."

**[Missing Migrants Project Methodology](https://missingmigrants.iom.int/methodology)**:

*Who are included?*: "Missing Migrants Project counts [migrants](https://www.iom.int/key-migration-terms) who have died at the external borders of states, or in the process of migration towards an international destination, regardless of their legal status. The Project records only those migrants who die during their journey to a country different from their country of residence. Missing Migrants Project data include the deaths of migrants who die in transportation accidents, shipwrecks, violent attacks, or due to medical complications during their journeys. It also includes the number of corpses found at border crossings that are categorized as the bodies of migrants, on the basis of belongings and/or the characteristics of the death."

*Who are not included?*: "The count excludes deaths that occur in immigration detention facilities or after deportation to a migrant’s homeland, as well as deaths more loosely connected with migrants´ irregular status, such as those resulting from labour exploitation. Migrants who die or go missing after they are established in a new home are also not included in the data, so deaths in refugee camps or housing are excluded.  The deaths of internally displaced persons who die within their country of origin are also excluded."

*See [methodology](https://missingmigrants.iom.int/methodology) for additional details on sources of information, difficulties encountered, and precise variable definitions*

**IOM Reports**
[Mixed Migration Flows in the Mediterranean: Compilation of Available Data and Information, December 2019](https://dtm.iom.int/reports/europe-%E2%80%94-mixed-migration-flows-europe-monthly-overview-december-2019)
[Calculating "Death Rates" in the Context of Migration Journeys: Focus on the Central Mediterranean](https://gmdac.iom.int/calculating-death-rates-context-migration-journeys-focus-central-mediterranean)


### [UNHCR's Asylum Arrivals Data](https://data2.unhcr.org/en/documents/details/58460)

This is the UNHCR (the UN refugee agency) official published data on the number of arrivals to Mediterranean countries, including Italy, Greece, Spain, Malta, and Cyprus. It offers total by month for each country, as well as (1) by country of origin for arrivals to Italy, Greece and Spain, (2) disaggregation of land and sea arrivals for Spain and Greece, and (3) daily arrivals for Greece and Italy. 

There are significant discrepancies in the numbers provided by the different UNHCR disaggregation methods. The monthly totals generally (but not always) have the largest totals and are available for all of the countries of interest, therefore they will be used.

**Limitations**: The data quality is suspect, as evidenced by the fact that the monthly totals vary across the disaggregation methods listed above. The data is also limited by the fact that this is only official asylum seeker registration. For smuggling routes, which are included in the mortality data, their goal is typically to bypass the Mediterranean countries and register for asylum in Western/Northern European countries. Therefore, asylum registries likely underestimate the monthly arrivals. 

    import requests
    import json  
    import pandas as pd
    from pandas.io.json import json_normalize  

    italy = json.loads(requests.get('https://data2.unhcr.org/population/get/timeseries?widget_id=191313&geo_id=656&sv_id=11&population_group=4908&frequency=day&fromDate=1900-01-01').text) 
    df = json_normalize(italy['data']['timeseries']) 
    df['date'] = pd.to_datetime(df['data_date'])
    df['year'] = df['date'].dt.year
    df['month'] = df['date'].dt.month
    df['day'] = df['date'].dt.day
    df.groupby(['year']).agg(crossed=('individuals', 'sum'))
    
    greece = json.loads(requests.get('https://data2.unhcr.org/population/get/timeseries?widget_id=192041&geo_id=640&sv_id=11&population_group=4908&frequency=day&fromDate=1900-01-01').text) 
    spain = json.loads(requests.get('https://data2.unhcr.org/population/get/timeseries?widget_id=190462&geo_id=729&sv_id=11&population_group=4797,4798&frequency=month&fromDate=1900-01-01').text) 
    malta = json.loads(requests.get('https://data2.unhcr.org/population/get/timeseries?widget_id=186069&geo_id=690&sv_id=11&population_group=4797,4798&frequency=month&fromDate=1900-01-01').text) 
    cyprus = https://data2.unhcr.org/population/get/timeseries?widget_id=186069&geo_id=616&sv_id=11&population_group=4797,4798&frequency=month&fromDate=2015-01-01

### Additional Sources
* [Turkish Coast Guard](https://en.sg.gov.tr/irregular-migration-statistics)
* IOM Libya Maritime updates: https://www.iom.int/sites/default/files/libya_in_20181216-31.pdf, posted weekly on [IOM Libya's Twitter](https://twitter.com/IOM_Libya), https://reliefweb.int/report/libya/maritime-update-libyan-coast-16-31-december-2018-enar, https://reliefweb.int/report/libya/iom-libya-maritime-update-01-15-april-2020

**TO DO**
* Fill out [IOM's spreadsheet](https://missingmigrants.iom.int/sites/default/files/Annex_Med%20arrivals%20interceptions%20deaths_0.xlsx) continued into 2020 
* Consider implementing a rolling annual average or other means to normalize mortality rates
* Decide on our threshold for problematic mortality rates:
* * From IOM: "There are different trains of thought and practice around what mortality rate constitutes a humanitarian emergency. The standard threshold has been a crude mortality rate of 1 death per 10,000 people a day, or 2 deaths per 10,000 per day for under-five years. The Sphere Project (available at www. spherestandards.org and the UNHCR (see more at www.refworld.org/docid/46a9e29a2.html) use a threshold of two times the “normal mortality rate” for the same population"
* Look into which ships came via the Central route and were diverted to Spain or another country because the Italian or Maltese government refused to allow them to disembark. For example, this [August 2019 incident](https://elpais.com/elpais/2019/08/20/inenglish/1566295598_196996.html)
* [Read Checchi, 2018](https://www.who.int/health-cluster/resources/publications/LSHTM-Mortality-Estimation-Options-oct2018.pdf) to shape conversation on the ethics of presenting our findings
