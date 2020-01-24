## Secure Application with Spring Security

* basic security
* configure basic authentication
* configure basic authorization
* jdbc authentication
  * configure auth
* * create schema and data
* custome form login

## Basic Security

```
//add username password @application.properties

spring.security.user.name=arrizaqu
spring.security.user.password=1234
```

## Configure Basic Authentication \(\*AuthenticationManagerBuilder\)

```
@Configuration
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.inMemoryAuthentication()
                .withUser("arrizaqu").password("cangkir").roles("user")
                .and()
                .withUser("sofia").password("tanisha").roles("admin");
    }

    @Bean
    public PasswordEncoder getPasswordEncoder(){
        return NoOpPasswordEncoder.getInstance();
    }
}

//tambahan menggunakan ini pengganti AuthenticationManagerBuild dengan UserDetailService
@Bean
public UserDetailsService users() {
    UserDetails user = User.builder()
        .username("user")
        .password("{bcrypt}$2a$10$GRLdNijSQMUvl/au9ofL.eDwmoohzzS7.rmNSJZ.0FxO/BTk76klW")
        .roles("USER")
        .build();
    UserDetails admin = User.builder()
        .username("admin")
        .password("{bcrypt}$2a$10$GRLdNijSQMUvl/au9ofL.eDwmoohzzS7.rmNSJZ.0FxO/BTk76klW")
        .roles("USER", "ADMIN")
        .build();
    return new InMemoryUserDetailsManager(user, admin);
}
```

## Configure Basic Authorization \(HttpSecurity\)

```
@Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
                .antMatchers("/rest/admin").hasRole("admin")
                .antMatchers("/rest/user").hasRole("user")
                .antMatchers("/").permitAll()
                .and()
                .formLogin();
    }
```

## Jdbc Authentication

### Configure Auth

```

```

### Create schema and data

```

```





