# Retrosheet 2024
Tool for extracting and organizing the second of the Retrosheet 2024 semi-annual updates.

Retrosheet publishes a semi-annual update to their data downloads. This notebook collects the updated files, compiles and converts them to a series of flat .CSV files, with a minimal amount of duplication, for easy uploading into a relational database. In the process, this tool attempts to correct any known errors and inconsistencies. It is a Jupyter notebook tested in Google Colab. Details regarding the ETL process can be found in the markdown of the notebook; here we are describing the errors and inconsistencies present in the source data. Furthermore, we discuss in detail the supporting evidence and rataionale for the changes made to the source data, including how the new files are organized.


## 1. Extracting the *ZIP* Files
The *bevent* extraction utility provided by Retrosheet fails to completely extract the *2021AS.EVE* event file. There is no obvious malformation of the source file, *ROS* (roster) file, or *TEAM* file that would cause this error. As a result, the events for this game are not recorded in the event files.

## 2. Biodata
- The *UMPIRES1939.txt* file has and entry for Finnis Brenaham (id=brenu901);
- *UMPIRES1931.txt* has an entry for Brenham (no first name; id=brenu902);
- *UMPIRES1940.txt* has an entry for Finnis Brenaham (id=brenu902);
- Biodata does not have an id for brenu901.

We assume the biographical data for Finnis Brenaham (id=brenu901) is correct and should have an id of brenf901. All other entries are adjusted accordingly.


## 3. Parks
The parks data has several changes from the Retrosheet source file:
- The location columns are expanded to city, state, and country.
- Countries are identified by three-letter codes described by the ISO 3166 standard.
- States, whenever possible, are identified by the formal postal abbreviation of the jurisdiction in question. Typically, this is a two, three, or four-character code except for London, England. In this case, 'England' is given as the state and 'GBR' is the country code.
- Dates are standardized to the YYYY-mm-dd format. This standard is applied to all tables.

## 4. Game Log Files
- Name columns are removed as they are redundant to the player/manager/umpire id codes.
- Dates are standardized to the YYYY-mm-dd format.
- Day of the week column is dropped as it is easily determined from the date by virtually every software package.
- Values of -1, used to indicate missing data, are converted to NULL values.
- Columns containing alpha-numeric code are converted to lowercase, except for game ids, team ids, league ids, and park ids.
- Line scores are reformatted to assist with splitting: parentheses are replaced with the tilde (~) symbol.

The game logs also contain instances where values disagree with values in the *bgame* and *gameinfo* files. In the charts below, the columns where incorrect values were discovered, the corrected value, and the rationale for making the changes are described in detail.

|   **GWRBI** |             |                        |                                           |
|--------------|-------------|----------------------|-------------------------------------------|
| Game ID           | GWRBI ID | Remediation          | Notes                                     |
| CAL197704160 | remyj001    | Change to NULL | Not official except for 1980-1988 seasons |
| CHA199004180 | boggw001    | Change to NULL | Not official except for 1980-1988 seasons |
| CHA199306260 | ventr001    | Change to NULL | Not official except for 1980-1988 seasons |
| CHN195307052 | bellg103    | Change to NULL | Not official except for 1980-1988 seasons |
| CHN195407041 | bakeg101    | Change to NULL | Not official except for 1980-1988 seasons |
| CHN195407232 | sched102    | Change to NULL | Not official except for 1980-1988 seasons |
| CHN196406160 | dalrc101    | Change to NULL | Not official except for 1980-1988 seasons |
| CIN195306161 | westw101    | Change to NULL | Not official except for 1980-1988 seasons |
| CIN195306162 | greej102    | Change to NULL | Not official except for 1980-1988 seasons |
| CLE196708062 | hortt101    | Change to NULL | Not official except for 1980-1988 seasons |
| CLE196708130 | clarh101    | Change to NULL | Not official except for 1980-1988 seasons |
| MLN196407192 | torrj101    | Change to NULL | Not official except for 1980-1988 seasons |
| NY1195109031 | ashbr101    | Change to NULL | Not official except for 1980-1988 seasons |
| PHA195308162 | mcdog101    | Change to NULL | Not official except for 1980-1988 seasons |
| PHI195307260 | musis101    | Change to NULL | Not official except for 1980-1988 seasons |
| SEA197704090 | joner002    | Change to NULL | Not official except for 1980-1988 seasons |
| SEA199005070 | evand002    | Change to NULL | Not official except for 1980-1988 seasons |
| SEA199008030 | hrbek001    | Change to NULL | Not official except for 1980-1988 seasons |
| SEA199307310 | jackb001    | Change to NULL | Not official except for 1980-1988 seasons |
| WS2196705120 | alvim101    | Change to NULL | Not official except for 1980-1988 seasons |


