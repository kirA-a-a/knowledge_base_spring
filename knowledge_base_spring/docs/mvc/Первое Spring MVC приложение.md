# Первое Spring MVC приложение

## Что ты сделаешь?
- Создашь простое web-приложение на Java с помощью Spring MVC
- Научишься создавать контроллер и отображать страницу

---

## Пошаговый гайд

### 1. Создай maven-проект (webapp)
- В IDE выбери шаблон maven-archetype-webapp

### 2. Добавь зависимости в pom.xml
- Spring MVC, JSTL, Lombok и т.д.

### 3. Настрой web.xml
- Укажи DispatcherServlet (см. предыдущие файлы)

### 4. Создай applicationContext.xml
- Опиши, где искать компоненты, настрой view resolver

### 5. Создай контроллер
```java
@Controller // Помечает класс как контроллер
public class HelloController {
    @GetMapping("/hello")
    public String sayHello() {
        return "hello"; // имя view (JSP)
    }
}
```

### 6. Создай view (JSP)
- Файл: /WEB-INF/view/hello.jsp
```jsp
<html>
<body>
    <h1>Привет, это первое Spring MVC приложение!</h1>
</body>
</html>
```

### 7. Запусти Tomcat и перейди на http://localhost:8080/hello
- Должна открыться твоя страница

---

## Как это работает?
- Пользователь заходит на /hello
- DispatcherServlet ищет контроллер с @GetMapping("/hello")
- Контроллер возвращает имя view (hello)
- View resolver ищет файл hello.jsp и показывает его пользователю

---

## Мини-глоссарий
- **Контроллер** — класс, который принимает запросы
- **View** — страница, которую видит пользователь
- **DispatcherServlet** — главный обработчик запросов
- **JSP** — технология для создания web-страниц на Java

---

## Советы новичку
- Не бойся ошибок — читай stacktrace, он подскажет, где проблема
- Всегда проверяй, что все файлы лежат в нужных папках
- Начинай с простого — один контроллер, одна страница

---

@Controller - это специальный компонент (разновидность компонентов), это означает что при сканировании спрингом пакетов, то классы помечанные аннотацией @Controller тоже будут добавлены в контейнер спринга



## Создание контролера

Создаем метод, внутри контроллера, с помощью которого будет происзходить вызов нашего view



```Java
    @RequestMapping("/")
    public String showRegisterForm(){
        return "myView";
    }
```


> Данная страница будет возвращаться, когда мы открываем наш сайт в борайзере|

Аннотация @RequestMapping("/") связывает нашу страницув браузре с кодом. Получается, когма мы открываем страницу "путь" + "значение из "@RequestMapping" то мы получаем наше страницу, которую возвращает наш метод

Данный метод возвращает тип данный String, потому что он возвращает наименование нашего View



![mvc схема](https://upload.wikimedia.org/wikipedia/commons/a/a0/MVC-Process.svg)

> А полное наименование формируется в нашем файле applicationComtext



```Java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <context:component-scan base-package="com.safronov.spring.mvc" />

    <mvc:annotation-driven/>

    <bean
            class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/view/" />
        <property name="suffix" value=".jsp" />
    </bean>

</beans>
```


> При помощи prefix и suffix мы формируем полное имя нашего файла и оно получается имет вид <br>  <br> valueInPrefix + возвращемая строка в методе в контроллере + valueInSuffix