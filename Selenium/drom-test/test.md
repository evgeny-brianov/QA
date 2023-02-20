**Selenium test example:**
```python
import time
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.common.exceptions import InvalidElementStateException
s=Service('F:/Test/chromedriver.exe')
driver = webdriver.Chrome(service=s)
#open and login
driver.get("https://auto.drom.ru/")
driver.maximize_window()
time.sleep(0.5)
#select brand
driver.find_element(By.XPATH, "//div/div[1]/div[1]/div/div[1]/input").click()
time.sleep(0.5)
driver.find_element(By.XPATH, "//div/div[1]/div[1]/div/div[1]/input").send_keys("Toyota")
time.sleep(0.5)
driver.find_element(By.XPATH, "//div/div[1]/div[1]/div/div[1]/input").send_keys(Keys.ENTER)
time.sleep(0.5)
#select model
driver.find_element(By.XPATH, "//div/div[1]/div[2]/div/div[1]/input").click()
time.sleep(0.5)
driver.find_element(By.XPATH, "//div/div[1]/div[2]/div/div[1]/input").send_keys("Harrier")
time.sleep(0.5)
driver.find_element(By.XPATH, "//div/div[1]/div[2]/div/div[1]/input").send_keys(Keys.ENTER)
time.sleep(0.5)
#select fuel type
driver.find_element(By.XPATH, "//div/div[2]/div[3]/div[2]/div[1]/button").click()
time.sleep(0.5)
driver.find_element(By.XPATH, "//div/div[2]/div[3]/div[2]/div[1]/button").send_keys(Keys.ARROW_DOWN)
driver.find_element(By.XPATH, "//div/div[2]/div[3]/div[2]/div[1]/button").send_keys(Keys.ARROW_DOWN)
driver.find_element(By.XPATH, "//div/div[2]/div[3]/div[2]/div[1]/button").send_keys(Keys.ARROW_DOWN)
driver.find_element(By.XPATH, "//div/div[2]/div[3]/div[2]/div[1]/button").send_keys(Keys.ARROW_DOWN)
driver.find_element(By.XPATH, "//div/div[2]/div[3]/div[2]/div[1]/button").send_keys(Keys.ARROW_DOWN)
driver.find_element(By.XPATH, "//div/div[2]/div[3]/div[2]/div[1]/button").send_keys(Keys.ENTER)
time.sleep(0.5)
#not sale chebox
driver.find_element(By.XPATH, "//div/div[3]/div[3]/div[1]/div/label").click()
time.sleep(0.5)
driver.find_element(By.XPATH, "//div/div[4]/div[2]/button/span").click()
driver.execute_script('window.scrollTo(0,400);')
time.sleep(0.5)
#mileage form
driver.find_element(By.XPATH, "//div/div[4]/div[3]/div[3]/div[1]/div/div/div[1]/div/div/div[1]/div/input").click()
driver.find_element(By.XPATH, "//div/div[4]/div[3]/div[3]/div[1]/div/div/div[1]/div/div/div[1]/div/input").send_keys("1")
time.sleep(0.5)
#year choose
driver.find_element(By.XPATH, "//div/div[2]/div[2]/div/div[1]/div[1]/button").click()
driver.find_element(By.XPATH, "//div/div[2]/div[2]/div/div[1]/div[2]/div[text()='2007']").click()
time.sleep(0.5)
driver.find_element(By.XPATH, "//div/div[5]/div[3]/button").click()
time.sleep(0.5)

def check_page():
    #check element year
    titles = driver.find_elements(By.XPATH, "//span[@data-ftid='bull_title']")
    for title in titles:
        year = int(title.text[-4:])
        if year < 2007:
            raise InvalidElementStateException("Error year")
    #check milege
    descs = driver.find_elements(By.XPATH, "//div[@data-ftid='component_inline-bull-description']")
    for descr in descs:
        end_descr = descr.text[-7:]
        if end_descr != 'тыс. км':
            raise InvalidElementStateException("Error milenage")
    #check line-through
    titles_parents = driver.find_elements(By.XPATH, "//span[@data-ftid='bull_title']/..")
    for title_parent in titles_parents:
        text_style = title_parent.value_of_css_property("text-decoration")
        if 'line-through' in text_style :
            raise InvalidElementStateException("Car is sold")
```
