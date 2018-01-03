import sys
sys.path.append('C:\\Program Files\\Anaconda3\\Lib\\site-packages')
import requests
from bs4 import BeautifulSoup as soup
reqMain=requests.get("https://en.wikipedia.org/wiki/List_of_Bollywood_films_of_2014")
soupMain=soup(reqMain.content,"html.parser")
tableAll=soupMain.findAll("table")
##print(len(tableAll))
Release_Date=[]
Movie_Name=[]
Movie_Genere=[]
Movie_Director=[]
Movie_Cast=[]
Movie_Url=[]
Movie_ProdComp=[]
Movie_DistComp=[]
Movie_RunTime=[]
Movie_Budget=[]
Movie_BoxOff=[]
Movie_Ratng=[]
b='https://en.wikipedia.org'

for table in tableAll:
    trAll=table.findAll("tr")
    
    for tr in trAll:
        tdAll=tr.findAll("td")
        if len(tdAll)==6:
            try:
                Release_Date.append(tdAll[0].text[22:])
                Movie_Name.append(tdAll[1].text)
                Movie_Genere.append(tdAll[2].text)
                Movie_Director.append(tdAll[3].text)
                Movie_Cast.append(tdAll[4].text)
                try:
                    Movie_Url.append(b + tdAll[1].a.get("href"))
                    url=b + tdAll[1].a.get("href")
                    reqUrl=requests.get(url)
                    soupUrl=soup(reqUrl.content,"html.parser")
                    mov_info=soupUrl.findAll("table",{"class":"infobox vevent"})
                    print(tdAll[1].text)
                    y1=('Yes:Production Company'if '\nProduction\ncompany\n' in mov_info[0].text else 'No :Production Company')
                    if y1=='No :Production Company':
                        Movie_ProdComp.append("No Production Company Info for this Movie")
                    y2=('Yes:Distributed Company'if 'Distributed by' in mov_info[0].text else 'No :Distributed Company')
                    if y2=='No :Distributed Company':
                        Movie_DistComp.append("No Production Company Info for this Movie")
                    y3=('Yes:Running'if 'Running time' in mov_info[0].text else 'No :Running')
                    if y3=='No :Running':
                        Movie_RunTime.append("No Running Time Info for this Movie")
                    y4=('Yes:Budget'if 'Budget' in mov_info[0].text else 'No :Budget')
                    if y4=='No :Budget':
                        Movie_Budget.append("No Budget  Info for this Movie")
                    y5=('Yes:Box'if 'Box office' in mov_info[0].text else 'No :Box')
                    if y5=='No :Box':
                        Movie_BoxOff.append("No Box Info for this Movie")
                    trUrl=mov_info[0].findAll("tr")
                    for eachtr in trUrl:
                       
                        try:
                            if '\nProduction\ncompany\n' in eachtr.text and y1=='Yes:Production Company':
                                Movie_ProdComp.append(eachtr.td.text.replace('\n','||'))
                        except:
                            print("Issue")
                           
                        try:
                           if 'Distributed by' in eachtr.text and y2=='Yes:Distributed Company':
                                Movie_DistComp.append(eachtr.td.text.replace('\n','||'))
                        except:
                            print("Issue")   
                        try:
                            if 'Running time' in eachtr.text and y3=='Yes:Running':
                                Movie_RunTime.append(eachtr.td.text)
                        except:
                            print("Issue")                         
                        try:
                            if 'Budget' in eachtr.text and y4=='Yes:Budget': 
                                Movie_Budget.append(eachtr.td.text)
                        except:
                            print("Issue")     
                        try:
                            if 'Box office' in eachtr.text and y5=='Yes:Box': 
                                Movie_BoxOff.append(eachtr.td.text)
                        except:
                            print("Issue")  
                except:
                    Movie_Url.append("Detailed Report are not available")
                    Movie_ProdComp.append("Detailed Report are not available")
                    Movie_DistComp.append("Detailed Report are not available")
                    Movie_RunTime.append("Detailed Report are not available")
                    Movie_Budget.append("Detailed Report are not available")
                    Movie_BoxOff.append("Detailed Report are not available")
                   
            except:
                print("Nothing Here")

print("Movies Released in 2015 are")
i=0
for itr in Release_Date:
    print("%10s|| %10s ||%10s||%10s||%10s||%10s" %(Release_Date[i],Movie_Name[i],Movie_Genere[i],Movie_Director[i],Movie_Cast[i],Movie_Url[i]))
    i=i+1

