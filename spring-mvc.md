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

## HTML sebagai View