| **Home Team Errors** |                       |                   |                  |                                       |
|----------------------|-----------------------|-------------------|------------------|---------------------------------------|
| Game ID              | home_err in Game Logs | home_err in BGAME | Remediation      | Note                                  |
| ATL197905210         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| ATL199310020         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| ATL199909050         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BAL195505280         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BAL195507300         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BAL195509141         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BAL200609230         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BOS193107152         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BOS193705260         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BOS193805130         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BOS200809230         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BOS201207300         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BRO192009220         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BRO192606021         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BRO193505080         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BRO193808050         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BRO194209100         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BRO194307090         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BRO194309110         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BRO194709240         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BRO195409220         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BSN192108250         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BSN193407112         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BSN193605302         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BSN193906030         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| BSN194804240         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CHA193709021         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CHA194907200         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CHA201305270         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CHN193506011         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CHN194707310         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CHN195105202         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CHN195408292         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CHN195705110         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CHN201704120         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CIN191410051         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CIN193809070         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CIN199708020         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CIN200708210         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CLE194205210         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| CLE195609162         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| DET191309271         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| DET192006120         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| DET192108240         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| DET193204140         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| DET194204140         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| DET194809120         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| DET195007270         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| DET195506040         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| DET195609150         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| DET195609210         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| FLO199307230         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| HOU196209060         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| HOU201208100         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| HOU201708290         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| KCA197505060         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| LAN199907030         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| LAN201108130         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| MIA201405240         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| MIL199906250         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| MIL199909020         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| MIN200906160         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| MIN200907030         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| MLN195506220         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| MLN196305040         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| MON197804222         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| MON199005060         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| NY1190510140         | 2                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| NY1194205200         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| NY1195008050         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| NY1195309010         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| NYA192906230         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| NYA194604190         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| NYA194905270         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| NYA197104150         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| NYA201007180         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| NYN197208020         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| NYN201505250         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| OAK197108270         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| PHA192405130         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| PHA192808160         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| PHA193106170         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| PHI191207290         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| PHI191209021         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| PHI194608312         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| PHI200307310         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| PIT194806030         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| PIT194906140         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| PIT195607270         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| PIT195709212         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| PIT198105160         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SDN199407030         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SDN201105030         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SDN201309040         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SFN198204300         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SFN201309240         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SLA192507180         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SLA193305060         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SLA194009220         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SLA194305210         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SLA195307161         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SLN192007160         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SLN193110020         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SLN194307280         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SLN195309160         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SLN195309221         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| SLN195706180         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| TBA200806210         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| TOR201009280         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| WS1191504270         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| WS1192807140         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| WS1194604280         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| WS1195505170         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| WS1195507311         | 0                     | 1                 | Change game logs | Event Files indicate Bgame is correct |
| ANA201807100         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| ATL197107170         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| ATL197409070         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| ATL197609171         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| BAL195506151         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| BOS192109130         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| BOS192306182         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| BOS192706250         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| BOS194709171         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| BOS196406102         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| BRO195406260         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| BSN191505312         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| BSN193407200         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CHA191609160         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CHA193804300         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CHA195209130         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CHA195305050         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CHA198709160         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CHN193504160         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CHN194209202         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CHN194405130         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CHN194508240         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CHN194806020         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CHN195508031         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CIN195105132         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CLE192006210         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CLE192908200         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CLE193105262         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CLE195008050         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CLE195108120         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CLE195306030         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CLE195607012         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CLE195609250         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CLE197308170         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CLE201405060         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| CLE201804130         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| DET192505090         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| DET194205290         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| DET194507270         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| DET198805150         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| LAN197008091         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| MIN197004250         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| MLN195406040         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| MLN195507102         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| NY1194207042         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| NY1194507312         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| NY1194608310         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| NY1195205161         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| NY1195705290         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| NYA192909210         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| NYA193005290         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| NYA194709231         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| OAK201809230         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHA191204110         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHA192606242         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHA192707270         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHA192805170         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHA193708012         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHA194208152         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHA194404220         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHA194609251         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHA195308040         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHI191205250         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHI193109051         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHI195608141         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PHI197006140         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PIT193005260         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PIT195406272         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| PIT195604200         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| SDN201704200         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| SFN200908260         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| SLA191206050         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| SLA191505170         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| SLA192209230         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| SLA193108130         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| SLN193909042         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| SLN194208231         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| SLN194307220         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| SLN195306272         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| SLN195605272         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| SLN198207230         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| TBA200408060         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| WS1191909210         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| WS1194007071         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| WS1194305260         | 0                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| WS1194706291         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| WS1195008242         | 1                     | 2                 | Change game logs | Event Files indicate Bgame is correct |
| BAL195507262         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| BAL195605080         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| BLF191410090         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| BOS195505060         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| BOS195609050         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| BRO193207100         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| BRO193707252         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| BRO194307020         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| BRO194508080         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| BSN192707201         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| BSN195104192         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CHA191206130         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CHA191607292         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CHA192006040         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CHA193007311         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CHA197804090         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CHF191505301         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CHN192208180         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CHN192510030         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CHN195308060         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CHN195407020         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CHN195606010         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CIN191709092         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CIN195108030         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CLE193005261         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| CLE195608192         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| DET191409262         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| IND191407030         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| NEW191504270         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| NY1195207310         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| NY1195209081         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| NY1195408222         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| NY1195505030         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| PHA191805200         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| PHA192109280         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| PHA192407191         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| PHA193106080         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| PHI191905260         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| PHI192307212         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| PHI192406060         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| PHI193508181         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| PHI194409042         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| PHI194508250         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| PHI195007042         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| SLA194308160         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| SLA194708160         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| SLA195006150         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| SLF191509122         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| SLN194005121         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| WAS200807310         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| WS1191608171         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| WS1192807170         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| WS1193507300         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| WS1194105180         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| WS1194105220         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| WS1194409090         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| WS1195005271         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| WS1195506150         | 2                     | 3                 | Change game logs | Event Files indicate Bgame is correct |
| BOS192306220         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| BRF191507091         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| CHN195005020         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| MIL201205180         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| NYN199507060         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| PHA191309050         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| PHA192709061         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| PHI191308270         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| PHI193606170         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| PHI193809232         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| PHI195405120         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| PIT201405030         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| SLA193705070         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| SLN195308040         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| WS1191408190         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| WS1193906210         | 3                     | 4                 | Change game logs | Event Files indicate Bgame is correct |
| CHN194007130         | 4                     | 5                 | Change game logs | Event Files indicate Bgame is correct |
| DET191806080         | 4                     | 5                 | Change game logs | Event Files indicate Bgame is correct |
| PHI193209101         | 4                     | 5                 | Change game logs | Event Files indicate Bgame is correct |
| PIT195207120         | 4                     | 5                 | Change game logs | Event Files indicate Bgame is correct |
| SLN193404190         | 3                     | 5                 | Change game logs | Event Files indicate Bgame is correct |
| WS1194408260         | 4                     | 5                 | Change game logs | Event Files indicate Bgame is correct |
| WS1195105140         | 4                     | 5                 | Change game logs | Event Files indicate Bgame is correct |
| CHA191206020         | 5                     | 6                 | Change game logs | Event Files indicate Bgame is correct |
| CHN192205120         | 5                     | 6                 | Change game logs | Event Files indicate Bgame is correct |
| IND191406070         | 5                     | 6                 | Change game logs | Event Files indicate Bgame is correct |
| PHI193807080         | 5                     | 6                 | Change game logs | Event Files indicate Bgame is correct |
| WS1192005200         | 8                     | 9                 | Change game logs | Event Files indicate Bgame is correct |

