# SCRZScrapper
SCRZScrapper is tool for scrap content, title, image from article in Detik.com, this tool made with Python3, The program is interactive and simply requires you to run it to begin
Once started, you will be asked to input an your keyword. A full scrapt can take as little as 15 seconds depending on your internet connection.

## Installation
The python Git module is required (python3-git on Debian).


## Usage

```
python3 detik.py
```

## Install module

```
- pip install requests
- pip install bs4
- pip install rich
```

## Usage

### Scrap
for scrap all link news 

```js
all_url = [] 																	 # save all url in array for calculate len
	pages = 1 																		 # pages on detik.com
	sloops = input('[x] Input ur Query : ')

	while(True):
		time.sleep(1)
		url = "https://www.detik.com/search/searchall?query={}&siteid=2&sortby=time&page={}" .format(sloops, pages)
		search = requests.get(url).text
		if '0 hasil ditemukan' in search: 											 # if page null, its mean no article in that page, and then break process
			break
		else:
			get_url_soup = BeautifulSoup(search, "html.parser") 					 # like requests.text, this for get content in url
			warning = get_url_soup.find('div', class_="list media_rows list-berita") # find div
			images = warning.find_all('article')	 								 # get article on div class list media_rows list-berita
			for images2 in images: 													 			
				ranz = images2.find_all('a') 										 # url of article is in a href, so this to find <a>
				for zzz in ranz:
					all_url.append(zzz['href'])										 # get href ( links )

			lenz = len(all_url)														 # check length url on array 
			siz = 1
			progress_bar = 1
			print(Panel.fit("Scraping Page {}" .format(pages)))
			print(Panel.fit("Grabbed {} URL" .format(len(all_url))))

			for example in track(all_url, total=lenz):
				if siz == lenz:
					url_request2(example, 'last')
				else:
					url_request2(example, 'nope')
				
				siz+=1
				time.sleep(1)
		all_url.clear()
		pages +=1
```

### Scrap
for scrap all article
```js
grab_title = re.findall('<title>(.*?)</title>', req)
	for title in grab_title:
		title_saved=title
	soup = BeautifulSoup(req, 'html.parser')

	try:
		imeg_grab = BeautifulSoup(req, "html.parser")
		warning = imeg_grab.find('div', class_="detail__media")
		images = warning.find_all('img')
		example = images[0].attrs['src']
		#print('[x] Images : '+example)
		image_saved = example
	except:
		try:
			imeg_grab = BeautifulSoup(req, "html.parser")
			warning = imeg_grab.find('figure')
			images = warning.find('picture', class_="img_con lqd")

			mages2 = warning.find('img')
			example = mages2.attrs['src']
			#print('[!] Images : '+example)
		except:
			pass



	soup.div['class'] = 'detail__body-text itp_bodycontent'

	fac = []
	for sub_heading in soup.find_all('p'):
		art = sub_heading.text.strip()
		#print(sub_heading.text)
		fac.append(sub_heading.text.strip())
```
## License

This project is licensed under the [MIT license](LICENSE).
