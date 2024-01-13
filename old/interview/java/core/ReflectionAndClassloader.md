# Reflection API и ClassLoader

Рефлексия используется для получения или модификации информации о типах во время выполнения программы. 
Этот механизм позволяет получить сведения о классах, интерфейсах, полях, методах, конструкторах во время исполнения программы. 
При этом не нужно знать имена классов, методов или интерфейсов. 
Также этот механизм позволяет создавать новые объекты, выполнять методы, получать и устанавливать значения полей.

## Возможности

- Определить класс объекта
- Получить инфу о модификаторах класса, полях, методах, константах, конструкторах и суперклассах
- Выяснить какие методы принадлежат реализуемому интерфейсу\интерфейсам
- Создать экземпляр класса, причем имя класса неизвестно до момента выполнения программы
- Получить и установить значение поля по имени
- Вызвать метод объекта по имени

## Пример

```java
public class MyClass {
   private int number;
   private String name = "default";
//    public MyClass(int number, String name) {
//        this.number = number;
//        this.name = name;
//    }
   public int getNumber() {
       return number;
   }
   public void setNumber(int number) {
       this.number = number;
   }
   public void setName(String name) {
       this.name = name;
   }
   private void printData(){
       System.out.println(number + name);
   }
}

// Пример как добраться к приватному полю без get метода
public static void main(String[] args) {
   MyClass myClass = new MyClass();
   int number = myClass.getNumber();
   String name = null; //no getter =(
   System.out.println(number + name);//output 0null
   try {
       Field field = myClass.getClass().getDeclaredField("name");
       field.setAccessible(true);
       name = (String) field.get(myClass);
   } catch (NoSuchFieldException | IllegalAccessException e) {
       e.printStackTrace();
   }
   System.out.println(number + name);//output 0default
}

// Создание экземпляра с помощью рефлексии
public static void main(String[] args) {
   MyClass myClass = null;
   try {
       Class clazz = Class.forName(MyClass.class.getName());
       myClass = (MyClass) clazz.newInstance();
   } catch (ClassNotFoundException | InstantiationException | IllegalAccessException e) {
       e.printStackTrace();
   }
   System.out.println(myClass);//output created object reflection.MyClass@60e53b93
}
```

## Описание

`getFields()` возвращает все доступные поля. 
`getDeclaredFields()` возвращает private и protected поля. 
Оба метода не возвращают поля суперкласса.

На момент старта java приложения далеко не все классы оказываются загруженными в JVM. Если в вашем коде нет обращения к классу `MyClass`, то тот, 
кто отвечает за загрузку классов в JVM, а им является `ClassLoader`, никогда его туда и не загрузит. 
Поэтому нужно заставить `ClassLoader` загрузить его и получить описание нашего класса в виде переменной типа `Class`. 
Для этой задачи существует метод `forName(String)`, который принимает имя класса, описание которого нам требуется.
Получив `Сlass`, вызов метода `newInstance()` вернет `Object`, который будет создан по тому самому описанию. Остается привести этот объект к нашему классу 
`MyClass`. 

## Где может пригодится рефлексивный вызов конструкторов? 

Современные технологии java не обходятся без Reflection API. Например, DI (Dependency Injection).

## Рефлексией нельзя изменить private final поле, при этом никакого исключения сгенерировано не будет. 