| **Visitor ERR** |                       |                   |                 |                                                       |
|-----------------|-----------------------|-------------------|-----------------|-------------------------------------------------------|
| **Game ID**     | **vis_err game logs** | **vis_err BGAME** | **Remediation** | **Note**                                              |
| CHA194005190    | 1                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CHN195607200    | 0                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| ANA199904070    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| ANA200805160    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| ATL201307110    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BAL195606130    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BAL195804170    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BAL198304190    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BAL200804170    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BAL201607240    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BLF191407270    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| BLF191410072    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BOS191404140    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| BOS192005240    | 4                     | 5                 | change gamelogs | Events files indicate BGAME is correct |
| BOS192207180    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BOS192807092    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| BOS192908020    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| BOS193208220    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BOS193408122    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| BOS193709041    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| BOS194309040    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BOS194408181    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BOS195008230    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| BOS195105210    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BOS195205040    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| BOS197507170    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BOS198607060    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BOS200709270    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BRF191506072    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| BRO191304210    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| BRO191808090    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BRO192604300    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BRO192605010    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| BRO192608300    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BRO192805130    | 6                     | 7                 | change gamelogs | Events files indicate BGAME is correct |
| BRO193007200    | 4                     | 5                 | change gamelogs | Events files indicate BGAME is correct |
| BRO193008050    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| BRO193306042    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BRO193804280    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BRO194006140    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BRO194009111    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BRO194206211    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BRO194209240    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BRO194507041    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| BRO194906070    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BRO195206180    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BRO195408040    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| BSN192208030    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BSN193407240    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BSN194309161    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BSN194508161    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BSN194609132    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| BSN194905040    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BSN195005230    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| BSN195208080    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHA191404180    | 5                     | 6                 | change gamelogs | Events files indicate BGAME is correct |
| CHA191407250    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHA192109090    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| CHA192408092    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHA192609110    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHA192708240    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CHA192905280    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHA193105160    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CHA193308202    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| CHA193408070    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CHA193808131    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHA194006190    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CHA194106050    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CHA194107120    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHA194107202    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CHA194607270    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHA195007280    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHA195007290    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CHA195008010    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHA195108160    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CHA195207252    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CHA200510120    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CHA201507040    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CHN190710080    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CHN192005130    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHN192509032    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CHN193809280    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| CHN193904240    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| CHN193906300    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHN193909160    | 5                     | 6                 | change gamelogs | Events files indicate BGAME is correct |
| CHN194109160    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| CHN194407130    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CHN194608202    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHN194608240    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHN194609210    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHN195008290    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHN195109022    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CHN195606120    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CHN195608220    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHN198807160    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHN198808240    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CHN199305120    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CIN191906080    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CIN192506100    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CIN192906162    | 5                     | 6                 | change gamelogs | Events files indicate BGAME is correct |
| CIN193509082    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CIN193807010    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CIN195005050    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CIN195305312    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CIN195508160    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CIN197308240    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CIN199308010    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CIN200309100    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CIN200709040    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CIN201707160    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CLE191508190    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CLE191807020    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CLE192006180    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| CLE192609120    | 4                     | 5                 | change gamelogs | Events files indicate BGAME is correct |
| CLE192809160    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CLE193405290    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CLE193806160    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CLE193904240    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CLE194207242    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| CLE194708222    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| CLE195410020    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| CLE195609300    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| COL201104010    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| COL201107160    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| DET191708180    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| DET192809210    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| DET193708130    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| DET193805260    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| DET194108122    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| DET194108211    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| DET194305220    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| DET198204160    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| DET201104100    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| DET201606240    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| FLO199405100    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| FLO199905210    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| HOU200806120    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| HOU201304070    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| KC1195609120    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| KC1196207152    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| LAA196106300    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| LAN199306040    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| LAN200709250    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| LAN200807120    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| MIL197206180    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| MIL201404130    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| MIL201806130    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| MIN196506040    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| MIN199009090    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| MIN199708040    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| MIN199908240    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| MIN200307310    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| MIN200708010    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| MLN195309080    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| MLN195509111    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| MLN196308030    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| MON199308050    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| NEW191506131    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| NLS194407110    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| NY1191806040    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| NY1192007052    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| NY1192207260    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| NY1192609111    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| NY1193007192    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| NY1193509010    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| NY1194208030    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| NY1195407290    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| NYA191506110    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| NYA191706231    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| NYA191807120    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| NYA192607200    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| NYA192805130    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| NYA193005270    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| NYA193209052    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| NYA193505190    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| NYA193608301    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| NYA193807121    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| NYA194405211    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| NYA194606120    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| NYA194705150    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| NYA194807220    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| NYA195104240    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| NYA195105240    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| NYA195107240    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| NYA195204210    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| NYA195208250    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| NYA195606070    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| NYA198804290    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| NYN198608290    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| NYN200304020    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| OAK197007290    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| OAK197609191    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHA191407021    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PHA191605040    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PHA191607111    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHA191909062    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| PHA192008201    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| PHA192106030    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHA192509250    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PHA192605040    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| PHA193208292    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PHA193809251    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PHA194005080    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PHI191206130    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHI191208311    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHI191505150    | 4                     | 5                 | change gamelogs | Events files indicate BGAME is correct |
| PHI191608142    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| PHI191706262    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| PHI191909241    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHI192004240    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| PHI192006150    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| PHI192508200    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHI192804300    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| PHI192905301    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHI193109052    | 5                     | 6                 | change gamelogs | Events files indicate BGAME is correct |
| PHI193605280    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHI194006302    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHI194206290    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHI194407151    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHI194409101    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PHI194506221    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PHI194508121    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| PHI194508210    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| PHI194907200    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PHI195005240    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PHI195308280    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PHI195507010    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| PHI201110070    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PIT193406021    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PIT193909272    | 4                     | 5                 | change gamelogs | Events files indicate BGAME is correct |
| PIT194309010    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| PIT195505210    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PIT195506121    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PIT195606171    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PIT195607310    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| PIT198604240    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SDN198907290    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| SDN200304040    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SDN200505310    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SDN201404130    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SEA200505180    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| SFN197009080    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SFN197206112    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SFN199304160    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SFN201404110    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SLA191405302    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| SLA191409262    | 4                     | 5                 | change gamelogs | Events files indicate BGAME is correct |
| SLA191507152    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| SLA191606211    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| SLA191608030    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| SLA191705082    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SLA192207010    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| SLA193007140    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| SLA193605120    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| SLA193806140    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| SLA193809190    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| SLA194704271    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SLN192905010    | 3                     | 4                 | change gamelogs | Events files indicate BGAME is correct |
| SLN192906161    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| SLN193110090    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SLN193504260    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SLN194007062    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SLN194008270    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SLN194109190    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SLN195308090    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| SLN195309140    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| SLN195309210    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| SLN195408310    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SLN195605271    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SLN196807250    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| SLN197008150    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| SLN200709152    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| SLN201705120    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| TBA201304190    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| TEX197609120    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| WS1191207100    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| WS1191408242    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| WS1191509200    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| WS1191704200    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| WS1192008290    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| WS1192506130    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| WS1192510100    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| WS1193005222    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| WS1193304250    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| WS1193406030    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| WS1194008080    | 0                     | 1                 | change gamelogs | Events files indicate BGAME is correct |
| WS1195004290    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |
| WS1195207140    | 4                     | 5                 | change gamelogs | Events files indicate BGAME is correct |
| WS1195608270    | 1                     | 2                 | change gamelogs | Events files indicate BGAME is correct |
| WS2196707301    | 2                     | 3                 | change gamelogs | Events files indicate BGAME is correct |


