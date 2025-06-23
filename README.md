## Initial Report and Exploratory Data Analysis (EDA) 
### Link to the Jupyter notebook
[My Jupyter notebook](https://github.com/jeffhonghou/Global_Terrorism_Initial_Analysis/blob/main/risklevel.ipynb)
### Overview
#### The research question you intend to answer (in one sentence, if possible):
Can we identify high-risk, medium-risk, and low-risk geographic clusters of terrorism attacks to provide pre-travel guidance using the Global Terrorism Database on Kaggle?

#### Data Source and Attribution
The analysis will use the Global Terrorism Database (GTD), available on Kaggle: https://www.kaggle.com/datasets/START-UMD/gtd. This dataset contains detailed records of over 180,000 terrorist incidents worldwide from 1970 to 2017, including date, location, weapons used, target type, and casualties.
> **Citation**:  
> National Consortium for the Study of Terrorism and Responses to Terrorism (START), University of Maryland. (2018).  *The Global Terrorism Database (GTD) [Data file].*  Retrieved from [https://www.start.umd.edu/gtd](https://www.start.umd.edu/gtd)

> **Copyright Notice**:  
> Copyright University of Maryland 2018.

> **Data Modifications**:  
> This analysis includes preprocessing of the original GTD dataset, including:
> - Filtering for relevant columns (e.g., country, region, latitude, longitude, casualties),
> - Handling missing values,
> - Creating a "casualties" column to represent attack severity.
>  
> These transformations were made solely for clustering and visualization purposes. They do not reflect any analytical decisions or interpretations made by the National Consortium for the Study of Terrorism and Responses to Terrorism (START), headquartered at the University of Maryland.

#### The techniques you expect to use in your analysis:
Data Preprocessing: Handle missing values, and filter relevant periods and columns (e.g., country, region, latitude, longitude, number of casualties, and attack type).
Exploratory Data Analysis: Visualize attack frequency by region, time trends, and severity.
Clustering Models: Since my main task is to cluster geographic regions into risk zones, I will use unsupervised learning models like K-Means or DBSCAN on spatial and severity features (e.g., latitude, longitude, casualties) to group areas into high, medium, and low-risk zones.
Visualization: Use Plotly to provide visual risk maps.

#### The expected results:
•	Creation of distinct geographic clusters that classify regions into high, medium, and low-risk zones based on historical terrorist activity.
•	Plots showing attack density and severity across continents and countries.

#### Why this question is important
The question is important because it can help travelers and organizations assess security risks for travel destinations, enhance public awareness and preparedness for travel in sensitive regions, and transform raw terrorism data into actionable intelligence for both individuals and institutions. 

#### Column name and description of the dataset based on the official GTD codebook provided by START (University of Maryland). 
| Column Name                  | Description                                           |
| ---------------------------- | ----------------------------------------------------- |
| `eventid`                    | Unique ID for the event (formatted YYYYMMDDXX)        |
| `iyear`                      | Year of the incident                                  |
| `imonth`                     | Month of the incident (0 = unknown)                   |
| `iday`                       | Day of the incident (0 = unknown)                     |
| `approxdate`                 | Approximate date when the actual day is unknown       |
| `extended`                   | Whether the incident extended beyond 24 hours         |
| `resolution`                 | How the extended incident was resolved                |
| `country`                    | Numeric code for the country                          |
| `country_txt`                | Country name                                          |
| `region`                     | Numeric code for the region                           |
| `region_txt`                 | Region name                                           |
| `provstate`                  | Province, state, or administrative division           |
| `city`                       | City where the attack occurred                        |
| `latitude`                   | Latitude of the incident location                     |
| `longitude`                  | Longitude of the incident location                    |
| `specificity`                | Geographic specificity of the location                |
| `vicinity`                   | Whether the attack happened in or near the city       |
| `location`                   | Additional descriptive location info                  |
| `summary`                    | Narrative summary of the event                        |
| `crit1`                      | Criterion 1 of GTD terrorist definition met (1 = yes) |
| `crit2`                      | Criterion 2 met                                       |
| `crit3`                      | Criterion 3 met                                       |
| `doubtterr`                  | Doubt that the incident was an act of terrorism       |
| `alternative`                | Alternative explanation code                          |
| `alternative_txt`            | Text label of alternative eguncertainxplanation                 |
| `multiple`                   | Was part of multiple coordinated attacks              |
| `success`                    | Whether the attack achieved its goal                  |
| `suicide`                    | Whether it was a suicide attack                       |
| `attacktype1`                | Code for primary attack type                          |
| `attacktype1_txt`            | Description of primary attack type                    |
| `attacktype2`                | Secondary attack type code                            |
| `attacktype2_txt`            | Description of secondary attack type                  |
| `attacktype3`                | Tertiary attack type code                             |
| `attacktype3_txt`            | Description of tertiary attack type                   |
| `targtype1`                  | Code for type of first target                         |
| `targtype1_txt`              | Text label for type of first target                   |
| `targsubtype1`               | Subtype code of first target                          |
| `targsubtype1_txt`           | Subtype text of first target                          |
| `corp1`                      | Organization/company name of first target             |
| `target1`                    | Specific entity or person targeted                    |
| `natlty1`                    | Nationality code of first target                      |
| `natlty1_txt`                | Nationality of first target                           |
| `targtype2`                  | Code for type of second target                        |
| `targtype2_txt`              | Text label for type of second target                  |
| `targsubtype2`               | Subtype code of second target                         |
| `targsubtype2_txt`           | Subtype text of second target                         |
| `corp2`                      | Organization/company of second target                 |
| `target2`                    | Specific entity or person targeted (2nd target)       |
| `natlty2`                    | Nationality code of second target                     |
| `natlty2_txt`                | Nationality of second target                          |
| `targtype3`                  | Code for type of third target                         |
| `targtype3_txt`              | Text label for type of third target                   |
| `targsubtype3`               | Subtype code of third target                          |
| `targsubtype3_txt`           | Subtype text of third target                          |
| `corp3`                      | Organization/company of third target                  |
| `target3`                    | Specific entity or person targeted (3rd target)       |
| `natlty3`                    | Nationality code of third target                      |
| `natlty3_txt`                | Nationality of third target                           |
| `gname`                      | Name of the perpetrator group                         |
| `gsubname`                   | Subgroup name (if any)                                |
| `gname2`                     | Second perpetrator group                              |
| `gsubname2`                  | Subgroup of second group                              |
| `gname3`                     | Third perpetrator group                               |
| `gsubname3`                  | Subgroup of third group                               |
| `motive`                     | Suspected or known motive (free-text)                 |
| `guncertain1`                | Uncertainty about responsibility of first group       |
| `guncertain2`                | Uncertainty for second group                          |
| `guncertain3`                | Uncertainty for third group                           |
| `individual`                 | Was the attack carried out by individuals?            |
| `nperps`                     | Number of perpetrators                                |
| `nperpcap`                   | Number of perpetrators captured                       |
| `claimed`                    | First group claimed responsibility?                   |
| `claimmode`                  | Mode of claim (e.g., letter, video)                   |
| `claimmode_txt`              | Description of claim mode                             |
| `claim2`                     | Second group claim                                    |
| `claimmode2`                 | Claim mode of second group                            |
| `claimmode2_txt`             | Text for second claim mode                            |
| `claim3`                     | Third group claim                                     |
| `claimmode3`                 | Claim mode of third group                             |
| `claimmode3_txt`             | Text for third claim mode                             |
| `compclaim`                  | Were there competing claims?                          |
| `weaptype1`                  | Primary weapon type code                              |
| `weaptype1_txt`              | Primary weapon description                            |
| `weapsubtype1`               | Weapon subtype code                                   |
| `weapsubtype1_txt`           | Subtype description                                   |
| `weaptype2`                  | Secondary weapon type                                 |
| `weaptype2_txt`              | Text label for secondary weapon                       |
| `weapsubtype2`               | Secondary weapon subtype                              |
| `weapsubtype2_txt`           | Subtype text                                          |
| `weaptype3`                  | Third weapon type                                     |
| `weaptype3_txt`              | Text label for third weapon                           |
| `weapsubtype3`               | Third weapon subtype                                  |
| `weapsubtype3_txt`           | Text label                                            |
| `weaptype4`                  | Fourth weapon type                                    |
| `weaptype4_txt`              | Text label                                            |
| `weapsubtype4`               | Fourth weapon subtype                                 |
| `weapsubtype4_txt`           | Subtype description                                   |
| `weapdetail`                 | Free-text detail on weapons used                      |
| `nkill`                      | Number of people killed                               |
| `nkillus`                    | Number of U.S. nationals killed                       |
| `nkillter`                   | Number of perpetrators killed                         |
| `nwound`                     | Number of people wounded                              |
| `nwoundus`                   | Number of U.S. nationals wounded                      |
| `nwoundte`                   | Number of perpetrators wounded                        |
| `property`                   | Was property damaged?                                 |
| `propextent`                 | Extent of property damage (coded)                     |
| `propextent_txt`             | Text for property damage extent                       |
| `propvalue`                  | Estimated property damage value                       |
| `propcomment`                | Notes on property damage                              |
| `ishostkid`                  | Were hostages or kidnapped victims involved?          |
| `nhostkid`                   | Number of hostages/kidnappings                        |
| `nhostkidus`                 | Number of U.S. hostages                               |
| `nhours`                     | Duration of hostage situation in hours                |
| `ndays`                      | Duration in days                                      |
| `divert`                     | Flight diversion location (if hijacking)              |
| `kidhijcountry`              | Country involved in hijacking                         |
| `ransom`                     | Was ransom demanded?                                  |
| `ransomamt`                  | Total ransom amount demanded                          |
| `ransomamtus`                | Amount demanded in USD                                |
| `ransompaid`                 | Amount paid in local currency                         |
| `ransompaidus`               | Amount paid in USD                                    |
| `ransomnote`                 | Was a ransom note involved?                           |
| `hostkidoutcome`             | Code for hostage situation outcome                    |
| `hostkidoutcome_txt`         | Outcome description                                   |
| `nreleased`                  | Number of hostages released                           |
| `addnotes`                   | Additional notes by researchers                       |
| `scite1`, `scite2`, `scite3` | Sources used for coding                               |
| `dbsource`                   | Source database(s) used                               |
| `INT_LOG`                    | Linkage to international logistics                    |
| `INT_IDEO`                   | Linkage to international ideology                     |
| `INT_MISC`                   | Other international link                              |
| `INT_ANY`                    | Any international involvement                         |
| `related`                    | Event IDs of related attacks                          |

## Exploratory data analysis (EDA)
### Feature selection
Now I am going to remove columns step by step that are not relevant to assessing risk levels.
#### Exclude all columns like summaries, notes, and motives
The following columns will be excluded in this step: summary, motive, addnotes, scite1, scite2, and scite3
#### Exclude all columns fields which describe detailes of the attack but not directly relevant to geographic risk clustering.
The following columns will be excluded in this step: targtype1,targtype1_txt,targsubtype1,targsubtype1_txt,corp1,target1,natlty1,natlty1_txt,targtype2,
targtype2_txt,targsubtype2,targsubtype2_txt,corp2,target2,natlty2,natlty2_txt,targtype3,targtype3_txt,targsubtype3,targsubtype3_txt,corp3,target3,natlty3,
natlty3_txt,gname,gsubname,gname2,gsubname2,gname3,gsubname3,guncertain1,guncertain2,guncertain3,individual,nperps,nperpcap,claimed,claimmode,
claimmode_txt,claim2,claimmode2,claimmode2_txt,claim3,claimmode3,claimmode3_txt,compclaim,weaptype1,weaptype1_txt,weapsubtype1,weapsubtype1_txt,
weaptype2,weaptype2_txt,weapsubtype2,weapsubtype2_txt,weaptype3,weaptype3_txt,weapsubtype3,weapsubtype3_txt,weaptype4,weaptype4_txt,weapsubtype4,
weapsubtype4_txt,weapdetail,property,propextent,propextent_txt,ishostkid,nhostkid,nhostkidus,ransom,ransomamt,ransomamtus,ransompaid,ransompaidus,
ransomnote,hostkidoutcome,hostkidoutcome_txt,INT_LOG,INT_IDEO,INT_MISC,INT_ANY
#### Exclude other fields manually
I am excluding the columns eventid,alternative,alternative_txt,multiple,nhours,ndays,divert,kidhijcountry,nreleased,dbsource, and related.
#### From the remaining features, I will select 'iyear', 'country_txt', 'region_txt', 'latitude', 'longitude', 'nkill', 'nwound', and 'attacktype1_txt' for further analysis.
To quantify overall severity, I will aggregate the number of fatalities and injuries, assigning a weight of 100 to each fatality (nkill) to reflect its substantially greater impact compared to an injury (nwound).

### Results
To establish a baseline, I analyzed the distribution of the casualties column (combined weighted nkill and nwound) using normalized value counts. This results in a baseline accuracy of 20.87% if we always predict an outcome equivalent to one fatality (or 100 injuries) per attack.

