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

1. Tambahkan fungsi findAll pada service
2. memodifikasi Controller index

#### Menambahkan fungsi findALL pada service

```java
public List<Employee> findAll(){
    return employeeRepo.findAll();
}
```

#### Memodifikasi Controller index

```java
model.addAttribute("employees", employeeService.findAll());
```

#### Menambahkan HTML table

```java
<table class="table">
  <thead>
    <tr>
      <th scope="col">Name</th>
      <th scope="col">Email</th>
      <th scope="col">Address</th>
      <th scop="col">Action</th>
    </tr>
  </thead>
    <tbody>
        <tr th:each="row : ${employees}">
            <td th:text="${row.name}"></td>
            <td th:text="${row.email}"></td>
            <td th:text="${row.address}"></td>
            <td>
            <a href="#" th:attr="data-id=${row.employeeId}" class="btn btn-sm btn-warning">Edit</a>
        <a href="#" th:attr="data-id=${row.employeeId}" class="btn btn-sm btn-danger">Hapus</a>
        </td>
        </tr>
    </tbody>
</table>
```

#### Hasil Browser

![](/assets/hasil-browser)

## Delete Data

### Javascript

```js
<script type="text/javascript" th:inline="javascript">
    $(document).ready(function(){
        var webRoot = /*[[@{/}]]*/
        $('.btn-warning').on('click', function(){
            var id = $(this).attr('data-id');
            var conf=confirm("Are you sure delete this data ?");
            if(conf){
                window.location=webRoot + 'employee/delete/' + id;
            }
            return false;
        });
    });
</script>
```

### Controller

```java
@GetMapping("/delete/{id}")
public String delete(@PathVariable("id") int id) {
        employeeService.delete(id);
    return "redirect:/employee";
}
```

#### Service

```java
public void delete(int id) {
    // TODO Auto-generated method stub
    Employee employee = new Employee();
    employee.setEmployeeId(id);
    employeeRepo.delete(employee);
}
```

## Update Data

### Modal

```html
<div class="modal" id="edit-modal" tabindex="-1" role="dialog">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Edit Employee</h5>
                    <button type="button" class="close" data-dismiss="modal"
                        aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <form action="#" th:action="@{/employee/update}"
                        th:object="${employee}" method="POST">
                <div class="modal-body">
                        <input type="hidden" id="edit-employeeId" th:field="*{employeeId}" />
                        Name : <input id="edit-name" type="text" th:field="*{name}" /><br />
                        Email : <input id="edit-email" type="text" th:field="*{email}" /><br />

                </div>
                <div class="modal-footer">
                <input value="Update" type="submit" class="btn btn-primary" />
                    <button type="button" class="btn btn-secondary"
                        data-dismiss="modal">Close</button>
                </div>
                </form>
            </div>
        </div>
    </div>
```

### Javascript

```js
$('.btn-warning').on('click', function(){
	var id = $(this).attr('data-id');
	$.ajax({
		url : webRoot + 'employee/get/'+ id,
		success: function(employee){
			console.log(employee);
			$('#edit-employeeId').val(employee.employeeId);
			$('#edit-name').val(employee.name);
			$('#edit-email').val(employee.email);
		}
	});
	$('#edit-modal').modal();
});
```

### controller

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

### Hasil Browser

![](/assets/result-browser)

