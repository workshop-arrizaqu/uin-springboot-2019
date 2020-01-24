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
@Override
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
auth.jdbcAuthentication().dataSource(dataSource)
        .usersByUsernameQuery("select username, password, enabled"
        + " from users where username=?")
        .authoritiesByUsernameQuery("select username, authority "
                + "from authorities where username=?")
        .passwordEncoder(new BCryptPasswordEncoder());
}
```

### Create schema and data

```
//create file schema.sql *src/main/resources
drop table users cascade;
drop table authorities;

create table users(
  username varchar(50) not null primary key,
  password varchar(100) not null,
  enabled boolean not null
);

create table authorities (
	username varchar(50) not null,
	authority varchar(50) not null,
constraint fk_authorities_users foreign key(username) references users(username)
);

create unique index ix_auth_username on authorities (username,authority);

//create file data.sql *src/main/resources => password : admin@123

insert into users(username,password,enabled)
values('admin','$2a$10$hbxecwitQQ.dDT4JOFzQAulNySFwEpaFLw38jda6Td.Y/cOiRzDFu',true);
insert into authorities(username,authority)
values('admin','ROLE_ADMIN'); 
```



