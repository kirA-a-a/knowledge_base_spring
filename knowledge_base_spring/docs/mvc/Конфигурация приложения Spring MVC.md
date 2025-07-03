# Конфигурация приложения Spring MVC (без Hibernate)

## Что это такое?
Spring MVC — это фреймворк для создания web-приложений на Java. Для работы нужно настроить зависимости, сервлеты, обработку запросов, отображение страниц и подключение к БД (если нужно).

---

## Пошаговая настройка (гайд)

### 1. Добавь зависимости в pom.xml
- Spring MVC, JSTL, Lombok, драйвер БД, C3P0 (если нужна БД)
- Пример:
```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>6.1.10</version>
</dependency>
<!-- и другие -->
```

### 2. Настрой web.xml
- Укажи главный сервлет Spring (DispatcherServlet)
- Пример:
```xml
<servlet>
  <servlet-name>dispatcher</servlet-name>
  <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  <init-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>/WEB-INF/applicationContext.xml</param-value>
  </init-param>
  <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
  <servlet-name>dispatcher</servlet-name>
  <url-pattern>/</url-pattern>
</servlet-mapping>
```

### 3. Настрой applicationContext.xml
- Опиши, где искать компоненты, как обрабатывать запросы, где лежат view (JSP)
- Пример:
```xml
<context:component-scan base-package="com.safronov.spring.mvc"/>
<mvc:annotation-driven/>
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/view/"/>
    <property name="suffix" value=".jsp"/>
</bean>
```

---

## Как это работает?
1. Пользователь отправляет запрос (например, открывает страницу)
2. DispatcherServlet принимает запрос и ищет нужный контроллер
3. Контроллер обрабатывает запрос, выбирает view
4. View (JSP) отображает результат пользователю

---

## Схема слоёв
```
[Браузер]
   |
   v
[Контроллер] -> [View]
```

---

## Мини-глоссарий
- **Spring MVC** — фреймворк для web-приложений
- **DispatcherServlet** — главный обработчик запросов
- **Bean** — объект, управляемый Spring
- **View** — страница, которую видит пользователь (обычно JSP)
- **JSTL** — библиотека тегов для JSP

---

## Советы новичку
- Не бойся xml — просто копируй и меняй под себя
- Всегда проверяй, что все зависимости указаны в pom.xml
- Для простых проектов не нужен Hibernate — достаточно Spring MVC и БД
- Разделяй логику: контроллеры для обработки запросов, view для отображения

---

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.safronov.spring.mvc</groupId>
    <artifactId>spring_course_mvc_hibernate_mvc</artifactId>
    <packaging>war</packaging>
    <version>1.0-SNAPSHOT</version>
    <name>spring_course_mvc_hibernate_mvc Maven Webapp</name>
    <url>http://maven.apache.org</url>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>3.8.1</version>
            <scope>test</scope>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>6.1.10</version>
        </dependency>

        <dependency>
            <groupId>jakarta.servlet.jsp.jstl</groupId>
            <artifactId>jakarta.servlet.jsp.jstl-api</artifactId>
            <version>3.0.0</version>
        </dependency>

        <dependency>
            <groupId>org.glassfish.web</groupId>
            <artifactId>jakarta.servlet.jsp.jstl</artifactId>
            <version>3.0.1</version>
        </dependency>

        <dependency>
            <groupId>org.hibernate.orm</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>6.5.2.Final</version>
        </dependency>

        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>42.3.8</version>
        </dependency>

        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.38</version>
        </dependency>

        <dependency>
            <groupId>com.mchange</groupId>
            <artifactId>c3p0</artifactId>
            <version>0.10.1</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-orm</artifactId>
            <version>6.1.10</version>
        </dependency>

    </dependencies>

    <build>
        <finalName>spring_course_mvc_hibernate_mvc</finalName>
    </build>
