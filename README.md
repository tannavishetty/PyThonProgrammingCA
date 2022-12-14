# PyThonProgrammingCA
CA One Python Programming
Objective:- The following website will be used to acquire data using APIs for this assignment:- The root URL of this API is https://musicbrainz.org/ws/2/
27/11/2022:- Trying to get data from musicBrainz.com but running into errors. 
30/11/2022:- Colab link https://colab.research.google.com/drive/1yZP5BkVIfWJD4NFUtqfP1WrJpyujGZMn?usp=sharing
________________________________________________________________________________________________________________________
Added code to extract each column using beautiful soup
Added code to extract data from multiple pages as shown below. This was done because the data on each page was limited, so extracting data from mutiple pages. 
for page in pages:
  print("Importing page", page)
  url = "https://musicbrainz.org/search?query=2022&type=release&limit=100&method=direct&page=" + page 
  response=requests.get(url)
________________________________________________________________________________________________________________________

The release event column had nested lists within them as shown below. These were particularly challenging to clean.
Created a For loop to extract data from individual list tags. 
The loop further extracts the country name from the title attribute and stores it as a list. 
The list then is updated to the final dataframe.
0     {"events":[{"date":{"year":2022,"month":1,"day...
1     {"events":[{"country":{"entityType":"area","is...
2     {"events":[{"country":{"gid":"525d4e18-3d00-31...
3     {"events":[{"country":{"gid":"525d4e18-3d00-31...
4     {"events":[{"country":{"iso_3166_2_codes":[],"...
                            ...                        
95    {"events":[{"date":{"year":2022,"day":22,"mont...
96    {"events":[{"country":{"iso_3166_3_codes":[],"...
97    {"events":[{"date":{"day":24,"month":10,"year"...
98    {"events":[{"country":{"iso_3166_3_codes":[],"...
99    {"events":[{"country":{"begin_date":null,"end_...

After the chnages the data looks like - 
0     [Worldwide]/2022-01-07
1          Brazil/2022-01-03
2     [Worldwide]/2022-01-31
3     [Worldwide]/2021-12-31
4     [Worldwide]/2022-01-15
               ...          
95    [Worldwide]/2022-10-14
96          Japan/2021-12-24
97    [Worldwide]/2022-08-23
98    [Worldwide]/2022-08-23
99    [Worldwide]/2022-08-23
__________________________________________________________________________________________________________________________
Split the country and the date columns into two separate columns based on the delimeter "/". The columns are displayed as follows - 
Country	      Date
Germany	      2019-03-08
[Worldwide]	  2021-08-13
__________________________________________________________________________________________________________________________
The Date column had varied date formats, changed it's datatyoe from object to datetime that aligned all the date formats. 
__________________________________________________________________________________________________________________________
Similar to the Country/Date column, the language column also displayed abbeviations. As part of data preprocessing, extracted the value of the title attribute to get the full detail of the column. The abbreviation was not making much sense and it needed cleaning. 
Perviously:-
Language
eng/latn	
eng/latn

After preprocessing:- 
Language
English/Latin	
English/Latin
__________________________________________________________________________________________________________________________
The Tracks column had strings in the format "10 + 14 + 8 + 2". 
Created a function to convert read the string, extract the integer value based on the "+" delimeter. 
Sum all the values and store it in the dataframe. 
__________________________________________________________________________________________________________________________
Added code to detect and remove duplicate rows from the dataframe. There were three particular columns (barcode, label and catalog#). 
These columns were not adding any value to the dataset and had many NULL values. so dropped these columns. 
__________________________________________________________________________________________________________________________

__________________________________________________________________________________________________________________________
Renamed few columns to more meaniingful names and stripped all the columns with any leading and trailing whitespaces. 
__________________________________________________________________________________________________________________________
To derive more meaning out of the data - 
checking null values 
checking for unique values 
statistical information 
__________________________________________________________________________________________________________________________
The final cleaned dataframe is now inserted into a Mongodb table using MongoDB Atlas. 
The database "MusicBrainz" and the table "MusicReleases" are successfully created on MongoDB Atlas. 
