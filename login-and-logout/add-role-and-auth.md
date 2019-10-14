# Adding Role

## Add Relation RoleApp and userApp

### \* UserApp

```java
import java.util.List;

import javax.persistence.CascadeType;
import javax.persistence.Entity;
import javax.persistence.FetchType;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.JoinColumn;
import javax.persistence.JoinTable;
import javax.persistence.ManyToMany;
import javax.persistence.Table;

import org.hibernate.annotations.Cascade;

@Entity
@Table(name="USER_APP")
public class UserApp {

    @Id
    @GeneratedValue(strategy=GenerationType.AUTO)
    private int id;
    private String username;
    private String password;
    @ManyToMany(fetch=FetchType.LAZY)
    @JoinTable(name="USER_ROLES_APP", joinColumns= {
            @JoinColumn(name="user_id")
    }, inverseJoinColumns= {
            @JoinColumn(name="role_id")
    })
    private List<RoleApp> roles;

    public List<RoleApp> getRoles() {
        return roles;
    }
    public void setRoles(List<RoleApp> roles) {
        this.roles = roles;
    }
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

### \* RoleApp

```java
import java.util.List;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.ManyToMany;
import javax.persistence.Table;

@Entity
@Table(name="ROLE_APP")
public class RoleApp {
    @Id
    @GeneratedValue(strategy=GenerationType.AUTO)
    private int id;
    private String name;
    private String note;
    @ManyToMany
    private List<UserApp> users;
    public int getId() {
        return id;
    }
    public void setId(int id) {
        this.id = id;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getNote() {
        return note;
    }
    public void setNote(String note) {
        this.note = note;
    }

}
```

### RoleApp Repository

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface RoleAppRepo extends JpaRepository<RoleApp, Integer>{

}
```

## Modify and Add Method JOIN Relation Object

```java
public interface UserAppRepo extends JpaRepository<UserApp, Integer> {

    public UserApp findUserAppByUsername(String username);
    @Query("select rl from UserApp as ua join ua.roles as rl where ua = ?1")
    public List<RoleApp> findRolesByUserApp(UserApp userApp);

}
```

## Modify UserApp Principal

```java
@Override
public Collection<? extends GrantedAuthority> getAuthorities() {
    // TODO Auto-generated method stub
     //return Collections.singletonList(new SimpleGrantedAuthority("admin"));
    final List<GrantedAuthority> authorities = new ArrayList<GrantedAuthority>();
    for (final RoleApp role : this.userApp.getRoles()) {
        authorities.add(new SimpleGrantedAuthority(role.getName()));
    }
    return authorities;
}
```

## Modify MyUserDetailsService

```java
List<RoleApp> myRoles = this.userAppRepo.findRolesByUserApp(user); 
user.setRoles(myRoles);
```

modify MyUserDetailsService to load **findRoleByUserApp** because FaceType is Lazy, and set roles before send to MyUserAppPricipal

```java
@Override
public UserDetails loadUserByUsername(String username) {
    // TODO Auto-generated method stub
    UserApp user = userAppRepo.findUserAppByUsername(username);
    List<RoleApp> myRoles = this.userAppRepo.findRolesByUserApp(user);
    user.setRoles(myRoles);

    if (user == null) {
            throw new UsernameNotFoundException(username);
    }

    return new MyUserAppPrincipal(user);
}
```

## Change HasRole to HasAuthentication

```java
@Override
protected void configure(HttpSecurity http) throws Exception {
    // TODO Auto-generated method stub
    //super.configure(http);
    http.authorizeRequests()
        .antMatchers("/hello").permitAll()
        .antMatchers("/department/**").hasAuthority("admin")
        .antMatchers("/employee/**").hasAuthority("user")
        .anyRequest()
        .authenticated()
        .and()
        .formLogin();
}
```

## Saving Data Login

### create Data Login Service

```java
import javax.transaction.Transactional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.uinjakarta.smartweb.security.RoleAppRepo;
import com.uinjakarta.smartweb.security.UserApp;
import com.uinjakarta.smartweb.security.UserAppRepo;

@Transactional
@Service
public class DataLoginService {

    @Autowired
    private UserAppRepo userAppRepo;
    @Autowired
    private RoleAppRepo roleAppRepo;

    public void saveUser(UserApp user) {
        //save user
        userAppRepo.save(user);
        //save role
        roleAppRepo.saveAll(user.getRoles());
    }
}
```

### InitDb

```java
public void initUser() {
    List<RoleApp> roles = new ArrayList<RoleApp>();
    RoleApp roleApp = new RoleApp();
    RoleApp roleApp2 = new RoleApp();
    RoleApp roleApp3 = new RoleApp();
    roles.add(roleApp);
    roles.add(roleApp2);
    roles.add(roleApp3);

    roleApp.setName("admin");
    roleApp2.setName("user");
    roleApp3.setName("operator");

    UserApp user = new UserApp();
    user.setUsername("arrizaqu");
    user.setPassword(new BCryptPasswordEncoder().encode("1234"));
    user.setRoles(roles);
    //save to db
    dataLoginServ.saveUser(user);
}
```

Reference

1. [https://stackoverflow.com/questions/31704593/spring-security-authorize-requests-value-from-database](https://stackoverflow.com/questions/31704593/spring-security-authorize-requests-value-from-database)

2. [https://github.com/eugenp/tutorials/blob/master/spring-security-mvc-boot/src/main/java/org/baeldung/custom/security/MyUserPrincipal.java](https://github.com/eugenp/tutorials/blob/master/spring-security-mvc-boot/src/main/java/org/baeldung/custom/security/MyUserPrincipal.java)

3. [https://stackoverflow.com/questions/9910252/how-to-reload-authorities-on-user-update-with-spring-security](https://stackoverflow.com/questions/9910252/how-to-reload-authorities-on-user-update-with-spring-security)



