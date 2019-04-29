## Searching Data

## Modify Repository @Query

```java
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;

import com.uinjakarta.smartweb.model.Department;

public interface DepartmentRepo extends JpaRepository<Department, Integer> {

	@Query("select dept from Department dept where dept.departmentName like %?1%")
	public Page findAllBySearchInput(String deptName, Pageable pageable);
}
```

## Modify Controller Passing Param

```java
@GetMapping("/findall")
@ResponseBody
public DataTablesPlugins findAll(@RequestParam(value="deptName", required=false) String deptName, Pageable pageable){
    Page page = deptServ.findAllBySearchInput(deptName, pageable);
    dataTables.setData(page.getContent());
    dataTables.setTotalPages(page.getTotalPages());
    dataTables.setRecordsFiltered(page.getTotalElements());

    return dataTables;
}
```



