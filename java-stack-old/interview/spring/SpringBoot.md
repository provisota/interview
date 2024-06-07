<!-- TOC -->
* [Spring Boot](#spring-boot)
  * [Что такое Spring Boot и каковы его основные особенности?](#что-такое-spring-boot-и-каковы-его-основные-особенности)
  * [В чем разница между Spring и Spring Boot?](#в-чем-разница-между-spring-и-spring-boot)
  * [Как мы можем настроить приложение Spring Boot с Maven?](#как-мы-можем-настроить-приложение-spring-boot-с-maven)
  * [Что такое Spring Initializr?](#что-такое-spring-initializr)
  * [Какие есть стартеры Spring Boot?](#какие-есть-стартеры-spring-boot)
  * [Как отключить определенную автоконфигурацию?](#как-отключить-определенную-автоконфигурацию)
  * [Как зарегистрировать пользовательскую автоконфигурацию?](#как-зарегистрировать-пользовательскую-автоконфигурацию)
  * [Как указать автоконфигурации, чтобы она отступила, когда бин существует?](#как-указать-автоконфигурации-чтобы-она-отступила-когда-бин-существует)
  * [Как задеплоить веб-приложения Spring Boot в виде файлов Jar и War?](#как-задеплоить-веб-приложения-spring-boot-в-виде-файлов-jar-и-war)
  * [Как использовать Spring Boot для приложений командной строки?](#как-использовать-spring-boot-для-приложений-командной-строки)
  * [Каковы возможные источники внешней конфигурации?](#каковы-возможные-источники-внешней-конфигурации)
  * [Что означает, что Spring Boot поддерживает Relaxed Binding?](#что-означает-что-spring-boot-поддерживает-relaxed-binding)
  * [Для чего используются инструменты разработки Spring Boot?](#для-чего-используются-инструменты-разработки-spring-boot)
  * [Как писать интеграционные тесты?](#как-писать-интеграционные-тесты)
  * [Для чего используется Spring Boot Actuator?](#для-чего-используется-spring-boot-actuator)
  * [Какой способ лучше настроить проект Spring Boot - с помощью application.properties или YAML?](#какой-способ-лучше-настроить-проект-spring-boot---с-помощью-applicationproperties-или-yaml)
  * [Какие основные аннотации предлагает Spring Boot?](#какие-основные-аннотации-предлагает-spring-boot)
  * [Как изменить порт по умолчанию в Spring Boot?](#как-изменить-порт-по-умолчанию-в-spring-boot)
  * [Какие встроенные серверы поддерживают Spring Boot и как изменить настройки по умолчанию?](#какие-встроенные-серверы-поддерживают-spring-boot-и-как-изменить-настройки-по-умолчанию)
  * [Зачем нужны Spring Profiles?](#зачем-нужны-spring-profiles)
  * [Starters](#starters)
  * [Web Starter](#web-starter)
  * [Test Starter](#test-starter)
  * [Data JPA Starter](#data-jpa-starter)
  * [Аннотации](#аннотации)
      * [@SpringBootApplication](#springbootapplication)
      * [@EnableAutoConfiguration](#enableautoconfiguration)
  * [Auto-Configuration Conditions](#auto-configuration-conditions)
      * [@ConditionalOnClass и @ConditionalOnMissingClass](#conditionalonclass-и-conditionalonmissingclass)
      * [@ConditionalOnBean и @ConditionalOnMissingBean](#conditionalonbean-и-conditionalonmissingbean)
      * [@ConditionalOnProperty](#conditionalonproperty)
      * [@ConditionalOnResource](#conditionalonresource)
      * [@ConditionalOnWebApplication и @ConditionalOnNotWebApplication](#conditionalonwebapplication-и-conditionalonnotwebapplication)
      * [@ConditionalExpression](#conditionalexpression)
      * [@Conditional](#conditional)
  * [Полезные ссылки](#полезные-ссылки)
<!-- TOC -->

# Spring Boot

## Что такое Spring Boot и каковы его основные особенности?

`Spring Boot` - это, по сути, платформа для быстрой разработки приложений, построенная на основе `Spring Framework`. Благодаря автоматической настройке и поддержке
встроенного сервера приложений, в сочетании с обширной документацией и поддержкой сообщества, `Spring Boot` на сегодняшний день является одной из самых популярных 
технологий в экосистеме `Java`.

Вот несколько важных особенностей:

- `Стартеры` - набор дескрипторов зависимостей для включения соответствующих зависимостей на ходу.
- `Автоконфигурация` - способ автоматической настройки приложения на основе зависимостей, представленных в пути к классам.
- `Актуатор` - для получения готовых к производству функций, таких как мониторинг.
- `Безопасность`
- `Логирование`

## В чем разница между Spring и Spring Boot?

`Spring Framework` предоставляет несколько функций, которые упрощают разработку веб-приложений. Эти функции включают `dependency injection`, `data binding`,
аспектно-ориентированное программирование, `data access` и многое другое.

С годами `Spring` становится все более и более сложным, и количество настроек, требуемых для этого приложения, может быть устрашающим. Вот где пригодится 
`Spring Boot` - он упрощает настройку приложения `Spring`.

По сути, в то время как `Spring` не пользуется особой популярностью, `Spring Boot` имеет самоуверенный взгляд на платформу и библиотеки, что позволяет нам быстро
приступить к работе.

Вот два наиболее важных преимущества `Spring Boot`:

- Автоматическая настройка приложений на основе артефактов, обнаруженных в пути к классам
- Предоставлять нефункциональные функции, общие для приложений в производственной среде, такие как проверки безопасности или работоспособности

## Как мы можем настроить приложение Spring Boot с Maven?

Мы можем включить `Spring Boot` в проект `Maven`, как и любую другую библиотеку. Однако лучший способ - унаследовать от родительского проекта `spring-boot-starter`
и объявить зависимости для стартеров `Spring Boot`. Это позволяет нашему проекту повторно использовать настройки `Spring Boot` по умолчанию.

Наследовать проект `spring-boot-starter-parent` очень просто - нам нужно только указать родительский элемент в `pom.xml`:

```xml
<parent>
     <groupId> org.springframework.boot </groupId>
     <artifactId> Spring-boot-starter-parent </artifactId>
     <version> 2.3.0.RELEASE </version>
</parent>
```

Использовать стартовый родительский проект удобно, но не всегда возможно. Например, если наша компания требует, чтобы все проекты унаследовали от стандартного 
`POM`, мы все равно можем извлечь выгоду из управления зависимостями `Spring Boot` с использованием настраиваемого родителя.

## Что такое Spring Initializr?

`Spring Initializr` - это удобный способ создать проект `Spring Boot`.

Мы можем перейти на сайт `Spring Initializr`, выбрать инструмент управления зависимостями (`Maven` или `Gradle`), язык (`Java`, `Kotlin` или `Groovy`), схему 
упаковки (`Jar` или `War`), версию и зависимости и загрузить проект.

Это создает для нас скелет проекта и экономит время на настройку, так что мы можем сосредоточиться на добавлении бизнес-логики.

Даже когда мы используем мастер новых проектов нашей `IDE` (например, `STS` или `Eclipse` с плагином `STS`) для создания проекта `Spring Boot`, он использует 
`Spring Initializr` под капотом.

## Какие есть стартеры Spring Boot?

Каждый стартер играет роль универсального центра для всех необходимых нам технологий `Spring`. Затем транзитивно подключаются и управляются согласованным образом 
другие необходимые зависимости.

Все стартеры находятся в группе `org.springframework.boot`, и их имена начинаются с `spring-boot-starter-`. Этот шаблон именования упрощает поиск стартеров, 
особенно при работе с IDE, которые поддерживают поиск зависимостей по имени.

На момент написания этой статьи в нашем распоряжении более 50 стартеров. Чаще всего используются:

- `spring-boot-starter`: стартер ядра, включая поддержку автоконфигурации, логирование и YAML
- `spring-boot-starter-aop`: стартер для аспектно-ориентированного программирования с помощью `Spring AOP` и `AspectJ`
- `spring-boot-starter-data-jpa`: стартер для использования `Spring Data JPA` с `Hibernate`
- `spring-boot-starter-security`: стартер для использования `Spring Security`
- `spring-boot-starter-test`: стартер для тестирования приложений `Spring Boot`
- `spring-boot-starter-web`: стартер для создания веб-приложений, включая `RESTful`, с использованием `Spring MVC`

## Как отключить определенную автоконфигурацию?

Если мы хотим отключить конкретную автоконфигурацию, мы можем указать это с помощью атрибута `exclude` аннотации `@EnableAutoConfiguration`. Например, этот фрагмент 
кода нейтрализует `DataSourceAutoConfiguration`:

```java
// other annotations
@EnableAutoConfiguration(exclude = DataSourceAutoConfiguration.class)
public class MyConfiguration { }
```

Если бы мы включили автоконфигурацию с аннотацией `@SpringBootApplication`, которая имеет `@EnableAutoConfiguration` в качестве метааннотации, мы могли бы отключить 
автоконфигурацию с помощью атрибута с тем же именем:

```java
/ other annotations
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)
public class MyConfiguration { }
```

Мы также можем отключить автоконфигурацию с помощью свойства среды `spring.autoconfigure.exclude`. Этот параметр в файле `application.properties` делает то же 
самое, что и раньше:

```java
spring.autoconfigure.exclude = org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```

## Как зарегистрировать пользовательскую автоконфигурацию?

Чтобы зарегистрировать класс автоконфигурации, мы должны указать его полное имя в разделе `EnableAutoConfiguration` в файле `META-INF/spring.factories`:

```java
org.springframework.boot.autoconfigure.EnableAutoConfiguration=com.baeldung.autoconfigure.CustomAutoConfiguration
```

Если мы создаем проект с `Maven`, этот файл должен быть помещен в каталог `resources/META-INF`, который окажется в указанном месте на этапе `package`.

## Как указать автоконфигурации, чтобы она отступила, когда бин существует?

Чтобы дать классу автоконфигурации команду отступить, когда компонент уже существует, мы можем использовать аннотацию `@ConditionalOnMissingBean`. Наиболее 
заметные атрибуты этой аннотации:
- `value`: типы бинов для проверки
- `name`: имена бинов для проверки

При размещении в методе, аннотированом `@Bean`, целевой тип по умолчанию соответствует типу возврата метода:

```java
@Configuration
public class CustomConfiguration {
    @Bean
    @ConditionalOnMissingBean
    public CustomService service() { ... }
}
```

## Как задеплоить веб-приложения Spring Boot в виде файлов Jar и War?

Традиционно мы упаковываем веб-приложение в файл `WAR`, а затем развертываем его на внешнем сервере. Это позволяет нам размещать несколько приложений на одном 
сервере. В то время, когда не хватало процессора и памяти, это был отличный способ сэкономить ресурсы.

Однако все изменилось. Компьютерное оборудование сейчас довольно дешево, и все внимание переключилось на конфигурацию серверов. Небольшая ошибка в настройке 
сервера при развертывании может привести к катастрофическим последствиям.

`Spring` решает эту проблему, предоставляя плагин, а именно `spring-boot-maven-plugin`, для упаковки веб-приложения в виде исполняемого `JAR`. Чтобы включить этот
плагин, просто добавьте элемент плагина в `pom.xml`:

```xml
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
</plugin>
```

Установив этот плагин, мы получим `fat JAR` после выполнения фазы `package`. Этот `JAR` содержит все необходимые зависимости, включая встроенный сервер. 
Таким образом, нам больше не нужно беспокоиться о настройке внешнего сервера.

Затем мы можем запустить приложение так же, как обычный исполняемый файл `JAR`.

Обратите внимание, что элемент `packaging` в файле `pom.xml` должен быть установлен на `jar` для создания файла `JAR`:

```xml
<packaging>jar</packaging>
```

Если мы не включим этот элемент, по умолчанию он также будет `jar`.

Если мы хотим создать файл `WAR`, измените элемент упаковки на `war`:

```xml
<packaging>war</packaging>
```

И оставьте зависимость контейнера от упакованного файла:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <scope>provided</scope>
</dependency>
```

После выполнения фазы `package` Maven у нас будет разворачиваемый файл `WAR`.

## Как использовать Spring Boot для приложений командной строки?

Как и любая другая программа `Java`, приложение командной строки `Spring Boot` должно иметь метод `main()`. Этот метод служит точкой входа, которая вызывает метод 
`SpringApplication#run` для начальной загрузки приложения:

```java
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class);
        // other statements
    }
}
```

Затем класс `SpringApplication` запускает контейнер `Spring` и автоматически настраивает бины.

Обратите внимание, что мы должны передать класс конфигурации методу `run()`, чтобы он работал в качестве основного источника конфигурации. По соглашению этим 
аргументом является сам входной класс.

После вызова метода `run()` мы можем выполнять другие операторы, как в обычной программе.

## Каковы возможные источники внешней конфигурации?

`Spring Boot` обеспечивает поддержку внешней конфигурации, позволяя запускать одно и то же приложение в различных средах. Мы можем использовать файлы `properties`, 
файлы `YAML`, `environment variables`, `system properties` и аргументы параметров командной строки, чтобы указать свойства конфигурации.

Затем мы можем получить доступ к этим свойствам с помощью аннотации `@Value`, связанного объекта с помощью аннотации `@ConfigurationProperties` или абстракции 
`Environment`.

## Что означает, что Spring Boot поддерживает Relaxed Binding?

`Relaxed Binding` в `Spring Boot` применима к типобезопасной привязке свойств конфигурации.

При `relaxed binding` ключ свойства не обязательно должен точно совпадать с именем свойства. Такое свойство среды может быть записано в `camelCase`, `kebab-case`, 
`snake_case` или в верхнем регистре со словами, разделенными символами подчеркивания.

Например, если свойство в классе `bean`-компонента с аннотацией `@ConfigurationProperties` названо `myProp`, оно может быть связано с любым из этих свойств среды:
`myProp`, `my-prop`, `my_prop` или `MY_PROP`.

## Для чего используются инструменты разработки Spring Boot?

`Spring Boot Developer Tools`, или `DevTools`, - это набор инструментов, упрощающих процесс разработки. Чтобы включить эти функции во время разработки, нам просто
нужно добавить зависимость в файл `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
</dependency>
```

Модуль `spring-boot-devtools` автоматически отключается, если приложение работает в `production` среде. При переупаковке архивов этот модуль также исключается по 
умолчанию. Следовательно, это не приведет к накладным расходам на наш конечный продукт.

По умолчанию `DevTools` применяет свойства, подходящие для среды разработки. Эти свойства отключают кэширование шаблонов, включают ведение логов для веб-группы и
тд. В результате у нас есть разумная конфигурация времени разработки без установки каких-либо свойств.

Приложения, использующие `DevTools`, перезапускаются при изменении файла в `Classpath`. Это очень полезная функция в разработке, так как она дает быструю обратную
связь для изменений.

По умолчанию статические ресурсы, включая шаблоны представлений, не запускают перезапуск. Вместо этого изменение ресурса вызывает обновление браузера. Обратите 
внимание, что это может произойти только в том случае, если в браузере установлено расширение `LiveReload` для взаимодействия со встроенным сервером `LiveReload`, 
который содержит `DevTools`.

## Как писать интеграционные тесты?

При запуске интеграционных тестов для приложения `Spring` у нас должен быть `ApplicationContext`.

Чтобы облегчить нам жизнь, `Spring Boot` предоставляет специальную аннотацию для тестирования - `@SpringBootTest`. Эта аннотация создает `ApplicationContext` из
классов конфигурации, указанных в его атрибуте classes.

Если атрибут `classes` не установлен, `Spring Boot` ищет основной класс конфигурации. Поиск начинается с пакета, содержащего тест, до тех пор, пока не будет найден
класс, помеченный `@SpringBootApplication` или `@SpringBootConfiguration`.

## Для чего используется Spring Boot Actuator?

По сути, `Actuator` оживляет приложения `Spring Boot`, предоставляя готовые к работе функции. Эти функции позволяют нам отслеживать и управлять приложениями, когда
они работают в производственной среде.

Интегрировать `Spring Boot Actuator` в проект очень просто. Все, что нам нужно сделать, это включить пускатель `spring-boot-starter-actuator` в файл `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

`Spring Boot Actuator` может предоставлять операционную информацию с помощью эндпоинтов `HTTP` или `JMX`. Однако большинство приложений используют `HTTP`, где
идентификатор конечной точки и префикс `/actuator` образуют путь `URL`.

Вот некоторые из наиболее распространенных встроенных эндпоинтов, которые предоставляет `Actuator`:

- `env`: Предоставляет свойства среды
- `health`: показывает информацию о состоянии приложения.
- `httptrace`: отображает информацию трассировки HTTP.
- `info`: отображает произвольную информацию о приложении.
- `metrics`: показывает информацию о показателях.
- `loggers`: показывает и изменяет конфигурацию регистраторов в приложении.
- `mappings`: отображает список всех путей `@RequestMapping`

## Какой способ лучше настроить проект Spring Boot - с помощью application.properties или YAML?

`YAML` предлагает множество преимуществ по сравнению с файлами `application.properties`, например:

- Больше ясности и лучше читаемость
- Идеально подходит для данных иерархической конфигурации, которые также представлены в лучшем, более читаемом формате
- Поддержка Map, Lists и скалярных типов
- Может включать несколько профилей в один файл

Однако его написание может быть немного сложным и подверженным ошибкам из-за правил отступов.

## Какие основные аннотации предлагает Spring Boot?

Основные аннотации, которые предлагает `Spring Boot`, находятся в `org.springframework.boot.autoconfigure` и его подпакетах. Вот пара основных:

- `@EnableAutoConfiguration` - чтобы `Spring Boot` искал компоненты автоконфигурации в своем пути к классам и автоматически применял их.
- `@SpringBootApplication` - используется для обозначения основного класса загрузочного приложения. Эта аннотация объединяет аннотации `@Configuration`,
`@EnableAutoConfiguration` и `@ComponentScan` с их атрибутами по умолчанию.

## Как изменить порт по умолчанию в Spring Boot?

Мы можем изменить порт по умолчанию для сервера, встроенного в `Spring Boot`, одним из следующих способов:

- мы можем определить это в файле `application.properties` (или `application.yml`), используя свойство `server.port`
- программно - в нашем основном классе @`SpringBootApplication` мы можем установить `server.port` в экземпляре `SpringApplication`
- используя командную строку - при запуске приложения как файла `jar` мы можем установить `server.port` в качестве аргумента команды `java`:

```java
java -jar -Dserver.port = 8081 myspringproject.jar
```

## Какие встроенные серверы поддерживают Spring Boot и как изменить настройки по умолчанию?

На сегодняшний день `Spring MVC` поддерживает `Tomcat`, `Jetty` и `Undertow`. `Tomcat` - это сервер приложений по умолчанию, поддерживаемый веб-стартером 
`Spring Boot`.

`Spring WebFlux` поддерживает `Netty`, `Tomcat`, `Jetty` и `Undertow` с `Reactor Netty` по умолчанию.

В `Spring MVC`, чтобы изменить значение по умолчанию, скажем, на `Jetty`, нам нужно исключить `Tomcat` и включить `Jetty` в зависимости:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>
```

Точно так же, чтобы изменить значение по умолчанию в `WebFlux` на `UnderTow`, нам нужно исключить `Reactor Netty` и включить `UnderTow` в зависимости.

## Зачем нужны Spring Profiles?

При разработке приложений для предприятия мы обычно имеем дело с несколькими средами, такими как `Dev`, `QA` и `Prod`. Свойства конфигурации для этих сред 
различны.

Например, мы можем использовать встроенную базу данных `H2` для `Dev`, но `Prod` может иметь проприетарный `Oracle` или `DB2`. Даже если СУБД одинакова для разных
сред, `URL`-адреса определенно будут разными.

Чтобы сделать это простым и понятным, в `Spring` есть профили, которые помогают разделить конфигурацию для каждой среды. Таким образом, вместо того, чтобы 
поддерживать это программно, свойства можно хранить в отдельных файлах, таких как `application-dev.properties` и `application-prod.properties`. По умолчанию 
`application.properties` указывает на текущий активный профиль с помощью `spring.profiles.active`, чтобы выбрать правильную конфигурацию.

## Starters

Управление зависимостями - важнейший аспект любого сложного проекта. А делать это вручную - далеко не идеально; чем больше времени вы потратите на это, тем меньше 
времени у вас будет на другие важные аспекты проекта.

Стартеры Spring Boot были созданы для решения именно этой проблемы. Стартовые POM - это набор удобных дескрипторов зависимостей, которые вы можете включить в свое 
приложение. Вы получаете полный набор зависимостей для всей Spring и связанной с ней технологии, которая вам нужна, без необходимости рыться в примерах кода и
копировать и вставлять множество зависимостей по-отдельности.

## Web Starter

Во-первых, давайте посмотрим на разработку службы `REST`; мы можем использовать такие библиотеки, как `Spring MVC`, `Tomcat` и `Jackson` - множество зависимостей 
для одного приложения.

Стартеры `Spring Boot` могут помочь уменьшить количество добавляемых вручную зависимостей, просто добавив одну зависимость. Поэтому вместо того, чтобы вручную
указывать зависимости, просто добавьте один стартер, как в следующем примере:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

Теперь мы можем создать `REST`-контроллер. Для простоты мы не будем использовать базу данных и сосредоточимся на контроллере `REST`:

```java
@RestController
public class GenericEntityController {
    private List<GenericEntity> entityList = new ArrayList<>();
 
    @RequestMapping("/entity/all")
    public List<GenericEntity> findAll() {
        return entityList;
    }
 
    @RequestMapping(value = "/entity", method = RequestMethod.POST)
    public GenericEntity addEntity(GenericEntity entity) {
        entityList.add(entity);
        return entity;
    }
 
    @RequestMapping("/entity/findby/{id}")
    public GenericEntity findById(@PathVariable Long id) {
        return entityList
          .stream()
          .filter(entity -> entity.getId().equals(id))
          .findFirst()
          .get();
    }
}
```

`GenericEntity` - это простой `bean`-компонент с идентификатором типа `Long` и значением типа `String`.

Вот и все - с запущенным приложением вы можете получить доступ к `http://localhost:8080/entity/all` и проверить, работает ли контроллер.

## Test Starter

Для тестирования мы обычно используем следующий набор библиотек: `Spring Test`, `JUnit`, `Hamcrest` и `Mockito`. Мы можем включить все эти библиотеки вручную, 
но можно использовать стартер `Spring Boot` для автоматического включения этих библиотек следующим образом:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

Обратите внимание, что вам не нужно указывать номер версии артефакта. `Spring Boot` определит, какую версию использовать - все, что вам нужно указать, это версия 
артефакта `spring-boot-starter-parent`. Если в дальнейшем вам потребуется обновить библиотеку загрузки и зависимости, просто обновите версию загрузки в одном
месте, а все остальное сделает она сама.

Давайте действительно протестируем контроллер, который мы создали в предыдущем примере.

Проверить контроллер можно двумя способами:
- Использование `mock` окружение
- Использование встроенного контейнера сервлетов (например, `Tomcat` или `Jetty`)

В этом примере мы будем использовать `mock` окружение:

```java
@RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(classes = Application.class)
@WebAppConfiguration
public class SpringBootApplicationIntegrationTest {
    @Autowired
    private WebApplicationContext webApplicationContext;
    private MockMvc mockMvc;
 
    @Before
    public void setupMockMvc() {
        mockMvc = MockMvcBuilders.webAppContextSetup(webApplicationContext).build();
    }
 
    @Test
    public void givenRequestHasBeenMade_whenMeetsAllOfGivenConditions_thenCorrect()
      throws Exception { 
        MediaType contentType = new MediaType(MediaType.APPLICATION_JSON.getType(),
        MediaType.APPLICATION_JSON.getSubtype(), Charset.forName("utf8"));
        mockMvc.perform(MockMvcRequestBuilders.get("/entity/all")).
        andExpect(MockMvcResultMatchers.status().isOk()).
        andExpect(MockMvcResultMatchers.content().contentType(contentType)).
        andExpect(jsonPath("$", hasSize(4))); 
    } 
}
```

Приведенный выше тест вызывает эндпоинт `/entity/all` и проверяет, что ответ `JSON` содержит 4 элемента. Чтобы этот тест прошел, мы также должны инициализировать
наш список в классе контроллера:

```java
public class GenericEntityController {
    private List<GenericEntity> entityList = new ArrayList<>();
 
    {
        entityList.add(new GenericEntity(1l, "entity_1"));
        entityList.add(new GenericEntity(2l, "entity_2"));
        entityList.add(new GenericEntity(3l, "entity_3"));
        entityList.add(new GenericEntity(4l, "entity_4"));
    }
    //...
}
```

Здесь важно то, что аннотация `@WebAppConfiguration` и `MockMVC` являются частью модуля Spring теста, `hasSize` используется из библиотеки `Hamcrest`, а `@Before`
аннотация `JUnit`. Все они доступны при импорте зависимости стартера.

## Data JPA Starter

Вместо того, чтобы определять все связанные `JPA` зависимости вручную, давайте воспользуемся стартером:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

Обратите внимание, что у нас есть автоматическая поддержка как минимум следующих баз данных: `H2`, `Derby` и `Hsqldb`. В нашем примере мы будем использовать `H2`.

Теперь создадим репозиторий для нашей сущности:

```java
public interface GenericEntityRepository extends JpaRepository<GenericEntity, Long> {}
```

Пора проверить код. Вот тест JUnit:

```java
@RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(classes = Application.class)
public class SpringBootJPATest {
    
    @Autowired
    private GenericEntityRepository genericEntityRepository;
 
    @Test
    public void givenGenericEntityRepository_whenSaveAndRetreiveEntity_thenOK() {
        GenericEntity genericEntity = genericEntityRepository.save(new GenericEntity("test"));
        GenericEntity foundedEntity = genericEntityRepository.findOne(genericEntity.getId());
        
        assertNotNull(foundedEntity);
        assertEquals(genericEntity.getValue(), foundedEntity.getValue());
    }
}
```

Мы не тратили время на указание поставщика базы данных, `URL`-адреса и учетных данных. Никакой дополнительной настройки не требуется, поскольку мы пользуемся 
надежными настройками загрузки по умолчанию; но, конечно, все эти детали можно настроить при необходимости.

## Аннотации

#### @SpringBootApplication

Мы используем эту аннотацию, чтобы отметить главный класс приложения `Spring Boot`:

```java
@SpringBootApplication
class VehicleFactoryApplication {
    public static void main(String[] args) {
        SpringApplication.run(VehicleFactoryApplication.class, args);
    }
}
```

`@SpringBootApplication` содержит аннотации `@Configuration`, `@EnableAutoConfiguration` и `@ComponentScan` с их атрибутами по умолчанию.

#### @EnableAutoConfiguration

`@EnableAutoConfiguration`, как следует из названия, включает автоконфигурацию. Это означает, что `Spring Boot` ищет компоненты автоконфигурации в своем пути к
классам и автоматически применяет их.

Обратите внимание, что мы должны использовать эту аннотацию с `@Configuration`:

```java
@Configuration
@EnableAutoConfiguration
class VehicleFactoryConfig {}
```

## Auto-Configuration Conditions

Обычно, когда мы пишем собственные автоконфигурации, мы хотим, чтобы `Spring` использовал их условно. Мы также можем добиться этого с помощью аннотаций.

Мы можем разместить аннотации в этом разделе на классах `@Configuration` или методах `@Bean`.

#### @ConditionalOnClass и @ConditionalOnMissingClass

Используя эти условия, `Spring` будет использовать помеченный `bean`-компонент автоконфигурации, только если класс в аргументе аннотации присутствует/отсутствует:

```java
@Configuration
@ConditionalOnClass(DataSource.class)
class MySQLAutoconfiguration {}
```

#### @ConditionalOnBean и @ConditionalOnMissingBean

Мы можем использовать эти аннотации, когда хотим определить условия на основе наличия или отсутствия определенного `bean`-компонента:

```java
@Bean
@ConditionalOnBean(name = "dataSource")
LocalContainerEntityManagerFactoryBean entityManagerFactory() {}
```

#### @ConditionalOnProperty

С помощью этой аннотации мы можем создавать условия для значений свойств:

```java
@Bean
@ConditionalOnProperty(
    name = "usemysql", 
    havingValue = "local"
)
DataSource dataSource() {}
```

#### @ConditionalOnResource

Мы можем заставить `Spring` использовать определение только при наличии определенного ресурса:

```java
@ConditionalOnResource(resources = "classpath:mysql.properties")
Properties additionalProperties() {}
```

#### @ConditionalOnWebApplication и @ConditionalOnNotWebApplication

С помощью этих аннотаций мы можем создавать условия в зависимости от того, является ли текущее приложение веб-приложением или нет:

```java
@ConditionalOnWebApplication
HealthCheckController healthCheckController() {}
```

#### @ConditionalExpression

Мы можем использовать эту аннотацию в более сложных ситуациях. `Spring` будет использовать отмеченное определение, когда выражение `SpEL` будет оценено как 
истинное:

```java
@Bean
@ConditionalOnExpression("${usemysql} && ${mysqlserver == 'local'}")
DataSource dataSource() {}
```

#### @Conditional

Для еще более сложных условий мы можем создать класс, оценивающий настраиваемое условие. Мы говорим `Spring` использовать это настраиваемое условие с 
`@Conditional`:

```java
@Conditional(HibernateCondition.class)
Properties additionalProperties() {}
```

Пример реализации HibernateCondition:
```java
import org.springframework.context.annotation.Condition;
import org.springframework.context.annotation.ConditionContext;
import org.springframework.core.type.AnnotatedTypeMetadata;

public class HibernateCondition implements Condition {

    @Override
    public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
        // application specific condition check
        return true;
    }

}
```

## Полезные ссылки

[Spring Boot Interview Questions - Baeldung](https://www.baeldung.com/spring-boot-interview-questions#q15-what-is-spring-boot-actuator-used-for)

[Intro to Spring Boot Starters - Baeldung](https://www.baeldung.com/spring-boot-starters)

[Spring Boot Annotations - Baeldung](https://www.baeldung.com/spring-boot-annotations#enable-autoconfiguration)
