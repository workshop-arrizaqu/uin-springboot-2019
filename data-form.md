# Data Form

Data form biasanya digunakan untuk memasukkan data pada aplikasi, biasa dikenal INSERT atau SAVE Data, pada prosesnya java menginginkan adalah setiap form data yang ada harus berkesuaian dengan model yang sudah dibuatkan sebelumnya, sebagai berikut :

## HTML Form

```java
<!-- Page Content -->
  <th:block th:replace="fragments/template :: app-nav" ></th:block>
  <div class="container">
    <div class="row">
      <div class="col-lg-12 text-center">
        <h1 class="mt-5">Hello, Java Spring Boot</h1>
        <p class="lead">Table : Employee</p>
            <form action="#" th:action="@{/employee/save}" th:object="${employee}"method="POST">
                Name : <input type="text" th:field="*{name}"/><br/>
                Email : <input type="text" th:field="*{email}"/><br/>
                <input type="submit" value="Save Data" />
            </form>
      </div>
    </div>
  </div>
```

## Membuat Repository Data

## Membuat Service Layer sebagai Service





## Form Validation



