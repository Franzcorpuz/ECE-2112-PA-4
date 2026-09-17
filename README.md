# ECE-2112-PA-4
Made by: Franz Justin M. Corpuz | 2ECE-D

The content of this repository contains the Programming Assignment 4 for our course ECE2112 Advanced Computer Programming. This assignment combines the different functions of Pandas and Matplot to use more functions such as to filter tabular data using different conditions, construct focused DataFrames, summarizing the relationship between categorical features and numerical variables, and data comparison using clear and properly labeled plots. 

# Importation of Libraries
Before the coding for this Programming Assignment starts, the Pandas and Matplot library must be imported into the notebook to be able to use most of the functions that are needed to fulfill the requirements in this assignment.

Below is the syntax for the libraries to be able to use their functions and to efficiently call them.
```python
import pandas as pd
import matplotlib.pyplot as plt
```

# Board 2 Table
To fulfill all the functions and operations that will be used, this table is needed, since everything revolves around it [View board2.xlsx](board2.xlsx).

For Python to read the .xlsx file, it needs this syntax:
```python
board2 = pd.read_excel('board2.xlsx')
```

# Input of the Average column
Since the Average is needed for all parts of this assignment the average columns need to be computed and concatenated to the Dataset Board 2.

Attached below is the syntax used:
```python
board2['Average'] = board2[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
```
This function computes for the mean across the different subjects to add to a column named 'Average'. This function also checks if there is already an existing column named average in which this would only edit the content, but when it detects that it does not exist it automatically adds the Average column.

# A. VISAYAS COMMUNICATION DATAFRAME
**Objective:** Create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track
is Communication. Retain only columns;Name, Gender, Math, Electronics, Average
Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to
the source dataset before the columns are selected.

To implement the two filters the following operations and functions were used.
```python
Vtrack = board2.loc[board2['Track'] == 'Communication']
homeTV = Vtrack.loc[Vtrack['Hometown'] == 'Visayas']

hometvselcol = homeTV.loc[:,['Name', 'Gender', 'Math', 'Electronics', 'Average']]
```
The 'Vtrack' and 'homeTV' variable is the first part of the filter that selects only the Communication track and the ones whose hometown is in Visayas. Therefore, minimizing the pool where the second filter would be applied. While the second part of the filter is the 'hometvselcol' where it selects and display the columns that are encoded within the syntax. The .loc was also used so as to not change or modify the main Dataset when performing functions.

To create the VisComm DataFrame the 'hometvselcol' is used to create the main DataFrame named VisComm since it is the data set that has gone through the filters. Below are the functions and operations used to create the DataFrame and to show the number of rows of the DataFrame.
```python
VisComm = pd.DataFrame(hometvselcol)
print(f'Number of rows: {len(VisComm)}')
```

# B. VISAYAS FEMALE DATAFRAME
**Objective:** Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and
whose Gender is Female. Retain only:
Name, Track, GEAS, Electronics, Average
Display VisFemale. Then display only the rows of VisFemale whose Average is at least 60.

For Part B. almost all the process is the same for Part A. such as the two-part filter but in this part of the assignment the filter is changed to filter those whose hometown is Visayas and gender is Female. The columns that need to be displayed is also changed but the syntax is generally also the same.

The following operations and functions were used.
```python
Vhomet = board2.loc[board2['Hometown'] == 'Visayas']
Fvhomet = Vhomet.loc[Vhomet['Gender'] == 'Female']

Filtfvhomet = Fvhomet.loc[:,['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
```
'Vhomet' and 'Fvhomet' is used to filter the data set to only show those who lives in Visayas and is female. While Filtfvhomet is the second filter used to only select the columns that are encoded.

The following operations and functions were used to create the VisFemale DataFrame.
```python
VisFemale = pd.DataFrame(Filtfvhomet)
```

Lastly for this Part B. a third filter is needed but it should not alter the results inside the DataFrame VisFemale so the syntax below is used to display the DataFrame and at the same time check is the average of the one being displayed is greater than or equal 60 if it is less than 60 it automatically excludes it from the list but it does not remove it.
```python
display(VisFemale[VisFemale['Average']>=60])
```

