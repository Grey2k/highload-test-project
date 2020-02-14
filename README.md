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
- spring web / security / jdbc
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

##### Генерация данных

Для генерации тестовых данных используется утилита javafaker

```
1. Удалить в файле ./backend/src/test/kotlin/dev/lysov/sn/FakerTest.kt аннотацию @Disabled
2. Выполнить команду из корня проекта: ./gradlew test --tests "*FakerTest"
3. В результате будет сгенерирован файл insert-account.txt с 1000000 записей
4. Запустить докер (см. п. выше)
5. Скопировать файл insert-account.txt в запущенный контейнер:
docker cp insert-account.txt docker_db_1:/var/tmp
6. Подключиться к mysql в докере (имя контейнера = docker_db_1)
docker exec -it docker_db_1 mysql -uroot -ppassw0rd sn
7. Выполнить вставку данных из файла:
LOAD DATA INFILE '/var/tmp/insert-account.txt'
    INTO TABLE account
    FIELDS TERMINATED BY ';'
    (username, password, first_name, last_name, age, gender, city, description)
    SET ID = NULL;

В результате:
Query OK, 1000000 rows affected (17.98 sec)
```