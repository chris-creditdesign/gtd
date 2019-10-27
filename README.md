# Infographic exploring the Global Terrorism Database

## Get the data

First things first download the entire GTD dataset from [http://www.start.umd.edu/gtd/contact/](http://www.start.umd.edu/gtd/contact/)

## CSVKIT

To inspect the data we'll used CSVKIT "a suite of utilities for converting to and working with CSV, the king of tabular file formats." [https://csvkit.readthedocs.org/en/0.9.0/](https://csvkit.readthedocs.org/en/0.9.0/)

Install CSVKIT with the command:

	pip install csvkit

Convert the provided Excel file into the csv format. (This might take a while).

	in2csv ref/globalterrorismdb_0814dist.xlsx > ref/gtd_full.csv

Create a new file containing a list of gtd_csv's headers. Not essential but useful for seeing what we've got to work with.

	head -n 1 ref/gtd_full.csv | tr , '\n' > ref/headers.txt

Or use csvcut to get line numbers:

	csvcut -n ref/gtd_full.csv > ref/headers.txt

From these columns I'd like to take a look at: 

<!-- -	**eventid**
-	**iyear**
-	**country_txt**
-	**region_txt**
-	**city**
-	**latitude**
-	**longitude**
-	**summary**
-	**attacktype1_txt**
-	**targtype1_txt**
-	**gname**
-	**nkill**
-	**nkillter**
-	**nwound**
-	**nwoundte**
-	**addnotes** -->

line number | Column name
------------- | -------------
 1  | eventid
 2  | iyear
 3  | imonth
 8  | country
10  | region
13  | city
14  | latitude
15  | longitude
29  | attacktype1
35  | targtype1
59  | gname
98  | nkill
00  | nkillter
01  | nwound
03  | nwoundte

Now make a new file with just those columns. This helps us trim that massive 100mb file to a slightly more manageable size.

<!-- 	csvcut -c eventid,iyear,country_txt,region_txt,city,latitude,longitude,summary,attacktype1_txt,targtype1_txt,gname,nkill,nkillter,nwound,nwoundte,addnotes ref/gtd_full.csv > data/gtd_edit.csv
 -->
	csvcut -c 1,2,3,8,10,13,14,15,29,35,59,98,100,101,103 ref/gtd_full.csv > data/gtd_edit_small.csv
