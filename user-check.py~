import bs4
from bs4 import BeautifulSoup
import urllib
import http.cookiejar
import urllib.request
import re
from urllib import parse, request
import sys

html_doc = "http://forum.fddn.network/"
req = urllib.request.Request(html_doc)
webpage = urllib.request.urlopen(req)
html = webpage.read()
soup = BeautifulSoup(html, 'html.parser')

header_dict={'cookie':'JSESSIONID=17pfv38b4nv181gvkjqr66k18h; _gat_nabble=1; _gat=1; v=x; userId=8; password="cWR6haFeih%2FzDfs1D05buWI8wbfU7xvC4tROMVv4uq4%3D"; username="greenbird+%28%E5%A3%B9%E9%9B%B6%29"; _ga=GA1.2.2065514445.1509592811; _gid=GA1.2.1639767535.1510294781','User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/61.0.3163.100 Safari/537.36'}
url = 'http://forum.fddn.network/template/NamlServlet.jtp?macro=manage_users_and_groups&group=All_Users'
req = request.Request(url=url, headers=header_dict)
res = request.urlopen(req)

output = sys.stdout
outfile = open('fddn-email.txt','w')

def A():
    for k in soup.find_all('tr', class_ = 'main-row'):                         
        for a in k.find_all('td', class_ = 'weak-color medium-border-color adbayes-content'):
            print (a.div.a.get_text())

def B():
    html = res.read()
    soup = BeautifulSoup(html, 'html.parser')
    table = []
    for k in soup.find_all('div', style = 'height:25em;overflow:auto'):
        k = k.get_text()
        s = str(k)
        S = s.split('>')
        for ss in S:
            ss = str(ss)
            ss = ss.replace(' ','')
            ss = ss.replace('\n','')
            ss = ss.replace('\t','')
            ss = ss.strip()
            ss = ss.lstrip()
            ss = ss.rstrip()
     #       print(ss)
            sss = ss.split('<')
            if(len(sss) > 1):
                table.append({'name': sss[0], 'email': sss[1]})
   
    print("---------users---------")
    for user in table:
        print(user)
    return table

def C():
    url = 'http://forum.fddn.network/template/NamlServlet.jtp?macro=manage_subscribers&node=1'
    req = request.Request(url=url, headers=header_dict)
    res = request.urlopen(req)
    html = res.read()
    soup = BeautifulSoup(html, 'html.parser')
    table =[]
    
    k = soup.find('table', class_ = 'subscriptions')
    A = k.find_all('tr')
    for a in A:
        b = a.find_all('td')
        if(len(b) > 2):
            table.append({'name': b[1].get_text(), 'email': b[2].get_text()})
       # if(len(b) and b[0].style == 'width:30px;padding:0'):
        #    print(b)

  #  print(table)
 
    print("-------subscribers-------")
    for user in table:
        print(user)
   
    return table

def D(A, B):
    table = []
    for a in A:
        flag = 0
        for b in B:
            if(b['name'] == a['name']):
           #     print('!!!' + b['name'])
                flag = 1

        if(flag == 0):
            table.append(a)

    return table



def E(url):
    req = request.Request(url=url)
    res = request.urlopen(req)
    html = res.read()
    soup = BeautifulSoup(html, 'html.parser')
    table =[]

    K = soup.find_all('div', class_ = 'classic-author-name nowrap')
    for k in K:
        s = k.get_text()
        s = s.strip()
        s = s.replace(' ','')
        table.append({'name': s})

    for user in table:
        print(user)
  
    return table



def printTable(table):
    for a in table:
        print(a['name'])
        print(a['email'])

output = sys.stdout
outfile = open('fddn-email.txt','w')   

userTable = B()
subTable = C() 
print("--------intro--------")  
introTable = E('http://forum.fddn.network/-td8.html') + E('http://forum.fddn.network/-td8i20.html')
table1 = D(userTable, subTable)
table2 = D(userTable, introTable)

sys.stdout = outfile
print('-------users--------')
printTable(userTable)
print("-------subscribers-------")
printTable(subTable)
print("-------not subscribers-------")   
printTable(table1)
print("-------haven't intro-------")
printTable(table2)



