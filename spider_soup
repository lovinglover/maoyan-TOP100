import requests
from bs4 import BeautifulSoup
import json
from requests.exceptions import RequestException

def get_one_page(url):
	try:
		response = requests.get(url)
		if response.status_code == 200:
			return response.text
	except RequestException:
		return None

def get_items(soup):
	items = soup.find(class_="content").find_all('dd')
	for i in items:
		# index = i.find(class_="board-index").string
		# name = i.find(class_="name").string
		# image = 'http://' + i.find('img').get('src')
		# star = i.find(class_="star").string.strip()[3:]
		# time = i.find(class_="releasetime").string.strip()[5:]
		# score = i.find(class_="integer").string + i.find(class_="fraction").string
		# print(index,name,image,star,time,score)
		yield {
			'index':i.find(class_="board-index").string,
			'name':i.find(class_="name").string,
			'star':i.find(class_="star").string.strip()[3:],
			'time':i.find(class_="releasetime").string.strip()[5:],
			'score':i.find(class_="integer").string + i.find(class_="fraction").string
		}

def save(content):
	with open('film.txt','a',encoding='utf-8') as f:
		f.write(json.dumps(content,ensure_ascii=False)+'\n')
		f.close()

def main(offset):
	url = "https://maoyan.com/board/4?offset=" + str(offset)
	html = get_one_page(url)
	#print(html)
	soup = BeautifulSoup(html,'lxml')
	for i in (get_items(soup)):
		print(i)
		save(i)


if __name__ == '__main__':
	for i in range(10):
		main(i*10)