На самом деле можно, но с небольшой оговоркой - [читать здесь](https://ru.stackoverflow.com/questions/498742/private-final-%D0%9D%D0%B5%D0%BB%D1%8C%D0%B7%D1%8F-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B8%D1%82%D1%8C).

## Минусы Рефлексии

Как и у всего в этом мире, у Рефлексии есть свои недостатки:
- **Худшая производительность** в сравнении с классической работой с классами, методами и переменными;
- **Ограничения безопасности**. Если мы захотим использовать рефлексию на классе, который защищен с помощью специального класса SecurityManager, 
то ничего у не выйдет т.к. этот класс будет выбрасывать исключения каждый раз, как мы попытаемся получить доступ к закрытым членам класса. 
Такая защита может применяться, например, в Апплетах (Applets);
- Получение доступа к внутренностям класса, что **нарушает принцип инкапсуляции**. Фактически, мы получаем доступ туда, куда обычному человеку 
лезть не желательно. Это как с розеткой, ребёнку лучше к ней не лезть, тогда как опытный электрик запросто с ней поладит.

## Можно ли загрузить один и тот же класс дважды разными ClassLoader-ами

#### Пример 1

В данном примере `ClassLoader`-ы разные, но итоговый класс один и тот же.

```java
// Loader 1
public class MyClassLoader extends ClassLoader {

    public MyClassLoader(){
        super(MyClassLoader.class.getClassLoader());
    }

    public Class loadClass(String classname){
        try {
            return super.loadClass(classname);
        } catch (ClassNotFoundException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        return null;
    }
}

// Loader 2
public class AnotherClassLoader extends ClassLoader {

    public AnotherClassLoader(){
        super(AnotherClassLoader.class.getClassLoader());
    }

    public Class loadClass(String classname){
        try {
            return super.loadClass(classname);
        } catch (ClassNotFoundException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        return null;
    }
}
```

Теперь я загружаю класс с именем A, используя эти два разных загрузчика классов. Полагаю, операция `classA1 == newClassA` должна возвращать `false`. Вот код:

```java
public static void main(String[] args) {
        MyClassLoader loader1 = new MyClassLoader();
        AnotherClassLoader newLoader = new AnotherClassLoader();
            System.out.println("Load with Custom Class Loader instance");
            Class classA1 = loader1.loadClass("com.hitesh.coreJava.A");
            System.out.println("Class Loader:::"+classA1.getClassLoader());
            Class newClassA = newLoader.loadClass("com.hitesh.coreJava.A");
            System.out.println("Class Loader:::"+newClassA.getClassLoader());
            System.out.println(classA1==newClassA);
            System.out.println(classA1.hashCode() + " , " + newClassA.hashCode());

    }
```

Но вот результат:

```java
Load with Custom Class Loader instance 
Class Loader:::sun.misc.Launcher$AppClassLoader@11b86e7 
Class Loader:::sun.misc.Launcher$AppClassLoader@11b86e7 
true 
1641745 , 1641745
```

Приведенный выше фрагмент кода верен. Это правда, что любой класс, загруженный в JVM, идентифицируется по `package`, `className`, `Class Loader Name`. 
Таким образом, можно дважды загрузить класс в JVM, используя два разных экземпляра загрузчика классов. Для этого вам нужно явно вызвать `defineClass()` в вашем
коде `Custom Class Loader`, поскольку этот метод проверяет во время выполнения, загружают ли класс два разных экземпляра.

#### Пример 2

В данном примере мы используем один и тот же `ClassLoader` и загружаем один и тот же класс дважды.

```java
public class Test1 {

    static class TestClassLoader1 extends ClassLoader {

        @Override
        public Class<?> loadClass(String name) throws ClassNotFoundException {
            if (!name.equals("Test1")) {
                return super.loadClass(name);
            }
            try {
                InputStream in = ClassLoader.getSystemResourceAsStream("Test1.class");
                byte[] a = new byte[10000];
                int len  = in.read(a);
                in.close();
                return defineClass(name, a, 0, len);
            } catch (IOException e) {
                throw new ClassNotFoundException();
            }
        }
    }


    public static void main(String[] args) throws Exception {
        Class<?> c1 = new TestClassLoader1().loadClass("Test1");
        Class<?> c2 = new TestClassLoader1().loadClass("Test1");
        System.out.println(c1);
        System.out.println(c2);
        System.out.println(c1 == c2);
    }
}
```

Но в результате получаем, что `class`-ы не равны

```java
class Test1
class Test1
false
```

## Полезные ссылки

[Reflection API. Рефлексия. Темная сторона Java](https://javarush.ru/groups/posts/513-reflection-api-refleksija-temnaja-storona-java)