</project>
```


В вашем `pom.xml` файле уже добавлены различные зависимости для вашего проекта Spring MVC с использованием Hibernate и JPA. Вот краткий обзор того, что каждый из этих зависимостей делает:

1. **JUnit**: Используется для написания и выполнения юнит-тестов. Указанная версия (`3.8.1`) является устаревшей, рекомендуется использовать более новую версию (например, `4.x` или `5.x`).

2. **Spring Web MVC**: Библиотека, которая предоставляет основные компоненты для разработки веб-приложений на основе Spring Framework.

3. **Jakarta Servlet JSP Taglibs (API и Реализация)**: Эти зависимости необходимы для использования JSTL в ваших JSP-страницах. API предоставляет интерфейсы, а реализация — их конкретные реализации.

4. **Hibernate Core**: Основной модуль Hibernate ORM, который позволяет взаимодействовать с базами данных через объектно-ориентированный интерфейс.

5. **PostgreSQL Driver**: Драйвер JDBC для подключения к базе данных PostgreSQL.

6. **Lombok**: Инструмент для упрощения кода Java. Он автоматически генерирует код (например, конструкторы, геттеры и сеттеры) на основе аннотаций, что уменьшает объем написанного кода и снижает вероятность ошибок.

7. **C3P0**: Пул соединений для управления ресурсами баз данных. Это помогает улучшить производительность приложения за счет повторного использования соединений вместо создания новых для каждого запроса.

8. **Spring ORM**: Поддержка для работы с различными ORM-технологиями, включая Hibernate. Эта зависимость позволяет интегрировать Spring с Hibernate и другими ORM системами. С помощью ORM мы можем отображать java объекты в БД в виде строк таблиц и наоборот



## Наполняем web.xml

```XML
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         id="WebApp_ID" version="3.1">

  <display-name>spring-cource-mvc-hibernate-mvc</display-name>

  <absolute-ordering />

  <servlet>
    <servlet-name>dispatcher</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>/WEB-INF/applicationContext.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>

  <servlet-mapping>
    <servlet-name>dispatcher</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>

  <jsp-config>
    <jsp-property-group>
      <url-pattern>*.jsp</url-pattern>
      <page-encoding>UTF-8</page-encoding>
    </jsp-property-group>
  </jsp-config>

</web-app>
```


Этот файл является файлом конфигурации для веб-приложения на Java, написанного с использованием Java Enterprise Edition (Java EE) и Spring Framework. Файл имеет расширение `web.xml` и используется для описания параметров и компонентов веб-приложения. Давайте разберем его содержимое по частям:

### 1. **XML Declaration**

```XML
<?xml version="1.0" encoding="UTF-8"?>

```


Эта строка указывает версию XML и кодировку документа. В данном случае, документ написан на XML версии 1.0 и использует UTF-8 для кодировки символов.

### 2. **Root Element and Namespace Declarations**

```XML
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         id="WebApp_ID" version="3.1">

```


Этот элемент `<web-app>` является корневым элементом файла конфигурации. Он объявляет, что этот файл является конфигурационным файлом для веб-приложения, использующего спецификацию Java EE версии 3.1. Пространство имен (`xmlns`) указывает, что документ следует спецификации Java EE. Атрибут `xsi:schemaLocation` указывает на URL-адрес схемы, которая используется для проверки валидности этого файла.

### 3. **Display Name**

```XML
<display-name>spring-cource-mvc-hibernate-mvc</display-name>

```


Этот элемент определяет имя приложения, которое будет отображаться в административных панелях или других инструментах для управления приложением. В данном случае, имя приложения установлено как `spring-cource-mvc-hibernate-mvc`.

### 4. **Absolute Ordering**

```XML
<absolute-ordering />

```


Этот элемент используется для фиксации порядка загрузки фильтров и сервлетов. В данном случае, он пустой, что означает, что порядок загрузки не изменяется.

### 5. **Servlet Configuration**

```XML
<servlet>
  <servlet-name>dispatcher</servlet-name>
  <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  <init-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>/WEB-INF/applicationContext.xml</param-value>
  </init-param>
  <load-on-startup>1</load-on-startup>
</servlet>

