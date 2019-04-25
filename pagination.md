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

## Thymeleaf HTML



