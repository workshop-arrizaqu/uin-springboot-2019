## Authentication From Database

for this tutorial, using **UserDetailsService,**

1. Create User POJO
2. Create Repository
3. Create Class Implementation UserDetailService
4. Create User Principal
5. Implementation of Spring Configuration

## User POJO

```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

@Entity
@Table(name="USER_APP")
public class UserApp {

    @Id
    @GeneratedValue(strategy=GenerationType.AUTO)
    private int id;
    private String username;
    private String password;
    public int getId() {
        return id;
    }
    public void setId(int id) {
        this.id = id;
    }
    public String getUsername() {
        return username;
    }
    public void setUsername(String username) {
        this.username = username;
    }
    public String getPassword() {
        return password;
    }
    public void setPassword(String password) {
        this.password = password;
    }
}
```

## User Repository

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserAppRepo extends JpaRepository<UserApp, Integer> {

    public UserApp findUserAppByUsername(String username);

}
```

## Create UserDetailsService Class

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.stereotype.Service;

@Service
public class MyUserDetailService implements UserDetailsService {

    @Autowired
    private UserAppRepo userAppRepo;

    @Override
    public UserDetails loadUserByUsername(String username) {
        // TODO Auto-generated method stub
        UserApp user = userAppRepo.findUserAppByUsername(username);

        if (user == null) {
            throw new UsernameNotFoundException(username);
        }

        return new MyUserAppPrincipal(user);
    }

}
```

## User Principal

```java
import java.util.Collection;
import java.util.Collections;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;

public class MyUserAppPrincipal implements UserDetails {

    private UserApp userApp;

    public MyUserAppPrincipal(UserApp userApp){
        this.userApp = userApp;
    }

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        // TODO Auto-generated method stub
        return Collections.singletonList(new SimpleGrantedAuthority("Admin"));
    }

    @Override
    public String getPassword() {
        // TODO Auto-generated method stub
        return this.userApp.getPassword();
    }

    @Override
    public String getUsername() {
        // TODO Auto-generated method stub
        return this.userApp.getUsername();
    }

    @Override
    public boolean isAccountNonExpired() {
        // TODO Auto-generated method stub
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        // TODO Auto-generated method stub
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        // TODO Auto-generated method stub
        return true;
    }

    @Override
    public boolean isEnabled() {
        // TODO Auto-generated method stub
        return true;
    }

    public UserApp getUserApp() {
        return userApp;
    }

    public void setUserApp(UserApp userApp) {
        this.userApp = userApp;
    }
}
```

## Spring Security Config

```java
@Override
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
    // TODO Auto-generated method stub
    auth.authenticationProvider(getAuthenticationProvider());
}

@Bean
public DaoAuthenticationProvider getAuthenticationProvider() {
    DaoAuthenticationProvider dap = new DaoAuthenticationProvider();
    dap.setUserDetailsService(myUserDetailService);
    dap.setPasswordEncoder(encoder());
    return dap;
}

@Bean
public PasswordEncoder encoder() {
    return new BCryptPasswordEncoder(11);
}
```

## Reference

1. [https://www.baeldung.com/spring-security-authentication-with-a-database](https://www.baeldung.com/spring-security-authentication-with-a-database)



