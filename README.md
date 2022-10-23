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
