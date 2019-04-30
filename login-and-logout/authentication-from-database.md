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

```

```



