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

### Custome Username and Password

```java
@Autowired
public void globalConfig(AuthenticationManagerBuilder auth) throws Exception {
    auth.inMemoryAuthentication()
        //user 1
        .withUser("arrizaqu")
        .password("{noop}1234")
        .roles("admin")
            .and()
            //user 2
            .withUser("tanisha")
            .password("{noop}arrizaqu")
            .roles("admin","child");
}
```

## Add Role In

add role, add script antMatchers like bellow :

```java
.antMatchers("/department/**").hasRole("admin")
.antMatchers("/employee/**").hasRole("child")
```

will full script like :

```java
@Override
protected void configure(HttpSecurity http) throws Exception {
	// TODO Auto-generated method stub
	//super.configure(http);
	http.authorizeRequests()
		.antMatchers("/department/**").hasRole("admin")
		.antMatchers("/employee/**").hasRole("child")
		.antMatchers("/quiz").permitAll()
		.anyRequest()
		.authenticated()
		.and()
		.formLogin();
}
```

## Another case example

```java
/*
case example : 
http.authorizeRequests()
        .antMatchers("/high_level_url_A/sub_level_1").hasRole('USER')
        .antMatchers("/high_level_url_A/sub_level_2").hasRole('USER2')
        .somethingElse() // for /high_level_url_A/**
        .antMatchers("/high_level_url_A/**").authenticated()
        .antMatchers("/high_level_url_B/sub_level_1").permitAll()
        .antMatchers("/high_level_url_B/sub_level_2").hasRole('USER3')
        .somethingElse() // for /high_level_url_B/**
        .antMatchers("/high_level_url_B/**").authenticated()
        .anyRequest().permitAll()
*/
```

## Reference

1. [https://www.mkyong.com/spring-boot/spring-security-there-is-no-passwordencoder-mapped-for-the-id-null/](https://www.mkyong.com/spring-boot/spring-security-there-is-no-passwordencoder-mapped-for-the-id-null/)
2. [https://stackoverflow.com/questions/35890540/when-to-use-spring-securitys-antmatcher](https://stackoverflow.com/questions/35890540/when-to-use-spring-securitys-antmatcher)



