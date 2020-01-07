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

### [UNHCR's Asylum Arrivals Data](https://data2.unhcr.org/en/documents/details/58460)

This is the UNHCR (the UN refugee agency) official published data on the number of arrivals to Mediterranean countries, including Italy, Greece, Spain, Malta, and Cyprus. It offers total by month for each country, as well as (1) by country of origin for arrivals to Italy, Greece and Spain, (2) disaggregation of land and sea arrivals for Spain and Greece, and (3) daily arrivals for Greece and Italy. 

There are significant discrepancies in the numbers provided by the different UNHCR disaggregation methods. The monthly totals generally (but not always) have the largest totals and are available for all of the countries of interest, therefore they will be used.

**Limitations**: The data quality is suspect, as evidenced by the fact that the monthly totals vary across the disaggregation methods listed above. The data is also limited by the fact that this is only official asylum seeker registration. For smuggling routes, which are included in the mortality data, their goal is typically to bypass the Mediterranean countries and register for asylum in Western/Northern European countries. Therefore, asylum registries likely underestimate the monthly arrivals. 

**TO DO, when final 2019 data is posted**
* assemble comparison table of the differing values by UNHCR data source
* Look into which ships came via the Central route and were diverted to Spain or another country because the Italian or Maltese government refused to allow them to disembark. For example, this [August 2019 incident](https://elpais.com/elpais/2019/08/20/inenglish/1566295598_196996.html)
* reach out to Kobo/UNHCR (stats@unhcr.org) to get their API to work
