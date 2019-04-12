# Spring MVC

Kerangka kerja Spring Web MVC menyediakan arsitektur Model-View-Controller \(MVC\) dan komponen-komponen siap yang dapat digunakan untuk mengembangkan aplikasi web yang fleksibel. Pola MVC menghasilkan pemisahan berbagai aspek aplikasi \(logika input, logika bisnis, dan logika UI\).

* Model merangkum data aplikasi dan secara umum akan terdiri dari POJO.
* View bertanggung jawab untuk memberikan data model dan secara umum menghasilkan output HTML yang dapat ditafsirkan oleh browser.

* Controller bertanggung jawab untuk memproses permintaan pengguna dan membangun model yang sesuai dan meneruskannya ke tampilan untuk rendering.

## Simple CRUD \(Create Read Update Delete\)

### Table : Employee

![](/assets/table-employee)

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

## POJO sebagai Model

## HTML sebagai View



