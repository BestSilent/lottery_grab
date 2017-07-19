#coding:utf8
import urllib2,cookielib
from bs4 import BeautifulSoup


url = "http://baidu.lecai.com/lottery/draw/list/50?type=range_date&start=2012-03-01&end=2017-06-16"
    
def getperiods(hbody):
	period =  hbody.find('a')
	if period != None:
	    return period.string	
def getredballs(balls):
	dict = []
	redball = balls.find("table").find_all("td")[0]
	redballnumber = redball.find_all("em");
	red=""
	for num in redballnumber:
	    "".join(num.string);	
	    dict.append(num.string)	
	return dict	
def getblueballs(balls):
	dict = []
	blueball = balls.find("table").find_all("td")[1]
	blueballnumber = blueball.find("em").string;
	dict.append(blueballnumber)
	return dict
request = urllib2.Request(url)
request.add_header("user-agent","Mozilla/5.0")
response2 = urllib2.urlopen(request)
soup = BeautifulSoup(response2.read())
bigtable = soup.find_all("table")
link_node = soup.find('tbody')
trs = link_node.find_all('tr')
tfile =  open("caipiao.txt","w")
for tr in trs: 
    period = getperiods(tr)
    if period != None:
        redball = getredballs(tr)
        blueball = getblueballs(tr)
        #str = period+'\t'+redball+'\t'+blueball		
        tfile.write(period+"\t"+",".join(redball)+"\t"+"".join(blueball)+"\n")		
   # print period;	
tfile.close



	