```


Этот блок определяет конфигурацию сервлета `dispatcher`, который является частью Spring MVC.

- `<servlet-name>`: Имя сервлета, которое будет использоваться для его идентификации.

- `<servlet-class>`: Класс, который будет запущен как сервлет. В данном случае, это `org.springframework.web.servlet.DispatcherServlet`, центральный компонент Spring MVC, который обрабатывает запросы и маршрутизирует их к соответствующим контроллерам.

- `<init-param>`: Определяет параметры инициализации для сервлета. В данном случае, параметр `contextConfigLocation` указывает на расположение файла конфигурации приложения (`applicationContext.xml`), который содержит настройки и определения бинов (beans).

- `<load-on-startup>`: Указывает, что сервлет должен быть загружен при старте сервера. Значение `1` означает, что этот сервлет будет одним из первых загруженных.

### 6. **Servlet Mapping**

```XML
<servlet-mapping>
  <servlet-name>dispatcher</servlet-name>
  <url-pattern>/</url-pattern>
</servlet-mapping>

```


Этот блок определяет, какие URL-адреса будут обрабатываться данным сервлетом. В данном случае, все запросы, поступающие на сервер, будут перехватываться сервлетом `dispatcher`, так как `<url-pattern>/` означает, что он будет обрабатывать все запросы.

### 7. **JSP Configuration**

```XML
<jsp-config>
  <jsp-property-group>
    <url-pattern>*.jsp</url-pattern>
    <page-encoding>UTF-8</page-encoding>
  </jsp-property-group>
</jsp-config>

```


Этот блок определяет свойства для JSP страниц. В данном случае:

- `<url-pattern>*.jsp</url-pattern>`: Определяет, что все JSP страницы должны использовать указанные свойства.

- `<page-encoding>UTF-8</page-encoding>`: Устанавливает кодировку страниц, чтобы они использовали UTF-8. Это важно для правильного отображения символов, особенно если страницы содержат текст на различных языках.

## Файл applicationContext

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd">

    <context:component-scan base-package="com.safronov.spring.mvc"/>

    <mvc:annotation-driven/>

    <bean
            class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/view/"/>
        <property name="suffix" value=".jsp"/>
    </bean>

    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource"
          destroy-method="close">
        <property name="driverClass" value="org.postgresql.Driver"/>
        <property name="jdbcUrl" value="jdbc:postgresql://localhost:5432/my_db?useSSL=false&amp;serverTimezone=UTC"/>
        <property name="user" value="bestuser"/>
        <property name="password" value="bestuser"/>
    </bean>

    <bean id="sessionFactory"
          class="org.springframework.orm.hibernate5.LocalSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <property name="packagesToScan" value="com.safronov.spring.mvc.entity"/>
        <property name="hibernateProperties">
            <props>
                <prop key="hibernate.dialect">org.hibernate.dialect.PostgreSQLDialect</prop>
                <prop key="hibernate.show_sql">true</prop>
            </props>
        </property>
    </bean>

    <bean id="transactionManager"
          class="org.springframework.orm.hibernate5.HibernateTransactionManager">
        <property name="sessionFactory" ref="sessionFactory"/>
    </bean>

    <tx:annotation-driven transaction-manager="transactionManager"/>

</beans>
```


Этот XML файл является конфигурационным файлом для Spring Framework, который используется для настройки различных компонентов приложения, таких как обработка веб-запросов, управление транзакциями и работа с базой данных. Давайте разберем его по частям:

### 1. Основные пространства имен:

```XML
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd">

```


- `xmlns:beans` - пространство имен для основных элементов Spring.

- `xmlns:context` - пространство имен для автоматического сканирования компонентов.

- `xmlns:mvc` - пространство имен для настройки MVC-контроллеров.

- `xmlns:tx` - пространство имен для управления транзакциями.

### 2. Сканирование компонентов:

```XML
<context:component-scan base-package="com.safronov.spring.mvc"/>

```


Эта строка указывает Spring на то, что он должен автоматически сканировать все классы в пакете `com.safronov.spring.mvc` и его подпакетах, чтобы найти аннотированные компоненты (например, `@Controller`, `@Service`, `@Repository`).

### 3. Настройка MVC:

```XML
<mvc:annotation-driven/>

```


Эта строка активирует обработку аннотаций, связанных с MVC, такие как `@RequestMapping`, `@Controller`, и другие. Она также включает поддержку для конвертации типов данных и обработки исключений.

