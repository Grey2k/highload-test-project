# Прототип социальной сети

https://a902285-sn.herokuapp.com/

#### Задачи
<details>
  <summary>TASK 01</summary>
  
  ```
  Требуется разработать создание и просмотр анект в социальной сети.
  
  Функциональные требования:
  Авторизация по паролю.
  Страница регистрации, где указывается следующая информация:
  Имя
  Фамилия
  Возраст
  Пол
  Интересы
  Город
  Страницы с анкетой.
  
  Нефункциональные требования:
  Любой язык программирования
  В качестве базы данных использовать MySQL
  Не использовать ORM
  Программа должна представлять из себя монолитное приложение.
  Не рекомендуется использовать следующие технологии:
  Репликация
  Шардинг
  Индексы
  Кэширование
  
  
  Верстка не важна. Подойдет самая примитивная.
  
  Разместить приложение на любом хостинге. Например, heroku.
  ```
</details>

<details>
  <summary>TASK 02</summary>
  
  ```
  Нагрузка Яндекса!
  
  Цель: Разработает тестовый скрипт нагрузочного тестирования, проведет тестирование, проанализирует результаты.
  1. По полученным навыкам на вебинаре - разработайте скрипт работы с сайтом яндекса:
  - переход на главную страницу
  - переход в раздел картинок
  - поиск картинки "котики" (или любой другой)
  - переход на найденному url из ответа системы
  2. Проведите нагрузочный тест в несколько потоков в течение не менее 10 минут
  3. Проанализируйте полученный результат и дайте ответ на вопрос - какие выводы можно сделать по результатам? Оформите выводы в виде краткого отчета
  ```
</details>

<details>
  <summary>TASK 03</summary>
  
  ```
  1. Сгенерировать любым способ 1,000,000 анкет. Имена и Фамилии должны быть реальными (чтобы учитывать селективность индекса)
  2. Реализовать функционал поиска анкет по префиксу имени и фамилии (одновременно) в вашей социальной сети (запрос в форме к firstName LIKE ? or secondName LIKE ?). Сортировать вывод по id анкеты. Использовать InnoDB движок.
  3. С помощью wrk провести нагрузочные тесты по этой странице. Поиграть с количеством одновременных запросов. 1/10/100/1000.
  4. Построить графики и сохранить их в отчет
  5. Сделать подходящий индекс.
  6. Повторить пункт 3 и 4.
  7. В качестве результата предоставить отчет в котором должны быть:
     1. Графики latency до индекса
     2. Графики throughput до индекса
     3. Графики latency после индекса
     4. Графики throughput после индекса
     5. Запрос добавления индекса
     6. Explain запросов после индекса
     7. Объяснение почему индекс именно такой
  ```
</details>

#### Стек
- kotlin
- spring reactive web / security / jdbc
- jwt
- react js
- mysql
- liquibase

#### Локальный запуск:

##### Требования к ПО:
- jdk 1.8
- nodejs 12.14.1
- docker / docker-compose

##### Запуск приложения
```
cd ./docker/
docker-compose up -d

cd ../
./gradlew clean build
java -jar ./backend/build/libs/backend-0.0.1-SNAPSHOT.jar
```
Перейти по ссылке: http://localhost:8080/

##### Деплой в heroku

```
$ heroku create a902285-sn
$ heroku addons:create cleardb:ignite
$ heroku run env
> При необходимости, изменить УРЛ к БД в ./Procfile (УРЛ указан явно для возможности задать useUnicode=true&characterEncoding=UTF-8)

> Проверить корректность baseUrl в ./frontend/src/config/config.js
$ heroku login
$ git commit -am "make it better"
$ git push heroku master
```