| **Home LOB*** |                        |                    |                  |                                       |
|---------------|------------------------|--------------------|------------------|---------------------------------------|
| **Game ID**   | **home_lob game logs** | **home_lob BGAME** | **Remediation**  | **Note**                              |
| ATL199210030  | 3                      | 4                  | change game_logs | Event Files indicate Bgame is correct |
| ATL201609180  | 8                      | 9                  | change game_logs | Event Files indicate Bgame is correct |
| BOS196904160  | 5                      | 6                  | change game_logs | Event Files indicate Bgame is correct |
| CHA197306160  | 6                      | 7                  | change game_logs | Event Files indicate Bgame is correct |
| CHA201208260  | 2                      | 4                  | change game_logs | Event Files indicate Bgame is correct |
| CHN194507280  | 8                      | 10                 | change game_logs | Event Files indicate Bgame is correct |
| DET195606260  | 3                      | 5                  | change game_logs | Event Files indicate Bgame is correct |
| DET196106010  | 9                      | 10                 | change game_logs | Event Files indicate Bgame is correct |
| FLO200906300  | 2                      | 4                  | change game_logs | Event Files indicate Bgame is correct |
| KCA197108070  | 1                      | 3                  | change game_logs | Event Files indicate Bgame is correct |
| NYN197907290  | 6                      | 7                  | change game_logs | Event Files indicate Bgame is correct |
| PHI198906050  | 10                     | 11                 | change game_logs | Event Files indicate Bgame is correct |
| TEX197208120  | 2                      | 4                  | change game_logs | Event Files indicate Bgame is correct |


