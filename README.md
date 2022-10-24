# LSE_DA_NHS_analysis_rohit
You are part of a team of data analysts that was contracted by the National Health Services (NHS), a publicly funded healthcare system in England. The NHS incurs significant, potentially avoidable, costs when patients miss general practitioner (GP) appointments. The reasons for missed appointments need to be better understood as explained by The British Medical Association (BMA) chair Professor Philip Banfield:
            "While it is frustrating when patients do not attend, the reasons why this happens should be investigated rather than simply resorting to punishing them.      Financially penalising patients inevitably impact the poorest and most vulnerable in the community (GP Practice News 2022)." 

Therefore, reducing or eliminating missed appointments would be beneficial financially as well as socially. The government needs a data-informed approach to deciding how best to handle this problem. At this stage of the project the two main questions posed by the NHS are:

    -Has there been adequate staff and capacity in the networks?
    -What was the actual utilisation of resources?

As you are new to Python, your role on the team is to get started with the data exploration, data wrangling, visualisations, and identifying possible trends in the data sets. For this, you’ll investigate:

    -What is the number of locations, service settings, context types, national categories, and appointment statuses in the data sets?
    -What is the date range of the provided data sets, and which service settings reported the most appointments for a specific period?
    -What is the number of appointments and records per month?
    -What monthly and seasonal trends are evident, based on the number of appointments for service settings, context types, and national categories?
    -What are the top trending hashtags (#) on Twitter related to healthcare in the UK?
    -Were there adequate staff and capacity in the networks?
    -What was the actual utilisation of resources?
    -What possible recommendations does the data provide for the NHS?
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------
                                                                    WEEK 2
Necessary libraries for the running of code were imported to the Jupyter notebook using the import function. The 3 datasets were imported to the notebook using the appropriate pandas read_() function. None of the datasets were found to have null values. Descriptive statistics were used to find the spread of the data of each dataset using the describe() function. Only the column count_of_appointments in all three data sets were of the data type int64. The count_of_appointments contains the total number of appointments made on a particular day at a particular location.
The 3 things which we wanted to check were:

                   1.How many locations are there in the dataset?
This was found by using the ‘national_categories’ dataset. The value_count() function was used first and returned a Series containing counts of unique rows in the dataframe, count()was used to return the number of elements with the specified value. The output was printed using the print()function.

                    2. What are the five locations with the highest number of records?
The value_count()function was used first and returned a Series containing counts of unique rows in the dataframe and then was sorted using the sort_values function. The output was printed using the print()function.

                    3. How many service settings, context types, national categories, and appointment statuses are there? 
 The answer to these followed the steps taken for the first question.
 
 ------------------------------------------------------------------------------------------------------------------------------------------------------------------------
                                                                      Week 3

The appointment date column in the actual duration column has to be converted from a string to a datetime format, this was done with the to_datetime() function. Once the format is changed, the first date and the last date can be found using the max() and min() functions. The output can be displayed using the print() function.

To find the most popular service setting for NHS North West London from 1 January  to 1 June 2022, first, the nc dataframe was subsetted to use only the columns required as the nc dataframe is large. 

Then the subsetted dataframe was filtered to include only the dates from 1 January to 1 June 2022. This was done by using the Boolean expression. The code is as follows: 
nc[(nc['appointment_date'] >= "2022-01-01") & (nc['appointment_date'] <= "2022-06-01")]

Then this filtered dataframe was again filtered to include only the location with the word ‘W2U3Z’. This was done using the apply() and lambda() function. The code is as follows:
df2[df2['sub_icb_location_name'].apply(lambda x:'W2U3Z' in x.title())]

To specify the date as 1 January 2022 to June 2022, the appointment date was changed to string format using the dt.strftime('%d %B %Y') function.

groupby() was used to group the dataframe by service_setting and sub_icb_location_name. And then, using the agg() function, the count of sub_icb_location_name was done, which was then sorted using sort_values(by=’ sub_icb_location_name’,’count’) in descending order.

The appointment_month column was split into month and year using dt.year and dt.month. Using the grouby() function, grouped the year and month column and then using the sum() function, summed the count_of_appointments and sorted it by descending order.

The total number of records per month can be found by grouping the month and year using groupby() function and using count() function on count_of_appointments column to return the number of records.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

                                                                     Week 4

Create three visualizations indicating the number of appointments per month for service settings, context types, and national categories.
For this, created 3 subsets, one each for service settings, context types, and national categories.
For each subset, use the groupby() function to group it by appointment month and the categories (service settings, context types, and national categories).  And then aggregate them with the sum of the count_of_appointments.
Now create a line plot using seaborn, with appointment_month on the x-axis and count_of_appointments on the y-axis, with hue as the categories (service settings, context types, and national categories).

To visualize the 4 seasons, create a separate data set by choosing only the required month. And then use the groupby()function to group it by appointment month and service_setting.  And then aggregate them with the sum of the count_of_appointments. Now create the line plot using seaborn, with service_setting on the x-axis and count_of_appointments on the y-axis. 

Plots are saved using the plt.savefig().

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

                                                                       Week 5

The tweet dataset was loaded using the read_csv() function. The metadata was explored using the info() function. 5 columns are of object type, 3 columns are of integer type, and 2 are of boolean type. Using the isna().sum() function, it was found that 167 of 1174 entries of ‘tweet_entities_hashtags’ are missing. The column ‘tweet_full_text’ was used to extract all the hashtags using a for loop and was assigned to a variable ‘tags’. This series was then converted to a dataframe using pd.DataFrame() and the unique number of hashtags were found using value_count. The columns of the dataframe were renamed using the rename() function. The records with a count lesser than 10 were removed from the dataframe to create a line plot. The overrepresented hashtags were removed by excluding the count of 41 and above. 

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

                                                                        Week 6
                                                                        
Use the max() & min () function to find the first and last dates in the appointments_regional dataframe. 
Filter the months to use data from 2021-08 onwards. Create a new dataframe (ar_agg_grpby) and aggregate the total number of appointments using the grouby() and sum() functions.
Create another dataframe (ar_df) and aggregate the total number of appointments using the grouby() and sum() functions. Create a column in ar_df which calculates the utilization of appointments per day, based on the fact that NHS can handle 1.2million per day. This was done by using the assign() and lambda functions.
A line plot for total monthly appointments and monthly capacity utilization is plotted using Seaborn. Likewise, the other line plots were done using these dataframe and Seaborn.

Box plots were created using the subset of the national_categories dataframe aggregated and grouped earlier. The second boxplot was created using the not equal (!=) to condition in the service_setting column for General Practice.

