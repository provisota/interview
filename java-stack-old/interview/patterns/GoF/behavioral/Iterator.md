<!-- TOC -->
  * [`Iterator (Итератор)`](#iterator-итератор)
    * [`Проблема`](#проблема)
    * [`Решение`](#решение)
    * [`Структура`](#структура)
    * [`Применимость`](#применимость)
    * [`Источники`](#источники)
<!-- TOC -->

## `Iterator (Итератор)`

Итератор — это поведенческий паттерн проектирования, который даёт возможность последовательно обходить элементы 
составных объектов, не раскрывая их внутреннего представления.

### `Проблема`

Большинство коллекций выглядят как обычный список элементов. Но есть и экзотические коллекции, построенные на основе 
деревьев, графов и других сложных структур данных.

Но каким способом следует перемещаться по сложной структуре данных? Например, сегодня может быть достаточным обход 
дерева в глубину, но завтра потребуется возможность перемещаться по дереву в ширину. А на следующей неделе и 
того хуже — понадобится обход коллекции в случайном порядке.

### `Решение`

Идея паттерна Итератор состоит в том, чтобы вынести поведение обхода коллекции из самой коллекции в отдельный класс.

![Alt text](https://refactoring.guru/images/patterns/diagrams/iterator/solution1-2x.png)

Объект-итератор будет отслеживать состояние обхода, текущую позицию в коллекции и сколько элементов ещё осталось обойти. 
Одну и ту же коллекцию смогут одновременно обходить различные итераторы, а сама коллекция не будет даже знать об этом.

### `Структура`

![Alt text](https://refactoring.guru/images/patterns/diagrams/iterator/example-2x.png)

### `Применимость`
 
- Когда у вас есть сложная структура данных, и вы хотите скрыть от клиента детали её реализации 
(из-за сложности или вопросов безопасности).
- Когда вам нужно иметь несколько вариантов обхода одной и той же структуры данных.
- Когда вам хочется иметь единый интерфейс обхода различных структур данных.

### `Источники`

- [Подробнее о паттерне на refactoring.guru](https://refactoring.guru/ru/design-patterns/iterator)

- [Реализация на Java](https://refactoring.guru/ru/design-patterns/iterator/java/example)