| **Visitor Hits** |                     |                 |                 |                                       |
|------------------|---------------------|-----------------|-----------------|---------------------------------------|
| **Game ID**      | **vis_h game logs** | **vis_h BGAME** | **Remediation** | **Note**                              |
| NY1190510140     | 5                   | 6               | change gamelogs | Event files indicate BGAME is correct |

| **Visitor LOB** |                       |                   |                 |                                       |
|-----------------|-----------------------|-------------------|-----------------|---------------------------------------|
| **Game ID**     | **vis_lob game logs** | **vis_lob BGAME** | **Remediation** | **Note**                              |
| CHN198708272    | 5                     | 6                 | change gamelogs | Event Files indicate Bgame is correct |
| CIN196005250    | 2                     | 3                 | change gamelogs | Event Files indicate Bgame is correct |
| CLE200106210    | 3                     | 4                 | change gamelogs | Event Files indicate Bgame is correct |
| KCA197204260    | 4                     | 5                 | change gamelogs | Event Files indicate Bgame is correct |
| NYA195407070    | 5                     | 6                 | change gamelogs | Event Files indicate Bgame is correct |
| PIT197406150    | 11                    | 12                | change gamelogs | Event Files indicate Bgame is correct |
| PIT202106100    | 10                    | 12                | change gamelogs | Event Files indicate Bgame is correct |
| TEX197609080    | 6                     | 8                 | change gamelogs | Event Files indicate Bgame is correct |
| WS1191405080    | 9                     | 8                 | change gamelogs | Event Files indicate Bgame is correct |
| WS2196804270    | 1                     | 3                 | change gamelogs | Event Files indicate Bgame is correct |
        

