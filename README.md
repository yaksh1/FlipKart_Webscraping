import requests
import datetime
from bs4 import BeautifulSoup
import time
from IPython.core.display import display,HTML

url="https://www.flipkart.com/search?q=ghee&otracker=search&otracker1=search&marketplace=FLIPKART&as-show=on&as=off&as-pos=1&as-type=HISTORY&as-backfill=on"
headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.87 Safari/537.36","Accept-Encoding": "gzip, deflate, br","Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9","Connection":"close","Upgrade-Insecure-Requests": "1",}

page = requests.get(url,headers=headers)
soup = BeautifulSoup(page.content,'html.parser')
soup = BeautifulSoup(soup.prettify(),'html.parser')

items_list = soup.find_all('div',class_='_4ddWXP')

for items in items_list:
  assured= items.find('img',height='21')

  if assured != None:
    title = items.find('a',class_='s1Q9rs').text.strip()
    price = items.find('div',class_='_30jeq3').text.strip()[1:]
    discount = items.find('div',class_='_3Ay6Sb').text.strip() if items.find('div',class_='_3Ay6Sb') else 'No discount'
    stars = items.find('div',class_='_3LWZlK').text.strip() if items.find('div',class_='_3LWZlK') else 'No Rating'
    details = items.find('a',class_='s1Q9rs')['href']
    today = datetime.date.today()


    import csv
    header = ['Title','Price','Discount Offered','Stars','Date']
    data = [title,price,today,discount,stars,details]
    

    with open('C:\\Users\\91635\\Desktop\\Projects\\WebScrapping\\Flipkart Scrapping\\FlipkartScrap2.csv','a+',newline='',encoding='UTF8') as f:
          writer=csv.writer(f)
          writer.writerow(data) 
def ghee():
  url="https://www.flipkart.com/search?q=ghee&otracker=search&otracker1=search&marketplace=FLIPKART&as-show=on&as=off&as-pos=1&as-type=HISTORY&as-backfill=on"
  headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.87 Safari/537.36","Accept-Encoding": "gzip, deflate, br","Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9","Connection":"close","Upgrade-Insecure-Requests": "1",}

  page = requests.get(url,headers=headers)
  soup = BeautifulSoup(page.content,'html.parser')
  soup = BeautifulSoup(soup.prettify(),'html.parser')

  items_list = soup.find_all('div',class_='_4ddWXP')

  for items in items_list:
    title = items.find('a',class_='s1Q9rs').text.strip()
    price = items.find('div',class_='_30jeq3').text.strip()[1:]
    discount = items.find('div',class_='_3Ay6Sb').text.strip() if items.find('div',class_='_3Ay6Sb') else 'No discount'
    stars = items.find('div',class_='_3LWZlK').text.strip() if items.find('div',class_='_3LWZlK') else 'No Rating'
    details = items.find('a',class_='s1Q9rs')['href']
    assured= items.find('img',height='21')
    today = datetime.date.today()


    import csv
    data = [title,price,today,discount,stars,details]
    
    if assured != None:
      with open('C:\\Users\\91635\\Desktop\\Projects\\WebScrapping\\Flipkart Scrapping\\FlipkartScrap2.csv','a',newline='',encoding='UTF8') as f:
        writer=csv.writer(f)
        # writer.writerow(header)
        writer.writerow(data)    
    
  
  
if __name__ == '__main__':
  while True:
    ghee()
    time_wait = 10
    time.sleep(time_wait)
    


