# Hello World

Sudah menjadi hal yang umum ketika belajar suatu bahasa pemrograman adalah bagaimana membuat code yang sangat sederhana, salah satunya adalah "Hello World".

## Spring MVC

Kerangka kerja Spring Web MVC menyediakan arsitektur Model-View-Controller \(MVC\) dan komponen-komponen siap yang dapat digunakan untuk mengembangkan aplikasi web yang fleksibel. Pola MVC menghasilkan pemisahan berbagai aspek aplikasi \(logika input, logika bisnis, dan logika UI\).

* Model merangkum data aplikasi dan secara umum akan terdiri dari POJO.
* View bertanggung jawab untuk memberikan data model dan secara umum menghasilkan output HTML yang dapat ditafsirkan oleh browser.

* Controller bertanggung jawab untuk memproses permintaan pengguna dan membangun model yang sesuai dan meneruskannya ke tampilan untuk rendering.

## Controller

### Membuat Package Controller

![](/assets/wizard-controller-package)

### Membuat Controller Class

```java
package com.uinjakarta.smartweb.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
@RequestMapping("/hello")
public class HelloWorld {

    @GetMapping
    @ResponseBody
    public String index() {
        return "hello world java springboot";
    }
}
```

### Jalankan di Browser

* buka browser dan ketik url: [http://localhost:8080](http://localhost:8080/hello)

* output :  "hello world java springboot"



