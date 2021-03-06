# Quiz Logika

## Guidance Quiz

> **Menghasilkan bilangan Fibonachi dengan inputan N**

* ### Function Fibonachi

  ```java
  public int[] getFibonachi(int n) {
      int[] data = new int[n];
      data[0] = 1;
      data[1] = 1;
      for(int i = 2; i < n; i++) {
          data[i] = data[i - 1] + data[i - 2];
      }

      return data;
  }
  ```
* ### Controller

  ```java
  package com.uinjakarta.smartweb.controller;

  import java.io.ObjectInputStream.GetField;
  import java.util.Arrays;

  import org.springframework.stereotype.Controller;
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.RequestParam;
  import org.springframework.web.bind.annotation.ResponseBody;

  @Controller
  @RequestMapping("/quiz")
  public class Quiz {

      @GetMapping
      @ResponseBody
      public String index(@RequestParam("n") int n) {
          int[] dataFib = this.getFibonachi(n);
          String hasil = Arrays.toString(dataFib);
          return hasil;
      }

      public int[] getFibonachi(int n) {
          int[] data = new int[n];
          data[0] = 1;
          data[1] = 1;
          for(int i = 2; i < n; i++) {
              data[i] = data[i - 1] + data[i - 2];
          }

          return data;
      }

  }
  ```

## Quiz

> **Buatlah hasil output 2 digit menggunakan format  Array dengan aturan sebagai berikut : **
>
> **Digit 1 -&gt; menuntukkan Panjang suatu Array yang dihasilkan dari Bilangan Fibonachi Quiz 1**
>
> **Digit 2 -&gt; menunjukkan Total Jumlah  jika hasil Quiz 1 dijumlahkan. **
>
> ```
> Contoh : 1
>     * input : 3 
>     * Fibonachi : [1, 1, 2]
>     * hasil : [3, 4]
>     
> Contoh : 2 
>     * input : 5
>     * Fibonachi : [1, 1, 2, 3, 5]
>     * hasil : [5, 12]
> ```

### Lengkapi penyelesain berikut ini :

```java
package com.uinjakarta.smartweb.controller;

import java.io.ObjectInputStream.GetField;
import java.util.Arrays;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
@RequestMapping("/quiz")
public class Quiz {

    @GetMapping
    @ResponseBody
    public String index(@RequestParam("n") int n) {
        int[] dataFib = this.getFibonachi(n);
        int[] dataMax = this.getMaxValues(dataFib);
        String hasil = Arrays.toString(dataMax);

        return hasil;
    }

    public int[] getFibonachi(int n) {
        int[] data = new int[n];
        data[0] = 1;
        data[1] = 1;
        for(int i = 2; i < n; i++) {
            data[i] = data[i - 1] + data[i - 2];
        }

        return data;
    }

    public int[] getMaxValues(int[] dataFib) {
        //complete your code here !!
    }

}
```



