# Сериализация (Serializable/Externalizable)

**Сериализация** — это процесс сохранения состояния объекта в последовательность байт.

**Десериализация** — это процесс восстановления объекта из этих байт.

Есть два способа сериализации в java: 
1. реализовать интерфейс `Serializable`
2. реализовать интерфейс `Externalizable`

## Serializable

В Java за процессы сериализации отвечает интерфейс `Serializable`. Этот интерфейс крайне прост: чтобы им пользоваться, не нужно реализовывать ни одного метода!
Интерфейс, у которого нет ни одного метода, выглядит странно :/ Зачем он нужен? Только чтобы предоставить нужную информацию JVM.

При сериализации объекта сериализуются все объекты, на которые он ссылается в своих переменных экземпляра. Это значит, что если в нашем классе используются
переменные не примитивных типов, то классы этих объектов должны реализовывать `Serializable`. Все классы в этой цепочке должны быть `Serializable`, иначе их невозможно будет сериализовать и будет выброшено исключение.

При десериализации вызывается конструктор без параметров родительского **НЕсериализуемого** класса. И если такого конструктора не будет – при десериализации возникнет ошибка. Конструктор же дочернего объекта, того, который мы десериализуем, не вызывается.

## serialVersionUID

Еще один важный момент: в классе, реализующем `Serializable` должна быть переменная `private static final long serialVersionUID`.
Это поле содержит уникальный идентификатор версии сериализованного класса. 

Идентификатор версии есть у любого класса, который имплементирует интерфейс `Serializable`. Он вычисляется по содержимому класса — полям, порядку объявления, методам. И если мы поменяем в нашем классе тип поля и/или количество полей, идентификатор версии моментально изменится. `serialVersionUID` тоже записывается при сериализации класса. 

Когда мы пытаемся провести десериализацию, то есть восстановить объект из набора байт, значение `serialVersionUID` сравнивается со значением `serialVersionUID` класса в нашей программе. Если значения не совпадают, будет выброшено исключение `java.io.InvalidClassException`.

