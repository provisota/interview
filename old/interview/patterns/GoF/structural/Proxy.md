## `Proxy (Прокси / Заместитель)`

Заместитель — это структурный паттерн проектирования, который позволяет подставлять вместо реальных объектов 
специальные объекты-заменители. Эти объекты перехватывают вызовы к оригинальному объекту, позволяя сделать что-то до 
или после передачи вызова оригиналу.

### `Проблема`

Рассмотрим такой пример: у вас есть внешний ресурсоёмкий объект, который нужен не все время, а изредка.
Мы могли бы создавать этот объект не в самом начале программы, а только тогда, когда он кому-то реально понадобится. 
Каждый клиент объекта получил бы некий код отложенной инициализации. 
Но, вероятно, это привело бы к множественному дублированию кода.

В идеале, этот код хотелось бы поместить прямо в служебный класс, но это не всегда возможно.
Например, код класса может находиться в закрытой сторонней библиотеке

### `Решение`

Паттерн Заместитель предлагает создать новый класс-дублёр, имеющий тот же интерфейс, что и оригинальный служебный объект. 
При получении запроса от клиента объект-заместитель сам бы создавал экземпляр служебного объекта 
и переадресовывал бы ему всю реальную работу.

Благодаря одинаковому интерфейсу, объект-заместитель можно передать в любой код, ожидающий сервисный объект.

### `Структура`

В этом примере Заместитель помогает добавить в программу механизм ленивой инициализации и кеширования 
результатов работы библиотеки интеграции с YouTube.

![Alt text](https://refactoring.guru/images/patterns/diagrams/proxy/example-2x.png)

Оригинальный объект начинал загрузку по сети, даже если пользователь запрашивал одно и то же видео. 
Заместитель же загружает видео только один раз, используя для этого служебный объект, но в остальных случаях 
возвращает закешированный файл.

### `Применимость`

- Ленивая инициализация (виртуальный прокси). Когда у вас есть тяжёлый объект, грузящий данные из файловой системы или базы данных.
- Защита доступа (защищающий прокси). Когда в программе есть разные типы пользователей, 
и вам хочется защищать объект от неавторизованного доступа. 
Например, если ваши объекты — это важная часть операционной системы, 
а пользователи — сторонние программы (хорошие или вредоносные).
- Локальный запуск сервиса (удалённый прокси). Когда настоящий сервисный объект находится на удалённом сервере.
- Логирование запросов (логирующий прокси). Когда требуется хранить историю обращений к сервисному объекту.
- Кеширование объектов («умная» ссылка). Когда нужно кешировать результаты запросов клиентов и управлять их жизненным циклом.

### `Источники`

- [Подробнее о паттерне на refactoring.guru](https://refactoring.guru/ru/design-patterns/proxy)

- [Реализация на Java](https://refactoring.guru/ru/design-patterns/proxy/java/example)