# Data Form

Data form biasanya digunakan untuk memasukkan data pada aplikasi, biasa dikenal INSERT atau SAVE Data, pada prosesnya java menginginkan adalah setiap form data yang ada harus berkesuaian dengan model yang sudah dibuatkan sebelumnya, pada sesi kali ini akan membahas tentang penerapan **CRUD** sebagai berikut :

## HTML Form

```java
<!-- Page Content -->
  <th:block th:replace="fragments/template :: app-nav" ></th:block>
  <div class="container">
    <div class="row">
      <div class="col-lg-12 text-center">
        <h1 class="mt-5">Hello, Java Spring Boot</h1>
        <p class="lead">Table : Employee</p>
            <form action="#" th:action="@{/employee/save}" th:object="${employee}"method="POST">
                Name : <input type="text" th:field="*{name}"/><br/>
                Email : <input type="text" th:field="*{email}"/><br/>
                <input type="submit" value="Save Data" />
            </form>
      </div>
    </div>
  </div>
```

## Membuat Repository Data

```java
package com.uinjakarta.smartweb.repository;
import org.springframework.data.jpa.repository.JpaRepository;
import com.uinjakarta.smartweb.model.Employee;

public interface EmployeeRepo extends JpaRepository<Employee, Integer> {

}
```

## Membuat Service Layer sebagai Service

```java
package com.uinjakarta.smartweb.service;
import javax.transaction.Transactional;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import com.uinjakarta.smartweb.model.Employee;
import com.uinjakarta.smartweb.repository.EmployeeRepo;

@Service
@Transactional
public class EmployeeService {

    @Autowired
    private EmployeeRepo employeeRepo;

    public void save(Employee employee) {
        employeeRepo.save(employee);
    }
}
```

## Controller

```java
@Autowired
private EmployeeService employeeService;

@Controller
@RequestMapping("/employee")
public class EmployeeController {

    @GetMapping
    public String index(Model model) {
        model.addAttribute("title", "Employee CRUD");
        model.addAttribute("employee", new Employee());
        return "view_employee";
    }

    @PostMapping("/save")
    @ResponseStatus(HttpStatus.CREATED)
    public void saveData(@ModelAttribute Employee employee) {
            employeeService.save(employee);
    }
}
```

## Jalankan Program

1. Compile ulang
2. Coba akses : [http://localhost:8080/employee](http://localhost:8080/employee)

![](/assets/view-add.png)

## Show Datatable

1. Tambahkan service findAll
2. load findAll from Controller

#### Menambahkan fungsi findALL

```

```

## Memodifikasi Controller index

```

```

## Form Validation

### Modifikasi POJO

```java
@NotNull
public String name;

@Email
public String email;
```

### Modifikasi HTML form

```java
<form action="#" th:action="@{/employee/save}" th:object="${employee}" method="POST">
            Name : <input type="text" th:field="*{name}"/><br/>
            <p th:if="${#fields.hasErrors('name')}" class="label label-danger" th:errors="*{name}"/>
            Email : <input type="text" th:field="*{email}"/><br/>
            <p th:if="${#fields.hasErrors('email')}" class="label label-danger" th:errors="*{email}"/>
            <input type="submit" value="Save Data" />
<!-- //show all error 
<div>
<div style="color: red;" th:each="err : ${#fields.errors('*')}" th:text="${err}" />
</div> 
-->
</form>
```

### Modifikasi Controller

```java
@PostMapping("/save")
public String saveData(Model model, @Valid @ModelAttribute("employee") Employee employee,  BindingResult bindingResult) {
    if(bindingResult.hasErrors()) {
        model.addAttribute("title", "Employee CRUD");
        return "view_employee";
    }

        employeeService.save(employee);
    return "redirect:/employee";
}
```



