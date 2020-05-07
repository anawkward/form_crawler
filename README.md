# crawler
easily scrape specific table or document. minimalize your effort to analyze HTML to get element addresses.

```python
## example ##
import selenium.webdriver
import crawler
from bs4 import BeautifulSoup

option = selenium.webdriver.ChromeOptions()
driver = selenium.webdriver.Chrome(executable_path='C:/chromedriver.exe',options=option)  # if you don't have, get one on the internet
url = r"some website address you want to address XD"
driver.get(url)
##... manually navigate to the place you want to scrape ... ##
# keys are to find "table where?" and "how many columns?" by analyzing distance between two keys with one row difference.
key1 = 'book_name_in_a_first_row'
key2 = 'book_name_in_a_second_row'
# or key2 = 'another_column_in_a_first_row_if_it_is_one_liner'

page_source = driver.page_source
soup = BeautifulSoup(page_source, 'html.parser')
common_parent_path, length_between_keys = crawler.crawl_first(soup, key1, key2)

xlpath = './myscraping.xlsx'
sheet_num = 0
page_source = driver.page_source
soup = BeautifulSoup(page_source, 'html.parser')
ncol = length_between_keys

# check dataList, if it's good.
dataList = crawler.crawl_to_list(soup, common_parent_path)[0:]
# if you have an empty excel file, save texts there.
# if excel file isn't empty, data is added along rows
crawler.list_to_excel(xlpath, sheet_num, dataList, ncol)
```
