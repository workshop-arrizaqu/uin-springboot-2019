Membuat Web Project

## Spring Boot Starter

Untuk pertama kali adalah tentunya membuat terlebih web project terlebih dahulu.sebagai berikut.

1. kunjungi [https://start.spring.io/](https://start.spring.io/)
2. Pilih Dependency standart diantaranya adalah :  
   1. JPA  
   2. MySQL  
   3. Thymeleaf

   ![](/assets/springinitializr.png)

3. Setelah itu ![](/assets/btn-generate-project.png) seperti terlihat button dibawah form dan **enter**

## Import File Project

Setelah melakukan generate Project dengan spring boot strater maka, selanjutknya adalah :

1. **Extract** file rar Generate Project ke dalam _**project workspace**_ anda.

2. Buka dan **import** file project yang telah di **extract** menggunakan IDE Eclipse / STS, yaitu : **File -&gt; Import **dan ketikan wizard "Maven" dan pilih Existing Maven Project, dan terakhir adalah cari file project yang telah di extract sebelumnya.

   ![](/assets/import-project.png)

## Menjalankan Program

Jalan program dengan banyak cara dalam hal ini secara cepat bisa dilakukan dengan menggunakan cara :

```
Klik kanan Project -> Pilih "RUN AS" -> pilih "Spring Boot App"
```

## ![](/assets/run-as)

## Koneksi Database

Dengan hadirnya dependency JPA, maka ketika project dijalankan maka biasanya akan error karena aplikasi harus memiliki koneksi dengan database, untuk kali ini menggunakan mysql, sebagai berikut:

1. buka file _**src -&gt; main -&gt; resources -&gt; application.properties**_ dan tuilis script sebagai berikut : 
   ```java
   # koneksi Database MySQL
   spring.jpa.hibernate.ddl-auto=validate
   spring.datasource.url=jdbc:mysql://localhost:3306/sb-uin-jakarta
   spring.datasource.username=root
   spring.datasource.password=
   ```
2. sfdsdf
3. fsdf



