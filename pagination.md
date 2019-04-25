# Pagination

Pagination adalah salah metode yang sangat penting untuk diimplementasikan dalam setiap menyajikan data yang besar, dengan hadirnya spring boot, maka implementasi yang sangat menyulitkan akan mudah jika menggunakan spring data. untuk pagination tersebut dapat dikita modifikasi sebagai berikut :

## Repository

```java
#sama tidak banyak perubahan.
public interface EmployeeRepo extends JpaRepository<Employee, Integer> {

}
```

## Service

Ada beberapa untuk bisa dimodifikasi adalah :

1. Pageable Parameter sebagai inputan.
2. memanggil findAll dengan parameter pageable.
3. Return Page&lt;Entity&gt;

```java
public Page<Employee> findAll(Pageable pageable){
    return employeeRepo.findAll(pageable);
}
```

## Controller

Hampir sama dengan service, menghadirkan Pageable Parameter sebagai inputan sebagai lalu lintas data pagination, contoh sebagai berikut:

```java
@GetMapping
@ResponseBody
public Page index(Model model, Pageable pageable) {
    Page page = employeeService.findAll(pageable);
    return page;
}
```

output :

```
{"content":[],"pageable":{"sort":{"sorted":false,"unsorted":true,"empty":true},"offset":0,"pageSize":20,"pageNumber":0,"unpaged":false,"paged":true},"totalElements":0,"last":true,"totalPages":0,"size":20,"number":0,"sort":{"sorted":false,"unsorted":true,"empty":true},"numberOfElements":0,"first":true,"empty":true}
```

pada hasil menginginkan output nya adalah text/html maka :

```java
@GetMapping
public String index(Model model,@PageableDefault(size=10) Pageable pageable) {
    model.addAttribute("title", "Employee CRUD");
    model.addAttribute("employee", new Employee());
    Page page = employeeService.findAll(pageable);
    model.addAttribute("page", page);
    
    //currentPage
    int numberOfShowing = 3;
    int currentPage = page.getNumber()+1;
    //startPaging
    int startPaging = ((currentPage - numberOfShowing ) < 0 ) ? 0 : currentPage - numberOfShowing;  
    //endPaging
    int endPaging = ((currentPage + numberOfShowing) > page.getTotalPages()) ? page.getTotalPages() : (currentPage-1) + numberOfShowing; 
    model.addAttribute("page", page);
    model.addAttribute("startPaging", startPaging);
    model.addAttribute("endPaging", endPaging);
    return "view_employee";
}
```

## Thymeleaf HTML

```java
<div id="pagination">
    <nav aria-label="Page navigation example">
        <ul class="pagination">
            <li th:if="${page.hasPrevious()}" class="page-item"><a
                class="page-link"
                th:href="@{/employee(page=${page.number-1},size=${page.size})}">Previous</a>
            </li>
            <span th:each="i: ${#numbers.sequence(0, page.totalPages - 1)}">
                <li class="page-item"
                th:classappend="${i == page.pageable.pageNumber} ? active">
                    <a class="page-link"
                    th:href="@{/employee(page=${i},size=${page.size})}">[[${i}+1]]</a>
                </li>
            </span>
            <li th:if="${page.hasNext()}" class="page-item"><a
                class="page-link"
                th:href="@{/employee(page=${page.number+1},size=${page.size})}">Next</a>
            </li>
        </ul>
    </nav>
</div>
```