### 4. Настройка резолвера представлений:

```XML
<bean
        class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/view/"/>
    <property name="suffix" value=".jsp"/>
</bean>

```


Этот бин настраивает `InternalResourceViewResolver`, который определяет, где находятся JSP-файлы, которые будут использоваться для отображения веб-страниц. В данном случае, префикс `/WEB-INF/view/` и суффикс `.jsp` указывают, что все представления должны быть найдены в директории `/WEB-INF/view/` с расширением `.jsp`.

### 5. Настройка подключения к базе данных:

```XML
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource"
      destroy-method="close">
    <property name="driverClass" value="org.postgresql.Driver"/>
    <property name="jdbcUrl" value="jdbc:postgresql://localhost:5432/my_db?useSSL=false&amp;serverTimezone=UTC"/>
    <property name="user" value="bestuser"/>
    <property name="password" value="bestuser"/>
</bean>

```


Этот бин настраивает источник данных (`dataSource`) с использованием C3P0, который предоставляет подключение к базе данных PostgreSQL. Он содержит информацию о драйвере, URL базы данных, имени пользователя и пароле.



В бине dataSource описыаются параметры подключения к БД

В нашем случае мы исползуем c3p0, как connection pool, так как механизм создания пула, очень трудозатратный и поэтому мы используем c3p0

Далее, мы указываем драйвер для подключения, jdbcUrl и пользователя под которым будем подключаться



### 6. Настройка `SessionFactory` для Hibernate:

```XML
<bean id="sessionFactory"
      class="org.springframework.orm.hibernate5.LocalSessionFactoryBean">
    <property name="dataSource" ref="dataSource"/>
    <property name="packagesToScan" value="com.safronov.spring.mvc.entity"/>
    <property name="hibernateProperties">
        <props>
            <prop key="hibernate.dialect">org.hibernate.dialect.PostgreSQLDialect</prop>
            <prop key="hibernate.show_sql">true</prop>
        </props>
    </property>
</bean>

```


Этот бин создает `SessionFactory`, который используется для создания сессий Hibernate. Он ссылается на ранее настроенный `dataSource`, указывает, какие пакеты должны быть сканированы для поиска сущностей (`packagesToScan`), и задает свойства Hibernate, такие как диалект базы данных и возможность вывода SQL-запросов в консоль.



Бин sessionFactory, нам необходим, для получения сессий из sessionFactory для подключения к БД

В параметре dataSource мы указываем ссылку на бин dataSource

Указываем путь, где лежат наши entity

Указываем конфигурацию hibernate, в нашем случае мы указали диалект (данная настройка необходима говорит hibernate что мы будем рабоать с postgreSQL и есму неоходимо использовать запросы совместимы с postgreSQL) и логирование sql запросов совершаемых hibernate



### 7. Настройка менеджера транзакций:

```XML
<bean id="transactionManager"
      class="org.springframework.orm.hibernate5.HibernateTransactionManager">
    <property name="sessionFactory" ref="sessionFactory"/>
</bean>
<tx:annotation-driven transaction-manager="transactionManager"/>

```


Эти строки настраивают менеджер транзакций для Hibernate, который позволяет управлять транзакциями с помощью аннотаций, таких как `@Transactional`. Менеджер ссылается на ранее настроенный `sessionFactory`, а `<tx:annotation-driven>` активирует обработку аннотаций для управления транзакциями.



При работе с hibernate при указании hql запров, мы перед запросом открывали транзакцию, а после выполнения запроса - закрывали транзакцию

Указание бина transactionManager позволяет нам напрямую не работать с тразакциями, тоесть спринг будет за нас это делать автоматически

Но для этого нам будет на методом, который совершает какую-ту операцию в БД указать аннотацию @Transactional

Для активации аннотация @Transactional мы используем

`<tx:annotation-driven transaction-manager="transactionManager"/>`



```Java
    @Autowired
    private SessionFactory sessionFactory;

    @Override
    @Transactional
    public List<Employee> getAllEmployees() {
         Session session = sessionFactory.getCurrentSession();
         return session.createQuery("from Employee", Employee.class).getResultList();
    }
```


