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



