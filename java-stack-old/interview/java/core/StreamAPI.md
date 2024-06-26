<!-- TOC -->
* [Stream API](#stream-api)
  * [Как работает стрим](#как-работает-стрим)
  * [Последовательные и параллельные стримы](#последовательные-и-параллельные-стримы)
  * [Операторы](#операторы)
  * [Основные Промежуточные операции:](#основные-промежуточные-операции)
  * [Основные Терминальные операции:](#основные-терминальные-операции)
  * [Некоторые промежуточные операторы:](#некоторые-промежуточные-операторы)
  * [Некоторые терминальные операторы](#некоторые-терминальные-операторы)
  * [Полезные ссылки](#полезные-ссылки)
<!-- TOC -->

# Stream API

**Stream API** — это новый способ работать со структурами данных в функциональном стиле. Мы указываем, какие операции хотим провести, при этом не заботясь о
деталях реализации. Данные могут быть получены из источников, коими являются коллекции или методы, поставляющие данные. Например, список файлов, массив строк,
метод `range()` для числовых промежутков и т.д. То есть, стрим использует существующие коллекции для получения новых элементов, это ни в коем случае 
не новая структура данных.

## Как работает стрим

У стримов есть некоторые особенности. 
1. Обработка не начнётся до тех пор, пока не будет вызван терминальный оператор. 
`list.stream().filter(x -> x > 100);` данный прмиер не возьмёт ни единого элемента из списка. 
2. Стрим после обработки нельзя переиспользовать. Исходя из первой особенности, делаем вывод, что обработка происходит от терминального оператора к источнику.

## Последовательные и параллельные стримы

Стримы бывают последовательными (sequential) и параллельными (parallel). 

**Последовательные** выполняются только в текущем потоке, а вот **параллельные** используют общий пул `ForkJoinPool.commonPool()`. 
При этом элементы разбиваются (если это возможно) на несколько групп и обрабатываются в каждом потоке отдельно. Затем на нужном этапе группы объединяются 
в одну для предоставления конечного результата. От нас лишь требуется вызвать нужный метод и проследить, чтобы функции в операторах не зависели от 
каких-либо внешних факторов, иначе есть риск получить неверный результат или ошибку.

Вот так делать нельзя:
```java
final List<Integer> ints = new ArrayList<>();
IntStream
  .range(0, 1000000)
  .parallel()
  .forEach(i -> ints.add(i));
System.out.println(ints.size());
```

Это код Шрёдингера. Он может нормально выполниться и показать `1000000`, может выполниться и показать `869877`, а может и упасть с ошибкой 
`ArrayIndexOutOfBoundsException`. Поэтому разработчики настоятельно просят воздержаться от побочных эффектов в лямбдах, то тут, то там говоря 
в документации о невмешательстве (non-interference).

## Операторы

![Screenshot](../../../resources/StreamAPI.png)

Операторы можно разделить на две группы:
**Промежуточные (intermediate)** — обрабатывают поступающие элементы и возвращают стрим. Промежуточных операторов в цепочке обработки элементов может
быть много.
**Терминальные (terminal)** — обрабатывают элементы и завершают работу стрима, так что терминальный оператор в цепочке может быть только один.

## Основные Промежуточные операции:

1. `filter(Predicate<T> predicate)`: Фильтрует элементы потока согласно условию, заданному предикатом.
2. `map(Function<T, R> mapper)`: Преобразует каждый элемент потока с помощью переданной функции.
3. `flatMap(Function<T, Stream<R>> mapper)`: Преобразует каждый элемент в поток, а затем объединяет результаты в один поток.
4. `distinct()`: Удаляет дубликаты из потока.
5. `sorted()`: Сортирует элементы потока. Можно передать компаратор для определения порядка сортировки.
6. `limit(long maxSize)`: Ограничивает количество элементов в потоке заданным значением.
7. `skip(long n)`: Пропускает указанное количество элементов в потоке.
8. `peek(Consumer<T> action)`: Выполняет заданное действие для каждого элемента потока, не изменяя его.

## Основные Терминальные операции:

1. `forEach(Consumer<T> action)`: Применяет заданное действие к каждому элементу потока.
2. `count()`: Возвращает количество элементов в потоке.
3. `collect(Collector<T, A, R> collector)`: Собирает элементы потока в коллекцию или другую структуру данных.
4. `reduce(T identity, BinaryOperator<T> accumulator)`: Передает каждый элемент потока в аккумулятор с заданным начальным значением и возвращает результирующее значение.
5. `findFirst()`: Возвращает первый элемент потока (или `Optional.empty()`, если поток пуст).
6. `findAny()`: Возвращает любой элемент потока (или `Optional.empty()`, если поток пуст).
7. `allMatch(Predicate<T> predicate)`: Проверяет, соответствуют ли все элементы потока заданному условию.
8. `anyMatch(Predicate<T> predicate)`: Проверяет, соответствует ли хотя бы один элемент потока заданному условию.
9. `noneMatch(Predicate<T> predicate)`: Проверяет, что ни один из элементов потока не соответствует заданному условию.

Эти операции можно комбинировать в различных комбинациях для выполнения сложных операций обработки данных.

## Некоторые промежуточные операторы:

- `generate(Supplier s)` - Возвращает стрим с бесконечной последовательностью элементов, генерируемых функцией `Supplier s`.
- `iterate(T seed, UnaryOperator f)` - Возвращает бесконечный стрим с элементами, которые образуются в результате последовательного применения функции `f` 
к итерируемому значению. Первым элементом будет `seed`, затем `f(seed)`, затем `f(f(seed))` и так далее.
- `concat(Stream a, Stream b)` - объединяет два стрима
- `IntStream.range(0, 10).forEach(System.out::println);` - [0, 10) = [0, 9]
- `IntStream.rangeClosed(0, 5).forEach(System.out::println);` - [0, 5]
- `flatMap(Function<T, Stream<R>> mapper)`
Один из самых интересных операторов. Работает как `map`, но с одним отличием — можно преобразовать один элемент в ноль, один или множество других. 
Для возвращения нескольких элементов, можно любыми способами создать стрим с этими элементами.

```java
class Human {
    private final String name;
    private final List<String> pets;
 
    //constructors, getters
}

// До Java 8
public static void main(String[] args) {
    List<Human> humans = asList(
            new Human("Sam", asList("Buddy", "Lucy")),
            new Human("Bob", asList("Frankie", "Rosie")),
            new Human("Marta", asList("Simba", "Tilly")));

    List<String> petNames = new ArrayList<>();
    for (Human human : humans) {
        petNames.addAll(human.getPets());
    }

    System.out.println(petNames); // output [Buddy, Lucy, Frankie, Rosie, Simba, Tilly]
}

// Java 8 
public static void main(String[] args) {
    List<Human> humans = asList(
            new Human("Sam", asList("Buddy", "Lucy")),
            new Human("Bob", asList("Frankie", "Rosie")),
            new Human("Marta", asList("Simba", "Tilly")));
 
    List<String> petNames = humans.stream()
            .map(human -> human.getPets()) //преобразовываем Stream<Human> в Stream<List<Pet>>
            .flatMap(pets -> pets.stream())//"разворачиваем" Stream<List<Pet>> в Stream<Pet>
            .collect(Collectors.toList());
 
    System.out.println(petNames); // output [Buddy, Lucy, Frankie, Rosie, Simba, Tilly]
}
```

- `skip(int n)` - пропускает n элементов стрима
- `sorted() & sorted(Comparator comparator)` - Сортирует элементы стрима. Причём работает этот оператор очень хитро: если стрим уже помечен как 
отсортированный, то сортировка проводиться не будет, иначе соберёт все элементы, отсортирует их и вернет новый стрим, помеченный как отсортированный.
- `distinct()` - Убирает повторяющиеся элементы и возвращаем стрим с уникальными элементами
- `boxed()` - Преобразует примитивный стрим в объектный.

## Некоторые терминальные операторы

- `long count()` - кол-во элем-ов
- `Stream.of(1, 2, 3).map(String::valueOf).collect(Collectors.joining("-", "<", ">"));` - результат: "<1-2-3>"
- `R collect(Supplier supplier, BiConsumer accumulator, BiConsumer combiner)`

То же, что и `collect(collector)`, только параметры разбиты для удобства. Если нужно быстро сделать какую-то операцию, нет нужды реализовывать интерфейс 
`Collector`, достаточно передать три лямбда-выражения. `supplier` должен поставлять новые объекты (контейнеры), например `new ArrayList()`, `accumulator` 
добавляет элемент в контейнер, `combiner` необходим для параллельных стримов и объединяет части стрима воедино.

`Stream.of("a", "b", "c", "d").collect(ArrayList::new, ArrayList::add, ArrayList::addAll);` - результат: ["a", "b", "c", "d"]

- `T reduce(T identity, BinaryOperator accumulator)`
- `U reduce(T identity, BiFunction accumulator, BinaryOperator combiner)`

Ещё один полезный оператор. Позволяет преобразовать все элементы стрима в один объект. Например, посчитать сумму всех элементов, либо найти минимальный
элемент. Сперва берётся объект `identity` и первый элемент стрима, применяется функция `accumulator` и `identity` становится её результатом. 
Затем всё продолжается для остальных элементов.

`Stream.of(1, 2, 3, 4, 5).reduce(10, (acc, x) -> acc + x);` - результат: 25

- `IntSummaryStatistics summaryStatistics()` - полезный метод примитивных стримов. Позволяет собрать статистику о числовой последовательности стрима, а именно:
количество элементов, их сумму, среднее арифметическое, минимальный и максимальный элемент.

## Полезные ссылки

[Полное руководство по Java 8 Stream API в картинках и примерах - annimon](https://annimon.com/article/2778)