The definition of a night is "any game that is played with the use of artificial lights". This definition, unfortunately leads to some ambiguity. In general, Retrosheet appears use 17:00:00 (5:00PM) as the delineation between the two. This is not universally applied, however, and we address this issue by only looking at games where the day/night indicator differs between the game logs and BGAME files. In these instances, if we can determine that a game ended after 20:15:00 (8:15PM), we change the value to indicate a night game. In all other instances, the values are not changed. This does not ensure the accuracy of the data, but is, arguably, an improvement.

| **DAY/NIGHT Games** |                         |                     |                 |                                                                 |
|---------------------|-------------------------|---------------------|-----------------|-----------------------------------------------------------------|
| **Game ID**         | **day_night game logs** | **day_night BGAME** | **Remediation** | **Note**                                                        |
| CIN194208092        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CIN194406281        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PIT194505302        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1194505301        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1194506051        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1194506151        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CLE194506301        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1194507161        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1194507181        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1194507201        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1194508011        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CIN194508031        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1194508031        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI194508081        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI194508101        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1194508311        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1194509051        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1194509061        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1194509101        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CIN195006011        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA195105272        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CLE195207221        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA195309230        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CHA195508231        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| SLN195706191        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1195806031        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS1195806101        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CLE195906072        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA195906212        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196006091        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196006211        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| SLN196007011        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196007081        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196008091        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196008261        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA196008261        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196009201        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA196105282        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA196106051        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| SLN196106061        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CIN196106201        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196106291        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| SLN196107171        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| SLN196107181        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196107191        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196107281        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA196108062        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196108081        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| LAN196108161        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196108251        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196108291        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| LAA196205301        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PIT196206051        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196206221        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYN196207191        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196207201        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| LAA196207241        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA196207251        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196207271        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| LAN196208052        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| LAA196208171        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196208200        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196208211        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196208281        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| LAA196306051        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196306302        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196307011        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196307051        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| LAA196307171        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196307271        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196308061        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196308141        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196308201        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196308211        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA196308211        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196308231        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196309061        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PIT196309061        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA196309201        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| WS2196405061        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196406091        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA196406161        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA196406301        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA196407020        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA196407160        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA196407230        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196408051        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196408201        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| MLN196409151        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CLE196409221        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196505241        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196505281        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CLE196506140        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYN196506281        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196507051        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196507081        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196507101        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| MIN196509020        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196509101        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| MIN196605120        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| KC1196605140        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196605201        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196606011        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CHA196606020        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196606041        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYN196606131        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196606131        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BOS196606300        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196607011        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196607041        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196607061        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| SFN196609140        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196609281        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196705101        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196706061        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PIT196706061        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196706151        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196706301        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196707041        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196707181        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196708151        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PIT196708171        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196708251        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196709151        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| OAK196804200        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| OAK196805211        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196805291        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| OAK196806150        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196806181        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| OAK196806220        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196807171        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PIT196807171        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| SLN196807220        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196807261        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196807291        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| LAN196808030        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| LAN196808042        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL196808080        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196808131        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| OAK196808170        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| LAN196808281        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196809021        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196809131        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196809201        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PIT196906171        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| MON196906251        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196907041        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196907091        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| MON196908051        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196908051        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| MON196908121        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CHA196908160        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CLE196909051        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| DET196909060        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PIT196909101        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196909151        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI196909160        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BOS200310140        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| PHI202008052        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYN202204192        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CLE202205072        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYN202205172        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CLE202206072        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| KCA202208092        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CLE202208152        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| NYA202209072        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| MIL202209082        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| SEA202210042        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CHA202304182        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CLE202304222        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CHA202309122        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| DET202404302        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| CHA202405142        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |
| BAL202407292        | d                       | n                   | change gamelogs | Game ended after 20:15:00; night games were common by this time |


