# Functional Interfaces

**Функциональный интерфейс** в Java – это интерфейс, который содержит **только 1 абстрактный метод**. Основное назначение – использование в лямбда выражениях 
и **method reference**.

Наличие 1 абстрактного метода - это единственное условие, таким образом функциональный интерфейс может содержать также `default` и `static` методы.

К функциональному интерфейсу можно добавить аннотацию `@FunctionalInterface`. Это не обязательно, но при наличии данной аннотации код не скомпилируется, 
если будет больше или меньше, чем 1 абстрактный метод.

Рекомендуется добавлять `@FunctionalInterface`. Это позволит использовать интерфейс в лямбда выражениях, не остерегаясь того, 
что кто-то добавит в интерфейс новый абстрактный метод и он перестанет быть функциональным.

В Java есть встроенные функциональные интерфейсы, размещенные в пакете `java.util.function`. 
Наиболее часто используются: `Consumer<T>`, `Function<T,R>`, `Predicate<T>`, `Supplier<T>`, `UnaryOperator<T>` и их `Bi` – формы. 

## Определение функционального интерфейса

```java
import java.util.function.Predicate;

//Определяем свой функциональный интерфейс
@FunctionalInterface
interface MyPredicate {
    boolean test(Integer value);
}

public class Tester {
    public static void main(String[] args) throws Exception {
        MyPredicate myPredicate = x -> x > 0;
        System.out.println(myPredicate.test(10));   //true

        //Аналогично, но используется встроенный функциональный интерфейс java.util.function.Predicate
        Predicate<Integer> predicate = x -> x > 0;
        System.out.println(predicate.test(-10));    //false
    }
}
```

## Функциональный интерфейс все-таки может содержать боле одного абстрактного метода, но есть одно "НО"

Но оказывается есть один тонкий момент, описанный в **Java Language Specification**: 
“interfaces do not inherit from Object, but rather implicitly declare many of the same methods as Object.”

Это означает, что функциональные интерфейсы **могут содержать дополнительно абстрактные методы, определенные в классе `Object`**. 
Код ниже валиден, ошибок компиляции и времени выполнения не будет:

```java
@FunctionalInterface
public interface Comparator<T> {
   int compare(T o1, T o2);
   boolean equals(Object obj);
   // другие default или static методы
}
```

## Какой из этих интерфейсов функциональный?

```java
@FunctionalInterfce 
interface FunInt {
  abstract public void abstractMethod();
}

interface FunInt1 extends FunInt {}

interface FunInt2 extends FunInt {
  @Override
  abstract public void abstractMethod();
}

interface FunInt3 extends FunInt {
  public default void defMethod(){};
}
```

Правильный ответ – все три. 
- Первый – не содержит в себе никаких методов, но наследует абстрактный метод от родительского интерфейса. 
- Второй – содержит в себе один абстрактный метод, который переопределяет метод родительского интерфейса. 
- Третий – содержит в себе метод по умолчанию, который абстрактным не является, но интерфейс также наследует абстрактный метод, который наследуется от 
родительского интерфейса. Помните не важно сколько у вас методов по умолчанию или статичных методов в функциональном интерфейсе, 
главное, чтобы у вас был только один абстрактный метод.

## Типы интерфейсов

- `Supplier` - (поставщик) используется для создание какого-либо объекта без использования входных параметров. 
```java
Supplier<String> sup = () -> "Java 8";
sout(sup.get());
```
- `Consumer` - (потребитель) используется в том случае, если нам нужно применить какое-то действие или операцию к параметру 
(или к двум параметрам для `BiConsumer`) и при этом в возвращаемом значении нет необходимости.
```java
BiConsumer<String, String> con = (s1, s2) -> sout(s1+s2);
con.accept("Java 8 - ", "BiConsumer");
```
- `Predicate<T>` и `BiPredicate<T, U>` - возвращает `boolean` для одного или двух объектов.
- `Function<T, U>` и `BiFunction<T, U, R>` - принимает объект или два объекта и возвращает объект другого типа.
- `UnaryOperator<T>` это то же самое что `Function<T, T>` и `BinaryOperator<T>` = `Function<T, T, T>` - разновидность `Function`. 
В них входные и выходные обобщенные параметры должны совпадать. 

## Полезные ссылки

[Java functional interfaces - JavaRush](https://javarush.ru/groups/posts/592-java-functional-interfaces)