# C. CATEGORY-AVERAGE VISUALIZATION
**Objective:** Examine how the recorded Average differs across the three categorical features Track, Gender, and
Hometown.

a. For each feature, compute the mean of Average for every category using Pandas.

b. Display the three summary tables.

c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by
Hometown.

d. Below the figure, write three concise statements identifying the category with the highest sample
mean for each feature.

Attached below are the different functions and operations to fulfill Part C.
```python
mean_track = board2.groupby('Track')['Average'].mean().reset_index()
mean_gender = board2.groupby('Gender')['Average'].mean().reset_index()
mean_hometown = board2.groupby('Hometown')['Average'].mean().reset_index()
```
The same syntax is used for all three applications but the columns where it would be extracted from is different thus the only modification in the syntax. The syntax groups the Data depending on the input such as the track, gender, and hometown which then computes for the mean for the averages of each person and compiles and groups it by track, gender, and hometown.

```python
display(mean_track)

display(mean_gender)

display(mean_hometown)
```
The function display is used to display the computed mean of averages for each category. Display is used since it is better than only using the print since print alters the look of the DataFrame while with display it shows it similar to the display of the DataFrame.

```python
fig, axes = plt.subplots(1, 3, figsize=(18, 5))

axes[0].bar(mean_track['Track'], mean_track['Average'], color='Yellow', edgecolor='black')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Mean Average')
axes[0].set_title('Mean Average by Track')
axes[0].set_ylim(0,80)

axes[1].bar(mean_gender['Gender'], mean_gender['Average'], color='Blue', edgecolor='black')
axes[1].set_xlabel('Gender')
axes[1].set_ylabel('Mean Average')
axes[1].set_title('Mean Average by Gender')
axes[1].set_ylim(0,80)

axes[2].bar(mean_hometown['Hometown'], mean_hometown['Average'], color='Green', edgecolor='black')
axes[2].set_xlabel('Hometown')
axes[2].set_ylabel('Mean Average')
axes[2].set_title('Mean Average by Hometown')
axes[2].set_ylim(0,80)

fig.text(0.125, 0.0, 'Interpretation', weight='bold', fontsize=10)
fig.text(0.125, -0.1, '(a.) The highest mean average for track is from Communication which is 67.975\n(b.) The highest mean average for gender is from Males which is 67.183\n(c.) The highest mean average for Hometown is from Luzon which is 68.083', fontsize=10)
plt.show()
```
For part C and D I combined everything in one cell.

Methods used:

The function `fig, axes = plt.subplots(1, 3, figsize=(18, 5))`s used to create the graph since it creates 1 row and 3 columns of bars for the graph while the figsize part dictates how big each bar is.

To create and visualize the graph, these standard functions and operations were used for each category. This is also the same line of code that would be used in the different category, except for the variable names and the 'axes'. 'axes[0].bar(mean_track['Track'], mean_track['Average'], color='Yellow', edgecolor='black')' was used to create the bar od the graph where in the data will come from the track group and teh column Average you canalso set the color of the bar and its outline color. 'axes[0].set_ylabel('Mean Average')' and 'axes[0].set_xlabel('Track')' sets the label for each axis such as the Track on the x-axis and the Mean Average on the y-axis. 'axes[0].set_title('Mean Average by Track')' sets the title for the specific bar of the graph below the x-axis label. Lastly, 'axes[0].set_ylim(0,80)' sets the y-axis limits to display the range 0 to 80, making the graph easier to read.

For interpreting the graphs, the 'fig.text' functions were used. I cannot paste it here since it would be too long, but the first figure text function establishes the Title of the interpretation, which in this case is Interpretation. While the second fig.text was used was the analysis of the graphs which is written normally.












README FILE VERSION HISTORY

September 14, 2026 - Started with the Codes

September 17, 2026 - Created the Repository

September 17, 2026 - Finished and uploaded the code

September 17, 2026 - Started with the readme file

September 18, 2026 - Minor revisions andfinalized teh readme file
