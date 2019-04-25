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

## Thymeleaf HTML



