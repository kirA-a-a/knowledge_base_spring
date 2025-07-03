# Аннотация @RequestMapping для Controller класса (Spring MVC)

## Что такое @RequestMapping?

Это специальная аннотация в Spring, которая связывает HTTP-запросы (например, переходы по ссылкам или отправку форм) с методами вашего Java-класса (контроллера). Проще: она говорит, какой метод будет вызван при обращении к определённому адресу на сайте.

---

## Зачем это нужно?
- Чтобы ваш сайт/приложение понимало, какой код запускать при переходе по разным адресам (URL)
- Для организации логики обработки запросов

---

## Пример кода с пояснениями
```java
package com.safronov.spring.mvc;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller // Помечает класс как контроллер (обрабатывает запросы)
@RequestMapping("/course") // Все методы этого класса будут доступны по адресу /course/...
public class MyController {

    @RequestMapping("/") // Обрабатывает запрос по адресу /course/
    public String showFirstView() {
        return "myView"; // Возвращает имя view (страницы), которую надо показать
    }

    @RequestMapping("askDetails") // Обрабатывает запрос по адресу /course/askDetails
    public String askEmployeeDetails() {
        return "ask-emp-details-view";
    }

    @RequestMapping("showDetails") // Обрабатывает запрос по адресу /course/showDetails
    public String showEmpDetails() {
        return "show-emp-details-view";
    }
}
```

---

## Как это работает?
- Когда пользователь заходит на сайт по адресу `/course/`, Spring вызывает метод `showFirstView()`
- Если по адресу `/course/askDetails` — вызывается `askEmployeeDetails()`
- Если по адресу `/course/showDetails` — вызывается `showEmpDetails()`

_Все эти методы возвращают строку — это имя страницы (view), которую Spring покажет пользователю._

---

## Мини-глоссарий
- **Контроллер (Controller)** — класс, который принимает и обрабатывает запросы от пользователя
- **Аннотация** — специальная метка в коде, которая даёт подсказку Spring, как работать с этим классом или методом
- **View** — страница, которую видит пользователь (например, HTML/JSP)
- **URL** — адрес страницы в браузере

---

## Советы новичку
- Всегда указывай слэш `/` в начале пути в @RequestMapping
- Если не знаешь, какой метод вызывается — смотри в адресную строку браузера
- Если страница не открывается — проверь, правильно ли написан путь в @RequestMapping и имя view

---

