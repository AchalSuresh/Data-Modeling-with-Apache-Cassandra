# Project: Data Modeling with Cassandra
A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analysis team is particularly interested in understanding what songs users are listening to. Currently, there is no easy way to query the data to generate the results, since the data reside in a directory of CSV files on user activity on the app.

##Overview
Model the data by creating tables in Apache Cassandra to run queries. ETL pipeline transfers data from a set of CSV files within a directory to create a streamlined CSV file to model and insert data into Apache Cassandra tables.

##Datasets
For this project, you'll be working with one dataset: event_data. The directory of CSV files partitioned by date. Here are examples of filepaths to two files in the dataset:

event_data/2018-11-08-events.csv
event_data/2018-11-09-events.csv

Process:

## Part I. ETL Pipeline for Pre-Processing the Files
Data currently resides in a directory of JSON files. We need to create a streamlined CSV file from all these. The final file will be used to extract and insert data into Apache Cassandra tables.

The ETL pipeline converts the csv files into smaller event data csv file called event_datafile_full.csv

The columns in the processed csv file are:
artist
firstName of user
gender of user
item number in session
last name of user
length of the song
level (paid or free song)
location of the user
sessionId
song title
userId


## Part II Data Modeling using Apache Cassandra
In Apache Cassandra, we model our data based on the queries we will perform. Aggregation like GROUP BY, JOIN are highly discouraged in Cassandra. This is because we shouldn't scan the entire data because it is distributed on multiple nodes. It will slow down our system because sending all of that data from multiple nodes to a single machine will crash it.

The tables are being modeled based on the following queries:
1. Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4
2. Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182
3. Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'