| **Home Starting Pitcher ID** |                                     |                                 |                 |                                                                                                                              |
|------------------------------|-------------------------------------|---------------------------------|-----------------|------------------------------------------------------------------------------------------------------------------------------|
| **GAME ID**                  | **home_start_pitcher_id game logs** | **home_start_pitcher_id BGAME** | **Remediation** | **Note**                                                                                                                     |
| CHA202408270                 | flexc001                            | crocg001                        | change gamelogs | crocg001 threw 4 pitches to start the game prior to a weather delay. Source: https://www.espn.com/mlb/recap?gameId=401570457 |

| **PARK ID**  |                       |                  |               |                                                                                                                |
|--------------|-----------------------|------------------|---------------|----------------------------------------------------------------------------------------------------------------|
| **Game ID**  | **park_id game logs** | **Remediation**  | **New Value** | **Note**                                                                                                       |
| ALS202407160 | ARL03                 | change game logs | ARL03         | ARL03 was opened by this date                                                                                  |
| BOS193109071 |                       | change game logs | BOS08         | game played at Braves Field, source: https://chroniclingamerica.loc.gov/lccn/sn99021999/1913-05-31/ed-1/seq-8/ |
| BOS193109072 |                       | change game logs | BOS08         | game played at Braves Field, source: https://chroniclingamerica.loc.gov/lccn/sn99021999/1913-05-31/ed-1/seq-8/ |

## 5. Event Files
- Question marks (?) are used as a NULL value; these are replaced with NULL.
- Dates are standardized to the YYYY-mm-dd format.
- 'Leadoff' and 'game start' columns are replaced with 'inning_progress' and 'game_progress'. These columns have values that indicate the start, middle, and finish of the inning/game with the values 's', 'm', and 'f', respectively.

## 6. BGAME Files
- Dates are standardized to the YYYY-mm-dd hh:mm:ss format to indicate start times (24 hour clock), when available. Separate columns for date and start time are eliminated. In cases where the start time in unknown, the value is 00:00:00.
- Various values used to indicate missing data are replaced with NULL. There are several null indicators: '?', '-1', and '(unknown)' to name a few.
- Attendance: Except for the 2020 season (COVID) and BAL201504290 (civil unrest), the majority of 0 attendance figures are likely single-admission double-headers. We treat these values as missing. Of the remaining, most occur prior to the 1941 season. It seems likely that these are missing; we will treat them as missing. The four modern occurrences are suspended games where the attendance should be considered ambiguous. We treat these values as missing.

## 7. Schedule Files
- Inconsistent file structure:
  - '1904schedule' does not have a file header,
  - '1921schedule' does not have a file header,
  - '1933schedule' does not have a file header,
  - '2024schedule' has an extra column.
- There are two entries for game_id = 'DET202205100'.

## 8. Game Info File
- Inconsistent values for the day/night indicator; these are changed to 'd' and 'n'.
- Dates are standardized to the YYYY-mm-dd hh:mm:ss format to indicate start times (24 hour clock), when available. Separate columns for date and start time are eliminated. In cases where the start time in unknown, the value is 00:00:00.
- The columns season (year), winning team id , and losing team id are dropped as they are easily derived from the existing data.
- Malformed start times are replaced with NULL values:

