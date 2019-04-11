# Hello World

Sudah menjadi hal yang umum ketika belajar suatu bahasa pemrograman adalah bagaimana membuat code yang sangat sederhana, salah satunya adalah "Hello World".

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



