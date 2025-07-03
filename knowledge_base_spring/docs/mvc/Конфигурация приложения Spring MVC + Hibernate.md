# Конфигурация приложения Spring MVC + Hibernate

## Что это такое?
- **Spring MVC** — фреймворк для создания web-приложений на Java
- **Hibernate** — библиотека для работы с базой данных через Java-объекты (ORM)
- Вместе они позволяют делать сайты, где данные хранятся в БД, а бизнес-логика и отображение разделены

---

## Зачем их связывать?
- Spring MVC отвечает за обработку запросов, отображение страниц, валидацию и т.д.
- Hibernate позволяет удобно сохранять и получать данные из БД, не пиша SQL вручную
- Вместе: контроллеры принимают запросы, сервисы обрабатывают логику, DAO через Hibernate работают с БД

---

## Пошаговая настройка (гайд)

1. **Создай maven-проект**
   - Используй шаблон `maven-archetype-webapp`
   - Это создаст структуру для web-приложения

2. **Добавь зависимости в pom.xml**
   - Spring, Hibernate, драйвер БД (например, PostgreSQL), JSTL, Lombok, C3P0 (для пула соединений)
   - Пример:
```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>6.1.10</version>
</dependency>
<dependency>
    <groupId>org.hibernate.orm</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>6.5.2.Final</version>
</dependency>
<!-- и другие -->
```

3. **Скачай Tomcat**
   - Это сервер, на котором будет работать твой сайт
   - Свяжи его с IDE (например, IntelliJ IDEA)

4. **Создай нужные папки и пакеты**
   - Обычно: `controller`, `service`, `dao`, `entity`, `config`

5. **Настрой web.xml**
   - Укажи сервлет Spring DispatcherServlet
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

6. **Настрой applicationContext.xml**
   - Опиши бины Spring, настрой подключение к БД, укажи параметры Hibernate
   - Пример:
```xml
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
    <property name="driverClass" value="org.postgresql.Driver"/>
    <property name="jdbcUrl" value="jdbc:postgresql://localhost:5432/your_db"/>
    <property name="user" value="your_user"/>
    <property name="password" value="your_password"/>
</bean>
<!-- и другие настройки -->
```

---

## Схема слоёв
```
[Браузер]
   |
   v
[Контроллер] -> [Сервис] -> [DAO] -> [Hibernate] -> [БД]
```

---

## Мини-глоссарий
- **Maven** — система сборки и управления зависимостями
- **Tomcat** — сервер для запуска web-приложений
- **DispatcherServlet** — главный сервлет Spring MVC
- **Bean** — объект, управляемый Spring
- **DAO** — слой для работы с БД
- **Entity** — класс, который отображается на таблицу в БД
- **JSTL** — библиотека тегов для JSP
- **C3P0** — пул соединений с БД

---

## Советы новичку
- Не бойся ошибок — читай stacktrace, он подскажет, где проблема
- Всегда проверяй настройки подключения к БД
- Разделяй логику по слоям: контроллеры, сервисы, DAO
- Используй аннотации Spring для автоматизации (например, @Controller, @Service, @Repository)

---