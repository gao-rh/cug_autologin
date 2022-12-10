## 安装selenium库

python 版本3.10（python3应该都兼容）

```shell
conda install selenium
```

或者

```powershell
pip install selenium
```

## 下载驱动

https://registry.npmmirror.com/binary.html?path=chromedriver/

要和chrome版本对应


设置 >> 关于chrome 里面查看版本![1670657454530](https://user-images.githubusercontent.com/66621797/206839317-b66f724d-fecf-4396-99a0-ae1541f0a9d0.png)

## 运行代码

更改驱动位置和账号密码

```python
from selenium import webdriver
from time import sleep

iss = 0
acc = '账号'
key = '密码'
is_open = 0
driver = webdriver.Chrome(executable_path=r'驱动位置')
sleep(2)
driver.get("http://192.168.167.14")
while not is_open:
    try:
        driver.find_element_by_id('notice-content')
        is_open = 1
        print('web opened')
    except:
        driver.refresh()
        sleep(5)
        print('web open failed, trying')
        iss += 1
        if iss > 10:
            print('failed')
            break

try:
    driver.find_element_by_xpath('//button[@id="logout"]')
    print('loged in')
except:
    account_input = driver.find_element_by_xpath('//input[@name="username"]')
    key_input = driver.find_element_by_xpath('//input[@name="password"]')
    account_input.send_keys(acc)
    key_input.send_keys(key)
    driver.find_element_by_xpath('//button[@id="login"]').click()
```
