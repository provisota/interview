<!-- TOC -->
* [JDBC](#jdbc)
  * [Строение JDBC](#строение-jdbc)
  * [Элементы JDBC](#элементы-jdbc)
  * [Connection](#connection)
  * [Statements](#statements)
  * [ResultSet](#resultset)
  * [Полезные ссылки](#полезные-ссылки)
<!-- TOC -->

# JDBC

`Java Database Connectivity` – это стандартный `API` для независимого соединения языка программирования `Java` с различными базами данных (далее – `БД`).

`JDBC` решает следующие задачи:
- Создание соединения с БД.
- Создание `SQL` выражений.
- Выполнение `SQL` – запросов.
- Просмотр и модификация полученных записей.

Если говорить в целом, то `JDBC` – это библиотека, которая обеспечивает целый набор интерфейсов для доступа к различным БД.

Для доступа к каждой конкретной БД необходим специальный `JDBC` – драйвер, который является адаптером `Java`–приложения к БД.

## Строение JDBC

`JDBC` поддерживает как 2-звенную, так и 3-звенную модель работы с БД, но в общем виде, `JDBC` состоит из двух слоёв.

- `JDBC API` - Обеспечивает соединение “приложение – `JDBC Manager`”.
- `JDBC Driver API` - Обеспечивает соединение “`JDBC Manager` – драйвер”.

`JDBC API` использует менеджер драйверов и специальные драйверы БД для обеспечения подключения к различным базам данных.

`JBDC Manager` проверяет соответствие драйвера и конкретной БД. Он поддерживает возможность использования нескольких драйверов одновременно для одновременной 
работы с несколькими видами БД.

Схематично, `JDBC` можно представить в таком виде:

![Screenshot](../../resources/JDBC.png)

## Элементы JDBC

`JDBC API` состоит из следующих элементов:

- Менеджер драйверов (`Driver Manager`) - Этот элемент управляет списком драйверов БД. Каждой запрос на соединение требует соответствующего драйвера. Первое 
совпадение даёт нам соединение.
- Драйвер (`Driver`) - Этот элемент отвечает за связь с БД. Работать с ним нам приходится крайне редко. Вместо этого мы чаще используем объекты 
`DriverManager`, которые управляют объектами этого типа.
- Соединение (`Connection`) - Этот интерфейс обеспечивает нас методами для работы с БД. Все взаимодействия с БД происходят исключительно через `Connection`.
- Выражение (`Statement`) - Для подтверждения `SQL`-запросов мы используем объекты, созданные с использованием этого интерфейса.
- Результат (`ResultSet`) - Экземпляры этого элемента содержат данные, которые были получены в результате выполнения `SQL` – запроса. Он работает как итератор 
и “пробегает” по полученным данным.
- Исключения (`SQL Exception`) - Этот класс обрабатывает все ошибки, которые могут возникнуть при работе с БД.

## Connection

Итак, у нас есть `JDBC` драйвер, есть `JDBC API`. Как мы помним, `JDBC` расшифровывается как `Java DataBase Connectivity`. Поэтому, всё начинается с 
`Connectivity` - возможности устанавливать подключение. А подключение — это `Connection`.

Обратимся снова к тексту спецификации `JDBC` и посмотрим на оглавление. Существует два способа подключения к БД:
- Через `DriverManager`
- Через `DataSource`

Разберёмся с `DriverManager`'ом. Как сказано, `DriverManager` позволяет подключиться к базе данных по указанному `URL`, а так же загружает `JDBC Driver`'ы, 
которыу он нашёл в `CLASSPATH` (а раньше, до `JDBC 4.0` загружать класс драйвера надо было самостоятельно).

Получения `Connection`:

```Java
Connection con = DriverManager.getConnection(url, user, passwd);
```

## Statements

Существует несколько типов или видов `statement`'ов:
- `Statement`: `SQL` выражение, которое не содержит параметров
- `PreparedStatement`: Подготовленное `SQL` выражение, содержащее входные параметры
- `CallableStatement`: `SQL` выражение с возможностью получить возвращаемое значение из хранимых процедур (`SQL Stored Procedures`).

Итак, имея подключение, мы можем в рамках этого подключения выполнить какой-нибудь запрос. Поэтому, логично, что экземпляр `SQL` выражения изначально мы 
получаем из `Connection`.

```java
private int executeUpdate(String query) throws SQLException {
	Statement statement = connection.createStatement();
  // Для Insert, Update, Delete
	int result = statement.executeUpdate(query);
	return result;
}
```

Добавим метод создания тестовой таблицы с использованием прошлого метода:

```java
private void createCustomerTable() throws SQLException {
	String customerTableQuery = "CREATE TABLE customers (id INTEGER PRIMARY KEY, name TEXT, age INTEGER)";
	String customerEntryQuery = "INSERT INTO customers VALUES (73, 'Brian', 33)";
	executeUpdate(customerTableQuery);
	executeUpdate(customerEntryQuery);
}
```

## ResultSet

`ResultSet` предоставляет методы для получения и манипуляции результатами выполненных запросов.

То есть если метод `execute` вернул нам `true`, значит мы можем получить и `ResultSet`. 

Давайте вынесем вызов метода `createCustomerTable()` в метод `init`, который отмечен как `@Before`. Теперь доработаем наш тест `shouldSelectData`:

```java
@Test
public void shouldSelectData() throws SQLException {
	String query = "SELECT * FROM customers WHERE name = ?";
	PreparedStatement statement = connection.prepareStatement(query);
	statement.setString(1, "Brian");
	boolean hasResult = statement.execute();
	assertTrue(hasResult);
	
// Обработаем результат

	ResultSet resultSet = statement.getResultSet();
	resultSet.next();
	int age = resultSet.getInt("age");
	assertEquals(33, age);
}
```

Тут стоит отметить, что `next` — это метод, который двигает так называемый "курсор". Курсор в `ResultSet` указывает на некоторую строку. Таким образом, чтобы 
считать строку, на неё нужно этот самый курсор установить. Когда курсор перемещается, то метод перемещения курсора возвращает `true`, если курсор валидный 
(правильный, корректный), то есть указывает на данные. Если возвращает `false`, значит данных нет, то есть курсор не указывает на данные. Если попытаться 
получить данные с невалидным курсором, то мы получим ошибку: `No data is available`.

Ещё интересно, что через ResultSet можно обновлять или даже вставлять строки:

```java
@Test
public void shouldInsertInResultSet() throws SQLException {
	Statement statement = connection.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);
	ResultSet resultSet = statement.executeQuery("SELECT * FROM customers");
	resultSet.moveToInsertRow();
	resultSet.updateLong("id", 3L);
	resultSet.updateString("name", "John");
	resultSet.updateInt("age", 18);
	resultSet.insertRow();
	resultSet.moveToCurrentRow();
}
```

## Полезные ссылки

[Руководство по JDBC. Введение. - proselyte](https://proselyte.net/tutorials/jdbc/introduction/)

[JDBC или с чего всё начинается - javarush](https://javarush.ru/groups/posts/2172-jdbc-ili-s-chego-vsje-nachinaetsja)
