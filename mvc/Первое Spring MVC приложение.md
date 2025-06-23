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



![image.png](https://cdn2.buildin.ai/s3/c2f0ad26-1b81-4c8a-9037-99feee8d1f9e/image.png?time=1750683600&token=7bb4a89800a9b7069c94bb11031a11c6&role=sharePaid)

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