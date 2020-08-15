# Умный сервис прогноза погоды "WhatGonnaWear-bot"
Проект реализован в форме чат-бота Телеграм.
_________________________________________
Программа написана Python с использованием:
- requests (направление http-запроса на сервер прогноза погоды),
- python-dotenv (загрузка и считывание переменных окружения из файла .env)
- pyTelegramBotAPI (работа с Телеграм-ботом),
- PySocks (направлениу трафика через SOCKS и прокси-серверы HTTP)

## Как запустить программу:

1) Клонируйте репозитроий с программой:
```
git clone https://github.com/leks20/WhatGonnaWear_bot.git
```
2) Установите виртуальное окружение, активируйте его и установите необхоимые зависимости:
```
python3 -m venv venv

. venv/bin/activate

pip install -r requirements.txt
```
3) Создайте в директории файл .env и поместите туда необходимые токены в формате telegram_token = 'ххххххххх', weather_token = 'ххххххххххх'
(API-токен можно получить на сайте https://openweathermap.org/forecast5)
4) Откройте файл main.py и запустите код
5) В мессенджере Телеграм найдите чат-бота WhatGonnaWear_bot, запустите его командой /start и дальше следуйте инструкции (либо создайте нового чат-бота в Телеграм)

## Как работает программа:
Полученные с API данные о погоде направляются пользователю в текстовом формате в ответ на запрос в чате.
В ответе содержится информация о погоде в выбранном городе в трех временных точках: ближайший час, через 6 часов и через 12 часов.
Поддерживается русский язык и метрическая система исчисления.
Погодные характеристики:
- общее описание погоды (ясно, пасмурно, облачно с прояснениями...),
- температура воздуха в гр. Цельсия,
- ощущение температуры в гр. Цельсия,
- влажность, %,
- скорость ветра, м/с.
Ответ также содержит небольшую рекомендацию о выборе одежды в зависимости от погодных условий (каждые 5 градусов в промежутке от -25 до +25)

### Пример ответа чат-бота:
Пальто и стильный шарф сегодня как никогда кстати!

Погода в г. Санкт-Петербург в 18:00
Небольшой дождь. Температура воздуха: 5°, по ощущениям: -2°. Влажность 85 %, скорость ветра 7 м/с.

Погода в г.Санкт-Петербург в 00:00
Небольшой дождь. Температура воздуха: 6°, по ощущениям: 0°. Влажность 85 %, скорость ветра 7 м/с.

Погода в г.Санкт-Петербург в 06:00
Пасмурно. Температура воздуха: 8°, по ощущениям: 2°. Влажность 74 %, скорость ветра 7 м/с.


### Процесс работы программы:
- Пользователь запускает чат-бота Телеграм "WhatGonnaWear-bot" кнопкой /start.
- В ответ приходит сообщение "Привет <имя пользователя в Телеграм>! Напишите название города или выберите из списка".
- В предложенном списке в виде кнопок - 10 городов России с наибольшим количеством жителей. Пользователь может написать любой другой город мира.
- Полученное наименование города передается в качетстве аргумента в функцию, которая осуществляет http-запрос на открытый API погодного сервера, который в свою очередь предоставляет информацию о погоде в городе в формате JSON (при этом функция обрабатывает возможные исключения и в случае ошибки соединения формирует соответствущий ответ пользователю).
- Из полученной информации отбираются только данные необходимые для ответа пользователю: общее описание погоды (ясно, пасмурно, облачно с прояснениями...), температура воздуха, ощущение температуры в гр. Цельсия, влажность, скорость ветра, м/с в трёх временных точках.
- Далее исходя из полученных данных о погоде формируется краткая рекомендация о выборе одежды.
- Пользователю приходит ответ от чат-бота с рекомендацией и прогнозом погоды в выбранном городе.
- В случае возникновения ошибки соединения или ввода неверного наименования города пользователю приходит соответсвующее сообщение.