[Зачем использовать SerialVersionUID внутри Serializable класса в Java](https://javarush.ru/groups/posts/1034-zachem-ispoljhzovatjh-serialversionuid-vnutri-serializable-klassa-v-java)

## Зачем нужен transient

`transient` позволяет исключить поле из списка сериализуемых.

## Недостатки Serializable

- Производительность. Внутренний механизм генерирует много служебной информации и использует Reflection API.
- Гибкость. Мы практически не управляем процессом сериализации. За исключением слова transient.
- Не дает возможность зашифровать личные данные (пароль).

## Пример сериализации c использованием Serializable

Объект, который будем сериализовать

```java
import java.io.Serializable;
import java.util.Arrays;

public class SavedGame implements Serializable {

   private static final long serialVersionUID = 1L;

   private String[] territoriesInfo;
   private String[] resourcesInfo;
   private String[] diplomacyInfo;

   public SavedGame(String[] territoriesInfo, String[] resourcesInfo, String[] diplomacyInfo){
       this.territoriesInfo = territoriesInfo;
       this.resourcesInfo = resourcesInfo;
       this.diplomacyInfo = diplomacyInfo;
   }

   public String[] getTerritoriesInfo() {
       return territoriesInfo;
   }

   public void setTerritoriesInfo(String[] territoriesInfo) {
       this.territoriesInfo = territoriesInfo;
   }

   public String[] getResourcesInfo() {
       return resourcesInfo;
   }

   public void setResourcesInfo(String[] resourcesInfo) {
       this.resourcesInfo = resourcesInfo;
   }

   public String[] getDiplomacyInfo() {
       return diplomacyInfo;
   }

   public void setDiplomacyInfo(String[] diplomacyInfo) {
       this.diplomacyInfo = diplomacyInfo;
   }

   @Override
   public String toString() {
       return "SavedGame{" +
               "territoriesInfo=" + Arrays.toString(territoriesInfo) +
               ", resourcesInfo=" + Arrays.toString(resourcesInfo) +
               ", diplomacyInfo=" + Arrays.toString(diplomacyInfo) +
               '}';
   }
}
```

Созраняем объект `SavedGame` в файл

```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;

public class Main {

   public static void main(String[] args) throws IOException {
       //создаем наш объект
       String[] territoryInfo = {"У Испании 6 провинций", "У России 10 провинций", "У Франции 8 провинций"};
       String[] resourcesInfo = {"У Испании 100 золота", "У России 80 золота", "У Франции 90 золота"};
       String[] diplomacyInfo = {"Франция воюет с Россией, Испания заняла позицию нейтралитета"};

       SavedGame savedGame = new SavedGame(territoryInfo, resourcesInfo, diplomacyInfo);

       //создаем 2 потока для сериализации объекта и сохранения его в файл
       FileOutputStream outputStream = new FileOutputStream("C:\\Users\\Username\\Desktop\\save.ser");
       ObjectOutputStream objectOutputStream = new ObjectOutputStream(outputStream);

       // сохраняем игру в файл
       objectOutputStream.writeObject(savedGame);

       //закрываем поток и освобождаем ресурсы
       objectOutputStream.close();
   }
}
```

Результат сериализации

```
¬н sr 	SavedGame        [ 
diplomacyInfot [Ljava/lang/String;[ 
resourcesInfoq ~ [ territoriesInfoq ~ xpur [Ljava.lang.String;­ТVзй{G  xp   t pР¤СЂР°РЅС†РёСЏ РІРѕСЋРµС‚ СЃ Р РѕСЃСЃРёРµР№, РСЃРїР°РЅРёСЏ Р·Р°РЅСЏР»Р° РїРѕР·РёС†РёСЋ РЅРµР№С‚СЂР°Р»РёС‚РµС‚Р°uq ~    t "РЈ РСЃРїР°РЅРёРё 100 Р·РѕР»РѕС‚Р°t РЈ Р РѕСЃСЃРёРё 80 Р·РѕР»РѕС‚Р°t !РЈ Р¤СЂР°РЅС†РёРё 90 Р·РѕР»РѕС‚Р°uq ~    t &РЈ РСЃРїР°РЅРёРё 6 РїСЂРѕРІРёРЅС†РёР№t %РЈ Р РѕСЃСЃРёРё 10 РїСЂРѕРІРёРЅС†РёР№t &РЈ Р¤СЂР°РЅС†РёРё 8 РїСЂРѕРІРёРЅС†РёР№
```

Десериализуем байты из файла обратно в объект
```java
import java.io.*;

public class Main {

   public static void main(String[] args) throws IOException, ClassNotFoundException {
       FileInputStream fileInputStream = new FileInputStream("C:\\Users\\Username\\Desktop\\save.ser");
       ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);
       SavedGame savedGame = (SavedGame) objectInputStream.readObject();
       System.out.println(savedGame);
   }
}
```

Результат десериализации

```
SavedGame{territoriesInfo=[У Испании 6 провинций, У России 10 провинций, У Франции 8 провинций], resourcesInfo=[У Испании 100 золота, У России 80 золота, У Франции 90 золота], diplomacyInfo=[Франция воюет с Россией, Испания заняла позицию нейтралитета]}
```

Если мы уберем поле `serialVersionUID` то получим следующую ошибку

```
InvalidClassException: local class incompatible: stream classdesc serialVersionUID = -196410440475012755, local class serialVersionUID = -6675950253085108747
```

## Совместимые и несовместимые изменения в классах

При внесении изменений в классы, необходимо учитывать, какие из них будут совместимы и не совместимы с сериализацией.

**Совместимые**
- Добавление полей
- Добавление методов `writeObject\readObject` при условии, что `defaultWriteObject\defaultReadObject` будут вызваны вначале
- Удаление методов `writeObject\readObject`
- Добавление `Serializable`
- Изменение доступа к полю
- Изменение static поля на non-static или transient на non-transient

**Несовместимые**
- Удаление поля
- Перемещение класса вверх или вниз по иерархии
- Изменение non-static поля на static или non-transient на transient
- Изменение типа данных у поля
- Изменение `writeObject/readObject` так, что они больше не читают поля по умолчанию
- Изменение `Serializable` на `Externalizable`
- Изменение enum на non-enum
- Удаление `Serializable` или `Externalizable`
- Добавление `writeReplace` или `readResolve` метода к классу

## Externalizable

При имплементации интерфейса `Externalizable` ты должен реализовать два обязательных метода — `writeExternal()` и `readExternal()`.
Вся ответственность за сериализацию и десериализацию будет лежать на программисте. 
Однако теперь ты можешь решить проблему отсутствия контроля над этим процессом! 
Весь процесс программируется напрямую тобой, что, конечно, создает гораздо более гибкий механизм.

## Пример сериализации c использованием Externalizable

```java
import java.io.Externalizable;
import java.io.IOException;
import java.io.ObjectInput;
import java.io.ObjectOutput;
import java.util.Base64;

public class UserInfo implements Externalizable {

   private static final long serialVersionUID = 1L;
   
   private String firstName;
   private String lastName;
   private String superSecretInformation;

   @Override
   public void writeExternal(ObjectOutput out) throws IOException {
       out.writeObject(this.getFirstName());
       out.writeObject(this.getLastName());
       out.writeObject(this.encryptString(this.getSuperSecretInformation()));
   }

   @Override
   public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
       firstName = (String) in.readObject();
       lastName = (String) in.readObject();
       superSecretInformation = this.decryptString((String) in.readObject());
   }

   private String encryptString(String data) {
       String encryptedData = Base64.getEncoder().encodeToString(data.getBytes());
       System.out.println(encryptedData);
       return encryptedData;
   }

   private String decryptString(String data) {
       String decrypted = new String(Base64.getDecoder().decode(data));
       System.out.println(decrypted);
       return decrypted;
   }

   public String getFirstName() {
       return firstName;
   }

   public String getLastName() {
       return lastName;
   }

   public String getSuperSecretInformation() {
       return superSecretInformation;
   }
}
```

## Отличия Serialziable от Externalizable

- Разница в механизме десериализации. 
При использовании `Serializable` под объект просто выделяется память, после чего из потока считываются значения, которыми заполняются все его поля. 
Если мы используем `Serializable`, конструктор объекта не вызывается! Вызывается конструктор без параметров родительского **НЕсериализуемого** класса. 
Вся работа производится через рефлексию.
В случае с `Externalizable` механизм десериализации будет иным. Сперва вызывается конструктор по умолчанию. 
И только потом у созданного объекта вызывается метод `readExternal()`, который и отвечает за заполнение полей объекта. 
Именно поэтому любой класс, имплементирующий интерфейс `Externalizable`, обязан иметь конструктор по умолчанию.
- При `Serializable` `static` поля вообще не сериализуются. При `Externalizable` мы можем это сделать, но это категорически не рекомендуется. 
- Стоит также обратить внимание на переменные с модификатором `final`. При использовании `Serializable` они сериализуются и десериализуются как обычно, 
а вот при использовании `Externalizable` десериализовать `final`-переменную невозможно! Причина проста: все final-поля инициализируются при вызове 
конструктора по умолчанию, и после этого их значение уже невозможно изменить. 
Поэтому для сериализации объектов, содержащих final-поля, используй стандартную сериализацию через `Serializable`.
- При использовании наследования, все классы-наследники, происходящие от какого-то `Externalizable`-класса, тоже должны иметь конструкторы по умолчанию.

## Сериализация Singleton

Проблема сериализации Singleton-ов в том, что после десериализации мы получим другой объект, то есть ссылки на исходный и десериализованный 
объекты не совпадают. Таким образом, сериализация дает возможность создать Singleton еще раз, что нам совсем не нужно. 
Можно, конечно, запретить сериализовать Singleton-ы, но это, фактически, уход от проблемы, а не ее решение.

```java
// Java code to explain effect of  
// Serilization on singleton classes 
import java.io.FileInputStream; 
import java.io.FileOutputStream; 
import java.io.ObjectInput; 
import java.io.ObjectInputStream; 
import java.io.ObjectOutput; 
import java.io.ObjectOutputStream; 
import java.io.Serializable; 
  
class Singleton implements Serializable  { 
    // public instance initialized when loading the class 
    public static Singleton instance = new Singleton(); 
      
    private Singleton()  
    { 
        // private constructor 
    } 
} 
  
  
public class GFG { 
  
    public static void main(String[] args) { 
        try { 
            Singleton instance1 = Singleton.instance; 
            ObjectOutput out = new ObjectOutputStream(new FileOutputStream("file.text")); 
            out.writeObject(instance1); 
            out.close(); 
      
            // deserailize from file to object 
            ObjectInput in = new ObjectInputStream(new FileInputStream("file.text")); 
              
            Singleton instance2 = (Singleton) in.readObject(); 
            in.close(); 
      
            System.out.println("instance1 hashCode:- " + instance1.hashCode()); 
            System.out.println("instance2 hashCode:- " + instance2.hashCode()); 
        } catch (Exception e) { 
            e.printStackTrace(); 
        } 
    }
    
} 

//Output:- 
//instance1 hashCode:- 1550089733
//instance2 hashCode:- 865113938
```

Как видите, hashCode обоих экземпляров отличается, следовательно, есть 2 объекта Singleton класса. Таким образом, класс больше не синглтон.

Чтобы решить эту проблему, мы должны реализовать метод `readResolve()`.

```java
// Java code to remove the effect of 
// Serialization on singleton classes 
import java.io.FileInputStream; 
import java.io.FileOutputStream; 
import java.io.ObjectInput; 
import java.io.ObjectInputStream; 
import java.io.ObjectOutput; 
import java.io.ObjectOutputStream; 
import java.io.Serializable; 

class Singleton implements Serializable { 
	// public instance initialized when loading the class 
	public static Singleton instance = new Singleton(); 
	
	private Singleton() { 
		// private constructor 
	} 
	
	// implement readResolve method 
	protected Object readResolve() { 
		return instance; 
	} 
} 

public class GFG { 

	public static void main(String[] args) { 
		try { 
			Singleton instance1 = Singleton.instance; 
			ObjectOutput out = new ObjectOutputStream(new FileOutputStream("file.text")); 
			out.writeObject(instance1); 
			out.close(); 
		
			// deserailize from file to object 
			ObjectInput in = new ObjectInputStream(new FileInputStream("file.text")); 
			Singleton instance2 = (Singleton) in.readObject(); 
			in.close(); 
		
			System.out.println("instance1 hashCode:- " + instance1.hashCode()); 
			System.out.println("instance2 hashCode:- " + instance2.hashCode()); 
		} catch (Exception e) { 
			e.printStackTrace(); 
		} 
	} 
  
} 

//Output:- 
//instance1 hashCode:- 1550089733
//instance2 hashCode:- 1550089733

```

## Полезные ссылки

[Сериализация как она есть](http://www.skipy.ru/technics/serialization.html)

[Сериализация и десериализация в Java](https://javarush.ru/groups/posts/2022-serializacija-i-deserializacija-v-java)

[Знакомство с интерфейсом Externalizable](https://javarush.ru/groups/posts/2023-znakomstvo-s-interfeysom-externalizable)

[Зачем использовать SerialVersionUID внутри Serializable класса в Java](https://javarush.ru/groups/posts/1034-zachem-ispoljhzovatjh-serialversionuid-vnutri-serializable-klassa-v-java)

[Топ 10 вопросов о сериализации Java на интервью](https://javarevisited.blogspot.com/2011/04/top-10-java-serialization-interview.html)
