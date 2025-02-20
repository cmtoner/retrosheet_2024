# retrosheet_2024
Tool for extracting and organizing the second of the Retrosheet 2024 semi-annual udpates.

Retrosheet publishes a semi-annual update to their data downloads. This notebook collects the updated files, compiles and converts them to a series of flat .CSV files with a minimal amount of data duplication for easy uploading into a relational database. In the process, this tool attempts to correct any known errors and inconsistencies. It is intended to run in Google Colab. 

The following sections detail the discovered errors, incosistencies, and changes made to the source data.

## 1. Extracting the *ZIP* Files
The *bevent* extraction utility provided by Retrosheet fails to completely extract the *2021AS.EVE* event file. There is no obvious malformation of the source file, *ROS* (roster) file, or *TEAM* file that would cause this error. As a result, the events for this game are not recorded in the event files.

## 2. Biodata
- The *UMPIRES1939.txt* file has and entry for Finnis Brenaham (id=brenu901);
- *UMPIRES1931.txt* has Brenham (no first name; id=brenu902);
- *UMPIRES1940.txt* has Finnis Brenaham (id=brenu902);
- Biodata does not have an id brenu901.

We assume Finnis Brenaham (id=brenu901) is correct and should have an id of brenf901. All other entries are adjusted accordingly.


## 3. Parks
The parks data has several changes from the Retrosheet source file:
- The columns are expanded to city, state, and country.
- Countries are identified by three-letter codes described by the ISO 3166 standard.
- States, whenever possible, are identified by the formal postal abbreviation of the jurisdiction in question. Typically, this is a two, three or four-character code except for London, England. In this case, 'England' is given as the state and 'GBR' is the country code.
- Dates are standardized to the YYYY-mm-dd format.

## 4. Game Log Files
- Name columns are removed as they are redundant with the player/manager/umpire id codes.
- Dates are standardized to the YYYY-mm-dd format.
- Day of the week column is dropped since it is easily determined with by virtually every software package.
- Values of -1, used to indicate missing data, are converted to NULL values.
- Columns containing alpha-numeric code are converted to lowercase, except for game ids, team ids, league ids, and park ids.

The game logs also contain instances where values disagree with values in the *bgame* and *gameinfo* files. In the charts below, the columns where incorrect values were discovered, the corrected value, and the rational for making the changes are described in detail.

|   |             |    **GWRBI**                    |                                           |
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
