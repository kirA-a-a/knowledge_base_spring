# Знакомство с JSON

## Что такое JSON?
JSON (JavaScript Object Notation) — это простой текстовый формат для хранения и обмена данными. Он очень популярен для передачи данных между сервером и браузером, а также между разными сервисами.

---

## Зачем нужен JSON?
- Для обмена данными между приложениями (например, фронт и бэк)
- Для хранения настроек, конфигов, данных
- Для работы с REST API

---

## Как выглядит JSON?
```json
{
  "name": "Иван",
  "age": 25,
  "email": "ivan@test.ru",
  "skills": ["Java", "Spring", "SQL"]
}
```
- Ключи и строки — всегда в двойных кавычках
- Массивы — в квадратных скобках
- Объекты — в фигурных скобках

---

## Схема: Java-объект <-> JSON
```
Java объект:
User {
  String name;
  int age;
  String email;
  List<String> skills;
  String house; // может быть null
}

<== сериализация/десериализация ==>

JSON:
{
  "name": "Иван",
  "age": 25,
  "email": "ivan@test.ru",
  "skills": ["Java", "Spring", "SQL"],
  "house": null
}
```
- Если какое-то поле в Java-объекте не заполнено, в JSON оно будет равно null или отсутствовать.
- Для преобразования JSON в Java-объект, у класса должны быть конструктор без аргументов и поля, совпадающие по имени с ключами JSON.

---

## Как использовать JSON в Java?
- Для преобразования Java-объектов в JSON и обратно используют библиотеки (например, Jackson)
- В Spring это делается "из коробки" — контроллер может возвращать объект, а Spring сам превратит его в JSON

### Пример:
```java
@RestController
public class UserController {
    @GetMapping("/user")
    public User getUser() {
        return new User("Иван", 25, "ivan@test.ru");
    }
}
```
_Ответ будет в формате JSON:_
```json
{
  "name": "Иван",
  "age": 25,
  "email": "ivan@test.ru"
}
```
- Для получения значений из JSON используются геттеры, для установки — сеттеры.

---

## Мини-глоссарий
- **JSON** — текстовый формат для обмена данными
- **Сериализация** — преобразование объекта в строку (например, в JSON)
- **Десериализация** — преобразование строки обратно в объект
- **Jackson** — популярная библиотека для работы с JSON в Java

---

## Советы новичку
- Всегда используй двойные кавычки для ключей и строк
- Проверяй JSON через онлайн-валидаторы (например, https://jsonlint.com)
- Не путай JSON с JavaScript — это просто формат, а не язык программирования
- Для корректной работы с JSON в Java-классах должны быть геттеры, сеттеры и конструктор без аргументов

---

JSON - JavaScript Data Notation

Формат данных JSON представляет собой текстовую информацию

JSON используется для хранения и особенно для обмена информацией

JSON не привязан к какому-то конкретному ЯП и используется повсеместно

Формат данных JSON содержит коллекцию пар ключ-значение

JSON Data Binding или JSON Mapping - это привязка JSON к Java объекту. Данная привязка используется для преобразования
Java обхекта в JSON и наоборот

> Если у нас есть есть JSON и мы хотим получить из него Java объект, то у нас должны быть такие классы, в которых есть
> NoArgsConstructor и поля, которые будут соответствовать полям JSON

Spring для преобразования из Java объекта в JSON или наоборот использует библиотеку Jackson

Для преобразования, у нас должен быть написан java класс, соответсвтуеющий json

> Для получения значений JSON используются гетеры, а для устанволения значения испольуются сетеры

