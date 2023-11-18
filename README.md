# census-data-scraper


In this file, we go through the below steps 1-3 in order to create a single csv file [cc-2003-2020.csv](clean/cc-2003-2020.csv) of census data covering years 2003 - 2020.


### Step 1: Get the data from census.gov

There are many folders describing different groups of years. There will be two processes here, one for 2003-2009 and one for 2010-2020. These files download as csv files.
 
Go to this link: [https://www2.census.gov/programs-surveys/popest/datasets/](https://www2.census.gov/programs-surveys/popest/datasets/).

1. For step 2, download the data for years 2010-2020 -- this will be a single file. In the above link, download the file `CC-EST2020-ALLDATA6.csv` located under 2010-2020>>counties>>asrh. Save it under folder `data`.
2. For step 3, download the data for years 2003-2009 -- this will be multiple files. The 2003-2009 data is structured differently, in that we have to download a file for each state and aggregate them. Here you will need to go to the folder titled 2000-2009>>counties>>asrh in the link above.
For each of the following numbers (correlating to state IDS): 1, 2, 4, 5, 6, 8, 9, 10, 11, 12, 13, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, we download the file `cc-est2009-alldata-#.csv`. Save these under folder `data/`

The structure of your project should look like this:

- parent_folder/
    - get-census-data.ipynb
    - data/
        -  CC-EST2020-ALLDATA6.csv
        -  cc-est2009-alldate-1.csv
        -  ...
        -  cc-est2009-alldate-56.csv

 ### Step 2a: Prepare data for years 2010-2020
In this step we deal with years 2010-2020. Let's use the file  `data/CC-EST2020-ALLDATA6.csv`. In this file, we keep the columns with the following headings: SUMLEV (column a) STATE (b), COUNTY (c), STNAME (d), CTYNAME (e), YEAR (f), AGEGRP (h), and any column with the suffix “_FEMALE” in the header (there should be 27 columns with this in the header but double check).
 
We also need to keep the following rows:
for STATE values 1, 2, 4, 5, 6, 8, 9, 10, 11, 12, 13, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56 (these correspond to the state FIPS codes for the contiguous 48 states plus Hawaii, DC, and Alaska). All COUNTY levels for each state should be kept.
 
For YEAR, the following values should be kept: 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 14, where they correspond to July 1st of each year in the data
 
For AGEGRP, 4, 5, 6, 7, 8, 9, and 10 should be kept; these correspond to five year age intervals from 15-19 to 45-49.
 
Save the file as `cc-2010-2020.csv` under folder `clean`. We should have this organization

- parent_folder/
    - get-census-data.ipynb
    - data/
        -  CC-EST2020-ALLDATA6.csv
        -  cc-est2009-alldate-1.csv
        -  ...
        -  cc-est2009-alldate-56.csv
    - clean/
        -  cc-2010-2020.csv

### Step 2b: Prepare data for years 2003-2009
In this step we deal with years 2003-2009, using the files under `cc-est2009-alldate-#.csv` We first clean them by removing unneeded columns and rows before aggregating them together. This data is kept the exact same columns as in Step 2A.
 
For YEAR, the following values should be kept: 5, 6, 7, 8, 9, 10, 11, 13, where they correspond to July 1st of each year in the data
For AGEGRP, 4, 5, 6, 7, 8, 9, and 10 should be kept; these correspond to five year age intervals from 15-19 to 45-49.

Save the file as you go as `cc-2003-2009.csv` under folder `clean`

- parent_folder/
    - get-census-data.ipynb
    - data/
        -  CC-EST2020-ALLDATA6.csv
        -  cc-est2009-alldate-1.csv
        -  ...
        -  cc-est2009-alldate-56.csv
    - clean/
        -  cc-2010-2020.csv
        -  cc-2003-2009.csv

### Step 3: Merge the files  
Merge files `cc-2010-2020.csv` and `cc-2003-2009.csv` under folder `clean/` from step 2 and 3 into one final output file `cc-2003-2020-all-data.csv` under `clean`, to get: 

- parent_folder/
    - get-census-data.ipynb
    - data/
        -  CC-EST2020-ALLDATA6.csv
        -  cc-est2009-alldate-1.csv
        -  ...
        -  cc-est2009-alldate-56.csv
    - clean/
        -  cc-2010-2020.csv
        -  cc-2003-2009.csv
        -  cc-2003-2020.csv # this is the final file 
