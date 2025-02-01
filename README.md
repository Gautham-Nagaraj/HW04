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
