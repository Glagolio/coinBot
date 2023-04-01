## Вітаю Вас в TestCoinBot.

## Етапи розгортування бота.

- Знайдіть в телеграмі BotFather і виконуючи його інструкції створіть свого бота, та отримайте token, який нам знадобиться далі.

  <img src='https://github.com/Glagolio/CoinBot/blob/main/assets/bot.png'>

- На зручному для Вас сервісі створіть MySQL базу.
  Створивши виконайте цю команду, щоб створити таблицю.

CREATE TABLE IF NOT EXISTS users
( id INT UNSIGNED AUTO_INCREMENT NOT NULL,  
email VARCHAR(50) NOT NULL,  
password VARCHAR(60) NOT NULL,  
chatId VARCHAR(50) NOT NULL,  
CONSTRAINT users_PK PRIMARY KEY (id) );

- Додаток використовує в якості API сервіс https://www.coinapi.io/
  Тому переходимо за посиланням та реєструємось, потім на вашу пошту отримаєте ключ доступа, який нам знадобиться пізніше.

- Склонуйте цей репозиторій собі локально.
  Для цього оберіть папку, відкрийте термінал та виконайте команду
  git clone https://github.com/Glagolio/CoinBot.git

- Запускати бота ми будемо на сервісі heroku.
  Для цього заходимо на їх сайт і встановлюємо локально heroku згідно інструкції:
  <img src='https://github.com/Glagolio/CoinBot/blob/main/assets/download.png'>

- Відкрийте термінал в папці з нашим проектом та виконайте наступні команди:
  heroku create
  git push heroku main
  В процессі виконання heroku може вимагати авторизації та підтвердження платіжної карти(все виконуйте)

- По закінченню, коли проект буде задеплоін на сервіс heroku необхідно ввести ключи, які будуть давати доступ до бази, бота, тощо.
  Для цього в налаштуванні додатку на heroku треба знайти розділ Config Vars
  <img src='https://github.com/Glagolio/CoinBot/blob/main/assets/keys.png'>

В проекті використовуються такі ключи:

- BOT_KEY=ТОКЕН вашого боту
- DB_HOST=Хост вашої бази данних
- DB_USER=Користувач у якого є доступ до бази данних
- DB_PORT=Порт на якому розгорнута база данних
- DB_PASSWORD=Пароль від бази данних
- DB_DATABASE=Ім’я бази данних
- API_KEY=Ключ доступа до API
- PORT=Порт на якому буде розгорнут додаток

Після виконання всіх цих дій Ви будете мати працюючий бот.

## Про роботу бота:

- Для початку роботи треба ввести команду /start
- Далі, якщо користувач вже зареєстрований в базі, то він одразу отримає доступ до функціонала бота, якщо ні, то буде запропонована реєстрація нового користувача.
- При реєстрації присутня проста Валідація, тому email має бути справжнім та закінчуваться на домени .net, .com або .ua, пароль також має бути надійним. (При записі в базу данних пароль хешується, тому не перейматесь, ніхто не з тих хто має доступ до бази не дізнається Ваш пароль.)
- Для авторизованих юзерів є 2 функціональних кнопки, які виведуть повідомлення з актуальною ціною Біткоіна, або Еферума.
- Для массової розсилки у нашого сервера створен end-point:
  https://host:port/mailing (можна дати будь який запит GET, POST тощо) і всім користувачам, які є базі данних буде виконана розсилка актуальної ціни біткоїна. В майбутньому цей end-point можна використати для переодичного “спама” користувачів, або більш персоналізованих повідомлень.
