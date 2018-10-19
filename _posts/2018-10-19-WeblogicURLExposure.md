```python
import requests
import urllib3

with open('H:\\Desktop\\test\\meituan.txt','r') as fr:
    list=[]
    for domainString in fr.readlines():
        list.append(str(domainString).strip())
    print(list)

targetURL=[":7001/uddiexplorer/SearchPublicRegistries.jsp?operator=http://localhost&rdoSearch=name&txtSearchname=sdf&txtSearchkey=&txtSearchfor=&selfor=Business+location&btnSubmit=Search",":7001/wls-wsat/CoordinatorPortType"]
schema=['http://','https://']
ua = {'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; WOW64; rv:40.0) Gecko/20100101 Firefox/40.1',}
with open('H:\\Desktop\\test\\result.txt','w+') as fw:
    for domain in list:
        for sche in schema:
            print("URL: " + sche + domain + targetURL[1])
            try:
                rsp = requests.get(sche + domain + targetURL[0],headers=ua,verify=False,timeout = 0.5)
                if "service" in str(rsp.text).lower():
                    print(rsp.text)
                    fw.write(rsp.text)
                    fw.write('=' * 30 + '\n')
                    fw.write('\n')
                else:
                    print("*" * 20 + " Not qualified" + "*" * 20)
            except Exception as e:
                print(e)



```
