# Web Security For Login and Logout

## Create Username and Password

### Create Security Configuration

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
public class SecurityConfig extends WebSecurityConfigurerAdapter{

}
```

### Authenticated

Default username : user.

password generated from console.

```java
@Override
protected void configure(HttpSecurity http) throws Exception {
    // TODO Auto-generated method stub
    //super.configure(http);
    http.authorizeRequests()
        .anyRequest()
        .authenticated()
        .and()
        .loginForm();
}
```

### Handle Controller Route and Role

## Reference

1. [https://www.mkyong.com/spring-boot/spring-security-there-is-no-passwordencoder-mapped-for-the-id-null/](https://www.mkyong.com/spring-boot/spring-security-there-is-no-passwordencoder-mapped-for-the-id-null/)



