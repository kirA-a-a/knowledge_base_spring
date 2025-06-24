Аннотация @Service помечает класс, содержащий бизнес-логику

В иерархии компонентов приложения Service является соеденительным звеном между Controller-ом и DAO (это компонент, который отвечает за работу с базой данных. Он изолирует всю логику доступа к данным от бизнес-логики и контроллеров, обеспечивая чистую архитектуру и тестируемость.)

Controller - это метод, который определяет логику работы приложения, когда клиент переходит на ту или иную страницу

```Java
import org.springframework.web.bind.annotation.*;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String sayHello() {
        return "Привет, это контроллер на Spring!";
    }
}
```

> В данном, случае когда на клиенте будет будет осущетвслен переход по пути /hello, то ему будет возвращен ответ "Привет, это контроллер на Spring!" <br> @Service - это специализированный @Component. Данный класс, в своих методах используем методы из DAO. <br> При поиске компонентов, Spring так же будет регистрировать все классы с аннотацией @Service в Spring Container-е


![image.png](https://cdn2.buildin.ai/s3/e07e1157-99d8-4b03-82ef-7a34a736f62d/image.png?time=1750786200&token=52f784ba6a15c3e23d5f23452d893718&role=sharePaid)



Метод в Secvice

```Java
@Service
public class EmployeeServiceImpl implements EmployeeService {

    @Autowired
    private EmployeeDAOImpl employeeDAO;

    @Override
    @Transactional
    public List<Employee> getAllEmployees() {
        return employeeDAO.getAllEmployees();
    }
}
```

> В данном случае, у нас есть EmployeeDAOImpl, который реализует всю логику работы с БД. У него есть метод, который получет всех работников и в Secvice мне жедаем одноименный метод и возвращаем результат работы метода .getAllEmployees() из EmployeeDAOImpl <br> То есть, в контроллерре мы обращаемся к сервису, а сервис обращается к ДАО <br> Так же, аннотацию @Transactional мы переносим в класс Service