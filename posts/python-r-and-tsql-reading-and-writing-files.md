<!--
.. title: Python, R and TSQL comparison - Reading and writing files
.. slug: python-r-tsql-comparison-reading-and-writing-files
.. date: 2019-03-30 00:00:00 UTC
.. tags: Python, R, tidyverse, pandas
.. category: 
.. link: 
.. description: 
.. type: text
.. updated: 2019-05-05 08:10:00 UTC
-->

This is the second part of a series of posts showing data wrangling code in Python, R, and TSQL. This part shows read/write options for Excel and CSV. This is not directly applicable to SQL. Therefore, there is no column for TSQL in the table below.

<!-- TEASER_END -->
Both Pandas and R can read/write many other formats than Excel and CSV which I mention in this post. For more information about them, I recommend reading the following pages:<br>

#### Python
* [Pandas](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html)

#### R

* [readr](https://readr.tidyverse.org/) (flat files)
* [dbplyr](https://dbplyr.tidyverse.org/articles/dbplyr.html) (databases)


### Misc
* In Python it is assumed that *numpy* is imported as *np* and *pandas* as *pd*.<br>
* In R it is assumed that the *tidyverse* library is imported.<br>
* If additional packages or installation is necessary it's specified in the table.

# Reading and writing files
| Purpose     | Python                                                                                                                                                                                                                                                                                                                                | R                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :---------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Read csv    | <code>FILEPATH = "path/to/file.csv"<br>**df = pd.read_csv(FILEPATH)**</code><br>[read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)                                                                                                                                                               | <code>FILEPATH <- "path/to/file.csv"<br><br>**df <- read_csv(FILEPATH)**<code><br><br>[read_delim](https://readr.tidyverse.org/reference/read_delim.html)                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Write csv   | <code>FILEPATH = "path/to/file.csv"<br>d = \{"dep":["a", "b", "c"],<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"x": [4, 3, 2],<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"y": [5, 6, 7]\}<br>df = pd.DataFrame(data=d)<br><br>**df.to_csv(FILEPATH)**</code><br><br>[to_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_csv.html)  | <code>FILEPATH <- "path/to/file.csv"<br>dep <- c("a", "b", "c")<br>x <- c(4,3,2)<br>y <- c(5,6,7)<br>df <- data.frame(dep, x, y)<br><br>**write_csv(df, FILEPATH)**<br><br>[write_delim](https://readr.tidyverse.org/reference/write_delim.html)                                                                                                                                                                                                                                                                                                                                     |
| Read excel  | <code>FILEPATH = "path/to/file.xlsx"<br>SHEET = "sheet1"<br><br>**df = pd.read_excel(FILEPATH, sheetname=SHEET)**</code><br>[read_excel](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_excel.html)                                                                                                               | <code>library(readxl)<br>FILEPATH <- "path/to/file.xlsx"<br>SHEET <- "sheet1"<br><br>**df <- read_excel(FILEPATH, sheet=SHEET)**<code><br><br>[readxl](https://readxl.tidyverse.org/)                                                                                                                                                                                                                                                                                                                                                                                                |
| Write excel | <code>FILEPATH = "path/to/file.xlsx"<br>d = \{"dep":["a", "b", "c"],<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"x":[4, 3, 2],<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"y":[5, 6, 7]\}<br>df = pd.DataFrame(data=d)<br><br>**df.to_excel(FILEPATH)**</code><br>[to_excel](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_excel.html) | <code>library(writexl)<br>FILEPATH <- "path/to/file.csv"<br>dep <- c("a", "b", "c")<br>x <- c(4,3,2)<br>y <- c(5,6,7)<br>df <- data.frame(dep, x, y)<br><br>**write_xlsx(df, FILEPATH)**</code><br><br>To be able to install writexl, devtools must be installed via install.packages(). Also, Rtools <br>needs to be downloaded from the following link:<br>[Rtools](https://cran.r-project.org/bin/windows/Rtools/)<br> and writexl via the following code:<br><br><code>devtools::install_github("ropensci/writexl")</code><br><br>[writexl](https://github.com/ropensci/writexl) |