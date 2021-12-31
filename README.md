# Collecting-Data-Using-Web-Scraping
Hands-on Lab : Web Scraping
Estimated time needed: 30 to 45 minutes

Objectives
In this lab you will perform the following:

Extract information from a given web site
Write the scraped data into a csv file.
Extract information from the given web site
You will extract the data from the below web site:

#this url contains the data you need to scrape
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/labs/datasets/Programming_Languages.html"
The data you need to scrape is the name of the programming language and average annual salary.
It is a good idea to open the url in your web broswer and study the contents of the web page before you start to scrape.

Import the required libraries

# Your code here
from bs4 import BeautifulSoup
import requests
import pandas as pd
Download the webpage at the url

#your code goes here
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/labs/datasets/Programming_Languages.html"
Create a soup object

#your code goes here
data = requests.get(url).text
soup = BeautifulSoup(data, "html5lib")
Scrape the Language name and annual average salary.

#your code goes here
table = soup.find('table')
for row in table.find_all('tr'):
    cols = row.find_all('td')
    language_name = cols[1].getText()
    annual_average_salary = cols[3].getText()
    print("{}--->{}".format(language_name,annual_average_salary))
Language--->Average Annual Salary
Python--->$114,383
Java--->$101,013
R--->$92,037
Javascript--->$110,981
Swift--->$130,801
C++--->$113,865
C#--->$88,726
PHP--->$84,727
SQL--->$84,793
Go--->$94,082
Save the scrapped data into a file named popular-languages.csv

# your code goes here
import csv
import pandas as pd
table_rows = table.find_all('tr')
l = []
for tr in table_rows:
    td = tr.find_all('td')
    row = [tr.text for tr in td]
    l.append(row)
df=pd.DataFrame(l, columns=["Column1","column2",...])
df
df.to_csv("filename.csv") #this could be used to save data into csv 
​
csv.save('popular-languages.csv')
import os
os.getcwd()
from IPython.display import HTML
import base64,io
​
​
def create_download_link( df, title = "Download CSV file", filename = "/home/wsuser/work/popular-languages.csv"):
    csv = df.to_csv()
    b64 = base64.b64encode(csv.encode())
    payload = b64.decode()
    html = '<a download="{filename}" href="data:text/csv;base64,{payload}" target="_blank">{title}</a>'
    html = html.format(payload=payload,title=title,filename=filename)
    return HTML(html)
​
​
​
create_download_link(df) #this could be used to save data into csv
Authors
Ramesh Sannareddy

Other Contributors¶
Rav Ahuja

Change Log
Date (YYYY-MM-DD)	Version	Changed By	Change Description
2020-10-17	0.1	Ramesh Sannareddy	Created initial version of the lab
Copyright © 2020 IBM Corporation. This notebook and its source code are released under the terms of the MIT License.