| Start Time (game info file) | New Value |
|--------------------------|-----------|
| 0.3125                   | Null      |
| 0.333333333333333        | Null      |
| 0.354166667              | Null      |
| 0.375                    | Null      |
| 0.583333333333333        | Null      |
| 0.767361111111111        | Null      |
| 0.833333333333333        | Null      |
| 0.864583333333333        | Null      |
| 12:00:00 AM              | Null      |
| 12:00:00 AM              | Null      |
| 0:00?m                   | Null      |
| (none)                   | Null      |

- Change values of wind direction to align with values from other tables:
  
| **Wind Direction (game info file)** | **Wind Direction (new value)** |
|-----------------------------|--------------------------|
| fromcf                      | from_center              |
| fromlf                      | from_left                |
| fromrf                      | from_right               |
| ltor                        | left_to_right            |
| rtol                        | right_to_left            |
| tocf                        | to_center                |
| tolf                        | to_left                  |
| torf                        | to_right                 |

Reconciling inconsistent values between the game logs, BGAME file, and game info file: The table below indicates the changes and evidence supporting the change.

| **PARK ID**  |                       |                   |                       |                         |               |                                                                                                                  |
|--------------|-----------------------|-------------------|-----------------------|-------------------------|---------------|------------------------------------------------------------------------------------------------------------------|
| ***Game ID** | **park_id Game Logs** | **park_id BGAME** | **park_id Game Info** | **Remediation**         | **New Value** | **Note**                                                                                                         |
| BSN191304191 | BOS05                 | BOS07             | BOS05                 | change bgame/info       | BOS07         | Game played at Fenway; source: https://chroniclingamerica.loc.gov/lccn/sn84020645/1913-04-20/ed-1/seq-14/        |
| BSN191304192 | BOS05                 | BOS07             | BOS05                 | change bgame/info       | BOS07         | Game played at Fenway; source: https://chroniclingamerica.loc.gov/lccn/sn84020645/1913-04-20/ed-1/seq-14/        |
| BSN191305301 | BOS05                 | BOS07             | BOS05                 | change bgame/info       | BOS07         | Game played at Fenway; source: source: https://chroniclingamerica.loc.gov/lccn/sn99021999/1913-05-31/ed-1/seq-8/ |
| NY1191104120 |                       | NYC10             | NYC13                 | change info             | NYC10         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191104130 |                       | NYC10             | NYC13                 | change info             | NYC10         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191106280 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191106290 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191106300 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107010 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107060 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107070 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107080 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107100 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107110 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107120 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107130 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107150 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107180 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107190 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107200 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107210 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191107220 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108110 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108120 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108141 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108142 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108160 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108171 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108172 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108191 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108192 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108210 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108220 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108230 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108241 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108242 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108250 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108260 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108280 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191108290 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191109041 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191109042 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191109070 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191109080 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191109090 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191110061 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191110062 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191110070 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191110121 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NY1191110122 |                       | NYC14             | NYC13                 | change info             | NYC14         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| NYA191205300 | NYC13                 | NYC14             | NYC13                 | change bgame & gameinfo | NYC14         | Played at Polo Grounds v (source: https://chroniclingamerica.loc.gov/lccn/sn83030272/1912-05-31/ed-1/seq-15/)    |
| SLN191104200 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191104210 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191104220 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191104230 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191104240 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191104250 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191104260 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191105270 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191105291 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191105292 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191105301 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191105302 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191105311 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191105312 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106011 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106012 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106020 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106030 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106040 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106050 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106070 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106080 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106090 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106100 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106110 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106120 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106130 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106150 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106160 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106170 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106180 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106271 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106272 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106280 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106290 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191106300 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191107010 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191107020 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191107240 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191107250 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191107260 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191107270 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191107280 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191107290 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191107300 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191107310 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191108020 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191108050 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191108061 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191108062 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191108070 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191108080 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191108090 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109070 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109091 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109092 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109100 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109141 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109142 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109151 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109152 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109171 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109172 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109181 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109182 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109190 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109201 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109202 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109211 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109212 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109220 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109230 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109240 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109270 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109280 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191109300 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191110030 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191110040 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |
| SLN191110050 |                       | STL05             | STL07                 | change info             | STL05         | Log files more accurate given start/end dates in ballparks.csv                                                   |

