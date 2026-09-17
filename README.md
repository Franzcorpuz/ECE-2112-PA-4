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

















README FILE VERSION HISTORY

September 14, 2026 - Started with the Codes

September 17, 2026 - Created the Repository

September 17, 2026 - Finished and uploaded the code

September 17, 2026 - Started with the readme file
