<!-- TOC -->
  * [`Bridge (Мост)`](#bridge-мост)
    * [`Проблема`](#проблема)
    * [`Решение`](#решение)
    * [`Пример`](#пример)
    * [`Структура`](#структура)
    * [`Применимость`](#применимость)
    * [`Источники`](#источники)
<!-- TOC -->

## `Bridge (Мост)`

Мост — это структурный паттерн проектирования, который разделяет один или несколько классов на две отдельные иерархии — 
абстракцию и реализацию, позволяя изменять их независимо друг от друга.

### `Проблема`

**Описание 1**: У вас есть класс геометрических `Фигур`, который имеет подклассы `Круг` и `Квадрат`. Вы хотите расширить иерархию фигур по цвету, 
то есть иметь `Красные` и `Синие` фигуры. 
Но чтобы всё это объединить, вам придётся создать 4 комбинации подклассов, вроде `СиниеКруги` и `КрасныеКвадраты`.

![Alt text](https://refactoring.guru/images/patterns/diagrams/bridge/problem-ru-2x.png)

Корень проблемы заключается в том, что мы пытаемся расширить классы фигур сразу в двух независимых плоскостях — по виду и по цвету. 
Именно это приводит к разрастанию дерева классов.

**Описание 2**: Требуется отделить абстракцию от реализации так, чтобы и то и другое можно было изменять независимо. 
При использовании наследования реализация жестко привязывается к абстракции, что затрудняет независимую модификацию.

### `Решение`

**Решение 1**: Паттерн Мост предлагает `заменить наследование агрегацией или композицией`. 

Мы можем сделать Цвет отдельным классом с подклассами `Красный` и `Синий`. Класс `Фигур` получит ссылку на объект `Цвета` 
и сможет делегировать ему работу, если потребуется. 
Такая связь и станет `мостом` между `Фигурами` и `Цветом`. 
При добавлении новых классов цветов не потребуется трогать классы фигур и наоборот.

**Решение 2**: Поместить абстракцию и реализацию в отдельные иерархии классов.

### `Пример`

Пример с отчетами. Есть абстрактный `Report`. У него есть наследники `YearlyReport`, `WeeklyReport` ...
Каждый из них нужно напечатать в трех форматах: `doc`, `xml`, `pdf`.

Мы же не будем делать все эти отчеты в разных форматах в виде разных классов: `YealyReportXml`, `YearlyReportDoc` ...
Будет правильным вынести отдельный класс `Format`. С наследниками: `DocFormat`, `XmlFormat`, `PdfFormat`.
И затем в классе `Report` появится ссылка на класс `Format`.

### `Структура`

Пример разделения двух иерархий классов — приборов и пультов управления.

![Alt text](https://refactoring.guru/images/patterns/diagrams/bridge/example-ru-2x.png)

### `Применимость`
 
- Когда вы хотите разделить монолитный класс, который содержит несколько различных реализаций какой-то функциональности
 (например, если класс может работать с разными поставщиками похожего API: cloud-сервисы, социальные сети, базы данных)
- Когда класс нужно расширять в двух независимых плоскостях.
- Когда вы хотите, чтобы реализацию можно было бы изменять во время выполнения программы.

### `Источники`

- [Подробнее о паттерне на refactoring.guru](https://refactoring.guru/ru/design-patterns/bridge)

- [Реализация на Java](https://refactoring.guru/ru/design-patterns/bridge/java/example)

- [Паттерн Bridge](https://bool.dev/blog/detail/strukturnye-patterny-most-csharp)

- [Сергей Немчинский о паттерне Bridge](https://youtu.be/oDM-lKXuQ1g?t=969) (Видео)