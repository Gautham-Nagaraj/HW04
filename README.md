# HW04
Data 601 HW 04 repository. Consists of all the ipynb files and dataset needed to work on the homework.

## Load and Inspect the dataset
Import the libraries necessary for working on the dataset i.e pandas, numpy, matplotlib
Import the dataset using the read_csv method of the pandas library
Use the head/tail method to view the first 5 or last 5 entries of the dataset
![image](https://github.com/user-attachments/assets/8329ff8a-4a4b-4cbe-bc34-fb4638168422)

## Handling missing data
We can use the .isna() function chained with sum() to give us the total number of na values in a column
Once the missing values have been found, we need to either drop the column or fill them with meanigful values
In this case, we are dropping columns that have more than 40% missing values
I have made a separte list of columns that have missing values. It is better to iterate through the columns and append these columns to a list,
rather than manually creating one. It works here as the dataset is very small.
Get the percentage of missing values by dividing the total number of missing values by the number of rows in the dataset -1 (to exclude 1st row)
Now the fill the remaining columns, which have missing values, either using the median/mode depending on the data type of the column
Had a few problems while converting from string to float due to commas. Used .astype() to convert string to float after replacing commas with ''
![image](https://github.com/user-attachments/assets/2bf4953b-47e3-4170-9488-4af7c2c326d6)
![image](https://github.com/user-attachments/assets/d4eb9970-4aa0-4167-8599-56e7c893f6b7)


## Extracting and cleaning data using regex
Extracted values from an 'Object' data type column and replaced it with numeric data using regex extract() method
To obtain valid postal codes ex: T2C 4M3 we use a regex: ^[A-Z][0-9][A-Z][ ][0-9][A-Z][0-9]$
This extracts all the valid postal codes and replaces invalid ones with []
![image](https://github.com/user-attachments/assets/97ba3168-4cd9-4166-ae33-850a75f9264a)
Used generative AI to get code that would clean and extract data from property to names and addresses
**Regex Has been used throughout the exercise file. It has been used wherever the columns contained non-numerical values**
![image](https://github.com/user-attachments/assets/a35095a5-ab47-47ce-a687-c30e2d4d9a74)

## EDA and aggregration
![image](https://github.com/user-attachments/assets/ab887ffe-9b0a-49e1-90fc-632df163dc42)
The above code displays natural gas use vs property year built. 
It was done to understand if properties which are newly built consume more natural gas as it a relative new form of energy
However the below data does not satisfy our initial hypothesis that newly constructed property consume more natural gas
We can also group the cloumns to study the total emissions by a property and sort them by values in descending order to see which property has the most emmisions
![image](https://github.com/user-attachments/assets/5b5b530e-6a11-42e2-8acb-ce77870d243b)
Aggregations
To compute the average energy use intensity for each property we can use the same steps done above
![image](https://github.com/user-attachments/assets/bb682baf-799f-4397-aa9f-b7b892227610)

To compute the total greehouse gas emmission per year we can simply group the data by year ending and Total GHG Emissions (Metric Tons CO2e)
However I did not check that the data type of this column was object, so summing the columns gave an undersired result
Upon replacing the commas with '' and converting it to float data type, summing of the columns worked as intended

## Detecting outliers 
We use the IQR method to find the number of outliers present in the data i.e Q1, Q3 IQR = Q3-Q1
Find the lower and upper bound, this is used to detect the outliers. Since the lower bound is negative we use the min() of the column
To replace the outliers I have used the mask function in pandas that replace values once a certain condition is met
I have replaced the outliers using the median of the column
This reomves all extreme outliers, however outliers within the range will remain

## Data Visualization
We use the groupby function to group the year and site EUI. Once grouped we can use the mean() to get the average

![image](https://github.com/user-attachments/assets/3bcaa85f-27f4-4d6a-8383-381d5272bf5a)

There is an overall decrease in the amount of Site energy use intensity compared to 2019 and 2023
This could be due to number of factors, maybe the machines are more energy efficient
There is a significant decrease in 2020 to 2021 probably due to the lock-down though it increases again it does not go pack to its peak value in 2019

![image](https://github.com/user-attachments/assets/6c98163f-a04a-4541-be62-88b5e10a916c)
Next we plot the top ten building type with highest emissions. 
I have used the sort method and set the ascending flag to false to obtain the series in descending order
THen I have indexed the first 10 values to obtain the 10 biggest emission buildings
Plotting it shows the graph in decending order, it is not necessary to plot them in order, but it looks neat so I left it as is!

![image](https://github.com/user-attachments/assets/095be219-869d-4236-b07f-da32463add76)
For the heatmap we use site EUI for different property times and use year to calculate the mean i.e over the years

## Correlation
![image](https://github.com/user-attachments/assets/3b51d371-4b8b-4081-a3d2-e073702e2355)

A strong linear correlation exists for those variables which have a correlation of 1 or -1
If we refer to the boxplot previously plotted we can see that office has a correlation of 1 vs emissions
THe bigger the building or more number of building a property type has the stronger correlation is associated with emissions
Greater number of building/building size higher the consumption and higher the emmission +1
The inverse can be said about property type having smaller buildings or less number of buildings 
They have a negative correlation with emissions and consumptions

##Hypothesis Testing
![image](https://github.com/user-attachments/assets/e2e84a07-953a-4176-8c2e-3b86d0befcc8)
The null hypothesis is the consideration that both these buildings have the same amount of emission output
The alternate hypothesis is to disprove the model and state there is difference in emission of these 2 buildings
The t-test is used when information is unkown about the population i.e mean and standard deviation unknown
From the above test we can conclude that there is a signifcant difference between emission from an office and a recreational centre
