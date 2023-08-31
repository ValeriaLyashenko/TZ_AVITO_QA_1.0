# TZ_AVITO_QA_1.0
## Автоматизация позитивного тест-кейса
##И нструкция
### Описание
Данный код использует библиотеку Selenium для автоматизации действий в браузере Chrome. Он осуществляет переход на определенную страницу объявления на сайте Avito и выполнение некоторых действий.

Установка
Убедитесь, что у вас установлен Python и pip.
Установите библиотеку Selenium, выполнив следующую команду в командной строке:
```
pip install selenium
```
### Использование
Загрузите Chrome WebDriver и укажите путь к исполняемому файлу в переменной webdriver_service.
При необходимости, внесите изменения в опции браузера в переменной chrome_options.
Замените ссылку в методе get() на страницу с нужным объявлением на сайте Avito.
Запустите скрипт, чтобы выполнить тест на Desktop-версии.


### Пример
Примечание: Перед запуском убедитесь, что у вас установлен Chrome WebDriver и указан корректный путь к нему в переменной webdriver_service.
```
python
Copy code
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.chrome.options import Options

# Установка пути к исполняемому файлу Chrome WebDriver
webdriver_service = Service(r'C:\Users\Андрей\VS_Code_projects\java_test_code\chromedriver\chromedriver.exe')

# Установка опций браузера
chrome_options = Options()
chrome_options.add_argument("--start-maximized")  # Развернуть окно браузера на максимальный размер

# Инициализация экземпляра браузера Chrome WebDriver
driver = webdriver.Chrome(service=webdriver_service, options=chrome_options)

# Переход на страницу нужного объявления
driver.get("https://www.avito.ru/ekaterinburg/mototsikly_i_mototehnika/mototsikl_avantis_enduro_250_dohc_pro_efi_exclusive_3681745005")

# Проверка, что тест выполняется на Desktop-версии
if driver.execute_script("return window.innerWidth") > 1024:  # Пример проверки разрешения экрана
    # Ищем кнопку "Добавить в избранное" и кликаем на нее
    add_to_favorites_button = driver.find_element(By.XPATH, "//button[@id='add-to-favorites']")
    add_to_favorites_button.click()

    # Проверка, что объявление добавлено в избранное
    success_message = driver.find_element(By.XPATH, "//div[@class='success-message']")
    if success_message.is_displayed() and success_message.text == "Объявление успешно добавлено в избранное":
        print("Объявление успешно добавлено в избранное")
    else:
        print("Ошибка при добавлении объявления в избранное")
else:
    print("Тест выполняется только на Desktop-версии")

# Закрытие браузера
driver.quit()
```

