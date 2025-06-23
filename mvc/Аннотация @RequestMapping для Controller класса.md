```Java
package com.safronov.spring.mvc;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;

import javax.servlet.http.HttpServletRequest;

@Controller
@RequestMapping("/course")
public class MyController {


    @RequestMapping("/")
    public String showFirstView(){
        return "myView";
    }

    @RequestMapping("askDetails")
    public String askEmployeeDetails(){
        return "ask-emp-details-view";
    }

    @RequestMapping("showDetails")
    public String showEmpDetails(){
        return "show-emp-details-view";
    }

}

```


> При указании аннотации @RequestMapping("/course") на классе, то параметр указанный над классом, будет добавлять к каждому запросу при открытии вью

Например:

> {host}/course{все методы из класса, помечанного аннотацией @RequestMapping}

