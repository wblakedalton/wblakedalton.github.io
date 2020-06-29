---
layout: post
title:      "Pandas Data Cleaning Techniques"
date:       2020-06-29 14:53:37 -0400
permalink:  module_1_final_project
---


   This project was the first truly exploratory data science work I took on and could feel overwhelming at times. I found myself digging through provided data sets and asking myself in what direction to go. Analyzing large sets of data can be tricky to wrap your head around at first, as the data you're exploring can seem formidable and not present a clear path in the beginning. The first step to making this work is to clean your data so that it is easier to work with. I discovered these particular data cleaning techniques to be useful when working on the Module 1 Final Project.
 	 
   I found it was easiest to begin by looking at the head() of each pandas dataframe that I created to get an understanding of what was contained within each data set. I then inspected each dataframe using .info() to learn what type of data was in each row and if any values seemed to be missing based on the number of rows. A simple way to determine how many missing values are contained within each column is to use .sum() in conjunction with .isna() to return a value.
	 
`df.isna().sum()`

   The NaN values could then be changed to usable values and removed completely. For numeric columns in this project, I opted to change the missing data to 0's as it would allow me to still work with the other information contained in each row. The missing data is changed by using .fillna() and choosing what to replace every NaN value with for each column. Inplace must be True in order for the change to be permanent.
	 
`df['column_name'].fillna(0, inplace=True)`
	 
   The next step in cleaning up the data was to look for duplicates, as they will skew the data if they are not removed. A new dataframe can be created by slicing the original dataframe to view which data has been repeated. A specific column must be chosen when looking for duplicates, and categorical data types tend to be the best for this approach. The duplicated() function is used on a specific column to return any values that are the same. If you then print the length of the new dataframe, it will reveal how many duplicate values there are in your original dataframe.
	 
```
duplicate_df = df[df['column_name'].duplicated()]
print(len(duplicate_df))
```
	 
Once you know how many duplicates are in your original dataframe, they must be removed to prevent the data from interfering with your analysis. In order to decide which duplicate to drop, the rows can be sorted by another column that contains numeric data and the row with the undesired data can then be removed. This is done by using the sort_values() function in conjunction with the drop_duplicates() function and placing the sliced information into a new dataframe that is clean.

```
clean_df = df.sort_values('numeric_column_name', ascending=False).drop_duplicates(categorical_column_name')
```

Now that missing and duplicate data has been removed from the dataframe you are analyzing, we must make sure the data type of each column is the correct type to work with as numerical data is required for plotting. The .info() method returns what data type is contained within each column. Sometimes, data that looks numerical is stored as categorical data and must be changed. If the values in these columns contain characters that are not numbers like a dollar sign($) or comma(,), the characters must be removed before the data type can be altered. The column is selected based on its name and then str.replace() is used to remove any non-numeral characters and astype() is used to assign the desired data type to the column. If the value contains multiple different characters that need to be removed, the str.replace() function can be repeated.

```
df['column_name'] = df['column_name'].str.replace(',','').str.replace('$','').astype(float)
```

The dataframe has now been thoroughly cleaned and the process can be repeated on other dataframes. Once our dataframes are cleaned, its possible to begin plotting them or running calculations on them in order to find useful information. While large data sets can seem daunting at first, by cleaning the data found in each set you will find it much easier to begin analyzing the data.
