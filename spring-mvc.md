# Spring MVC

Kerangka kerja Spring Web MVC menyediakan arsitektur Model-View-Controller \(MVC\) dan komponen-komponen siap yang dapat digunakan untuk mengembangkan aplikasi web yang fleksibel. Pola MVC menghasilkan pemisahan berbagai aspek aplikasi \(logika input, logika bisnis, dan logika UI\).

* Model merangkum data aplikasi dan secara umum akan terdiri dari POJO.
* View bertanggung jawab untuk memberikan data model dan secara umum menghasilkan output HTML yang dapat ditafsirkan oleh browser.

* Controller bertanggung jawab untuk memproses permintaan pengguna dan membangun model yang sesuai dan meneruskannya ke tampilan untuk rendering.

## Simple CRUD \(Create Read Update Delete\)

### Table : Employee

![](/assets/table-employee)

## POJO sebagai Model

Berikut ini akan kita buatkan Model deskripsi table berbasis Object, dengan hadirnya JPA, hal ini sangat memungkin dimana sebelumnya biasa menggunakan SQL Native. dengan Model ini akan kita definisikan Object dan Properti sebagai bagian dari struktur data yang akan disimpan secara persistance di dalam database.

untuk itu perlu dilakukan pembuat package Model tersendiri sebagai berikut:

![](/assets/package-model)

#### Membuat Class Employee

```java
package com.uinjakarta.smartweb.model;
import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

@Entity
@Table(name="EMPLOYEE")
public class Employee {

    @Id
    @GeneratedValue(strategy=GenerationType.AUTO)
    @Column(name="employee_id")
    public int employeeId;
    public String name;
    @Column(name="address")
    public String address;
    public String email;
    public int getEmployeeId() {
        return employeeId;
    }
    public void setEmployeeId(int employeeId) {
        this.employeeId = employeeId;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getAddress() {
        return address;
    }
    public void setAddress(String address) {
        this.address = address;
    }
    public String getEmail() {
        return email;
    }
    public void setEmail(String email) {
        this.email = email;
    }

}
```

Sebelum dilanjutkan ke Controller, lebih baik untuk dicoba terlebih dahulu dengan menjalankan project. sehingga jika tidak terjadi masalah, maka tentunya POJO diatas akan membuatkan table EMPLOYEE pada MySQL. bisa di cek melalui commandline :

```command
mysql> use sb_uin_jakarta
Database changed
mysql> show tables;
+------------------------------+
| Tables_in_pre_sb_uin_jakarta |
+------------------------------+
| employee                     |
| hibernate_sequence           |
+------------------------------+
2 rows in set (0.01 sec)

mysql> desc employee;
+-------------+--------------+------+-----+---------+-------+
| Field       | Type         | Null | Key | Default | Extra |
+-------------+--------------+------+-----+---------+-------+
| employee_id | int(11)      | NO   | PRI | NULL    |       |
| address     | varchar(255) | YES  |     | NULL    |       |
| email       | varchar(255) | YES  |     | NULL    |       |
| name        | varchar(255) | YES  |     | NULL    |       |
+-------------+--------------+------+-----+---------+-------+
4 rows in set (0.01 sec)

mysql>
```

Terlihat jelas pada command diatas, sudah berhasil membuat table Employee dengan model yang dibuat sebelumnya.

## HTML sebagai View

Seperti yang sudah di singgung sebelumnya View akan bertanggung jawab sebagai interaksi user dengan aplikasi dalam hal ini adalah tampilan yang ada di browser \(Front End\). namun demikian tentu web developer harus memiliki waktu yang cukup untuk mempelajari itu semua terutama adalah User Experiance \(UX\). dalam aplikasi kali ini akan menggunakan _**Thymeleaf Engine Template.**_

Untuk mempersingkat waktu sudah disiapkan untuk bisa di **Copy Paste, **yaitu UI Framework dengan simple Bootstrap dan Jquery bisa diakses sebagai layout di aplikasi yang sedang kita buat pada:

[https://github.com/arrizaqu-matrial/workshop-uin-2019/blob/master/view\_content.md](https://github.com/arrizaqu-matrial/workshop-uin-2019/blob/master/view_content.md).

### Membuat DIrectory Fragment

Buatlah directory Fragments pada template, yaitu **src-&gt;main-&gt;resources-&gt;templates-&gt;fragments** seperti gambar berikut ini :

![](/assets/directory-fragment.png)

### Membuat FIle HTML

1. #### template.html

   Buatlah file tersebut di dalam directory _**fragments**_

   ```html
   <!DOCTYPE html>
   <html>
   <head th:fragment="header">
   <title th:text="${title}">Template</title>
   <meta charset="utf-8">
   <meta name="viewport"
       content="width=device-width, initial-scale=1, shrink-to-fit=no">
   <meta name="description" content="simple workshop UIN Jakarta">
   <meta name="author" content="arrizaqu">
   <title>Home</title>
   <!-- Bootstrap core CSS -->
   <link rel="stylesheet"
       href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
       integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T"
       crossorigin="anonymous">
   <!-- Bootstrap core JavaScript -->
   <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js"
       integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo"
       crossorigin="anonymous"></script>
   <script
       src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"
       integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1"
       crossorigin="anonymous"></script>
   <script
       src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"
       integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM"
       crossorigin="anonymous"></script>
   </head>

   <body>
       <div th:fragment="app-nav">
           <!-- Navigation -->
           <nav class="navbar navbar-expand-lg navbar-dark bg-dark static-top">
               <div class="container">
                   <a class="navbar-brand" href="#">Xsis - Uin Jakarta</a>
                   <button class="navbar-toggler" type="button" data-toggle="collapse"
                       data-target="#navbarResponsive" aria-controls="navbarResponsive"
                       aria-expanded="false" aria-label="Toggle navigation">
                       <span class="navbar-toggler-icon"></span>
                   </button>
                   <div class="collapse navbar-collapse" id="navbarResponsive">
                       <ul class="navbar-nav ml-auto">
                           <li class="nav-item active"><a class="nav-link" href="#">Home
                                   <span class="sr-only">(current)</span>
                           </a></li>
                           <li class="nav-item"><a class="nav-link" href="#">Contact</a>
                           </li>
                       </ul>
                   </div>
               </div>
           </nav>
       </div>
   </body>
   </html>
   ```

2. #### view\_employee.html

   Buat file index.html pada directory templates.

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head th:replace="fragments/template :: header"></head>
   <body>
     <!-- Page Content -->
     <th:block th:replace="fragments/template :: app-nav" ></th:block>
     <div class="container">
       <div class="row">
         <div class="col-lg-12 text-center">
           <h1 class="mt-5">Hello, Java Spring Boot</h1>
           <p class="lead">Table : Employee</p>
               Tulis kontent disini ..
         </div>
       </div>
     </div>
   </body>
   </html>
   ```

## Employee Controller

Pertama kali tentu membuat Controller dengan nama **EmployeeController** pada package controller.

```java
@Controller
@RequestMapping("/employee")
public class EmployeeController {

    @GetMapping
    public String index() {
        return "view_employee";
    }
}
```



