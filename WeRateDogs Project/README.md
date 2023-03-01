## WeRateDogs Twitter Project

### Wrangling Efforts

#### Data Gathering
The data gathering stage involved getting 3 different datasets, all in different ways. For the first dataset which is the twitter_archive data, this was relatively easy to do. All I did was download the file given and read the file into a pandas DataFrame using the pd.read_csv() function.

For the second data, the image_prediction data, I programmatically downloaded the data using the requests library and wrote it's contents into a file. I then read the file into a pandas DataFrame using the pd.read_csv() function, but this time I specified the sep argument as "\t" because the file was tab separated.

For the last data, I was to get the data using twitter's API, I tried doing this but I wasn't able to complete this because it wasn't easy to get twitter to approve the request. So I ended up using the tweet_json file provided by the classroom. While trying to work with the json file, I realised it wasn't properly formatted and formatted it properly in VScode. I then proceeded to read it into my pandas DataFrame using the pd.read_json() function.

#### Assessing The data
For this section, It was required that I detect and document at least eight (8) quality issues and two (2) tidiness issues. I Assessed the data both visually and programmatically, both assessment I did in Jupyter nootebook. For the visual assessment, I used the pd.set_option() function to display all the rows and columns of each of the three datasets, because I didn't want pandas to collapse any row or column. I was able to find 4 issues out of 10 by assessing visually.

For the Programmatic assessment, I used some functions to give me a summary of the data. Functions like info(), which showed me the data types that were incorrect, isnull(), which showed me more columns with missing values that I didn't catch by assessing visually, duplicated(), which I used to check for duplicates in the dataset, and value_counts(), which helped me see distinct values of a column and their counts. After assessing programmatically, I was able to see the remaining 6 issues, which I then documented.

#### Cleaning the data
The cleaning section involved the most work. I also found myself going over the assesing stage to find more about the issues I had highlighted, if they needed to be dropped or not. Although it required the most work, it was interesting, as I got to learn new things as I got my hands dirty.

##### Data Quality Issues:
To fix the missing values I dropped some columns, filled in the median in some missing columns, and dropped some records.
For the the wrong datatypes, I corrected them to their appropriate data types.
I remove records that are not from @dog_rate's official twitter account
##### Data Tidiness Issues:
I melted columns with dog_type values into one column called dog_type.
I merged individual tables to one master table While trying to merge the individual dataset, I made the mistake of merging the the tweet_json file with its id column, instead of id_str. I had to go back and assess the data to investigate why the ids didn't match, and found that the id column that had datatype int was rounded. I was able to fix this, but this is an example of how iterative the wrangle proccess was.


### Insights gotten from the Dataset

1. After exploring the dataset. I found that some ratings were extremely high. The first plot(Figure 1), which is a boxplot, shows that ratings numerator greater than 15 are considered as outliers. I also grouped the ratings numerator into bins and plotted that. The figure 2 below shows that more dogs had the rating numerator between 10 and 15.

#### Figure 1

#### Figure 2

2. I created a function that plots a group plot and passed the dog type feature(without the None Values) and the new ratings bin feature I created to it. Figure 3 which is the output of the group plot function shows that there's no relationship between ratings numerator feature and the dog_type feature.

#### Figure 3

3. I used the pairplot function to check the relationship of some columns and found no relationship between ratings and length of text(I took the end range value from the display_text_range column to create this feature), however, there was a relationship between the favourite and retweet count column and the length of text column.
4. From the pairplot I also noticed a positive relationship between retweet count and favourite count.

#### Figure 4

5. From the timestamp feature, I got a date column which I then used to derive a year and month column. With these new features, I found that the year with the highest retweet and likes was the year 2016, as shown in Figure 5 below. However it was also the year with the highest number of tweets from the dog rates account, so this might be the reason for it's high retweet counts. I also found it interesting that the year 2017 was the year with the lowest number of tweets, but the number of likes that year was almost up to that of 2016.
6. Filtering the data to investigate only the year 2016, I noticed that the month of July had the highest retweet count and the month of October had the highest likes in the year 2016.

#### Figure 5

Most of my analysis work involved finding relationships and correlation, it is important to note that these correlations don't mean causation.
