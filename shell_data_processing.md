pip install csvkit

in2csv : converting files (in tabular data) i.e excel to csv 

in2csv spotifydata.Xlsx > spotifydata.csv
spotifydata.Xlsx : is the original data
> : is the redirect operator for redirecting and saving an output
spotifydata.csv: newly generated csv data

To vide all the sheet name in an excel document
we use --names or -n flag with the command below

in2csv -n spotifydata.xlsx

which will print the available output for example:
Worsheet1_popularity
Worsheet2_musicAttributes

if the file we want to convert is for example Worsheet1_popularity, we do

in2csv spotifydata.xlsx --sheet 'Worsheet1_popularity' > spotify_popularity.csv

To confirm the creation of new csv: ls 

To view the content of csv data

csvlook spotify_popularity.csv

To view the details of the csv data, we use csvstat

csvstat spotify_popularity.csv


FILTERING DATA USING CSVKIT

csvcut : filters data using column name
csvgrep : filters data by row through exact match, pattern matching or regex

To print all column names in csv
csvcut -n spotify_MusicAttributes.csv

Getting data from the first column in the csv (getting data by column number)
csvcut -c 1 spotify_MusicAttributes.csv

For muiltiple columns
csvcut -c 2,3 spotify_MusicAttributes.csv

returning only the first column in the data by name
csvcut -c "customer_name" spotify_MusicAttributes.csv

for multiple column by name
csvcut -c "customer_name", "address" spotify_MusicAttributes.csv


FILTERING DATA BY ROW VALUES

Question: Find in the csv where track_id = '5RCBAGSFSF"

csvgrep -c "track_id" -m 5RCBAGSFSF spotify_popularity
or 
using the column position
csvgrep -c 1 -m 5RCBAGSFSF spotify_popularity

STACKING DATA AND CHAINING COMMANDS WITH CSVKIT
csvstack: stacks up the rows from two or more csv files
But is better to use when two different csv has similar data

csvstack Spotify_Rank6.csv Spotify_Rank7.csv > Spotify_Allranks.csv

In order to indicate the source of resultant data in Spotify_Allranks.csv
a new column will then be created which indicate where the data are coming from either Spotify_Rank6.csv or Spotify_Rank7.csv which is represented by "Rank6" and "Rank7" respectively.

csv -g "Rank6", "Rank7" \ Spotify_Rank6.csv Spotify_Rank7.csv > Spotify_Allranks.csv

in order to rename the new column from group to source:
csv -g "Rank6", "Rank7" -n "source" \ Spotify_Rank6.csv Spotify_Rank7.csv > Spotify_Allranks.csv

Chaining command-line commands
; : links command together and run sequentially, example below
csvlook Spotify_Allranks.csv; csvstat Spotify_Allranks.csv

&& : links commands together but only runs the 2nd command if the 1st succeeds
csvlook Spotify_Allranks.csv && csvstat Spotify_Allranks.csv

| : uses the output of the 1st command as input to the 2nd command
csvcut -c "track_id", "danceability" Spotify_Allranks.csv | csvlook

IMPORTANT : \ indicate that we are writing to te next line as the syntax is very long, line break is use to keep code clean and readable 

PULLING DATA FROM THE DATABASE USING SQL2CSV
for more options: sql2csv -h

Sample syntax
sql2csv --db "sqlite:///SpotifyDatabase.db" \ --query "SELECT * FROM Spotify_Popularity" \ > Spotify_Popularity.csv

Manipulating a csv file in sql query format

csv --query "SELECT * FROM Spotify_Popularity LIMIT 1" \ Spotify_MusicAttributes.csv
To beautify the above result, we do:
csv --query "SELECT * FROM Spotify_Popularity LIMIT 1" \ Spotify_MusicAttributes.csv | csvlook

Joing:
csvsql --query "SELECT * FROM file_a INNER JOIN file_b" file_a.csv file_b.csv
NOTE: SQL QUERY MUST BE WRITTEN IN ONE LINE, NO BREAKS

PUSHING CSV DATA BACK TO THE DATABSE
You might need to create an empty table before running the script below
csvsql --db "sqlite:///SpotifyDatabase.db" \ --insert Spotify_MusicAttributes.csv

if data has a number columns that shows attribute of text column, we use this command below, scvsql will treat the column as text weither it looks like numbers, date or string
no-constraints allows table to be created without character length limit or null checks
csvsql --no-inference --no-sconstraint \ --db "sqlite:///SpotifyDatabase.db" \ --insert Spotify_MusicAttributes.csv