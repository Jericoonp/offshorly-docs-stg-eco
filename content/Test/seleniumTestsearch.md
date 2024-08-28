# Search Behavior of CodeBase Website

This is just a sample for testing the behavior of the site when no text is entered

## Import

Import the necessary

```python

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.wait import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.support.ui import Select
import time
import difflib


```

### Going to the site

```python?(test with special characters)
options = webdriver.ChromeOptions()
chrome_options = Options()
chrome_options.add_experimental_option("detach",True)
driver = webdriver.Chrome(options=chrome_options)
driver.maximize_window()
driver.get("https://kb-frontend-git-staging-clarence-coronels-projects-f9df158c.vercel.app/?page=1")
initial_content = driver.page_source

print("To verify that default search behavior is correct")

```

## Code

```python001
enter = driver.find_element(By.XPATH, "/html[1]/body[1]/div[1]/main[1]/div[1]/form[1]/div[1]/div[2]/button[1]/*[name()='svg'][1]")
enter.click()

updated_content = driver.page_source

if initial_content != updated_content:
    diff = difflib.unified_diff(initial_content.splitlines(), updated_content.splitlines())
    for line in diff:
        print(line)
    print("TC-1808: failed")
    driver.quit()
else:
    print("TC-1808: success")
    driver.quit()
```
