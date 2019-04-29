# Datatables plugins

Beberapa library yang tidak asing untuk kalangan web developer adalah salah satunya Datatables, beberapa kebutuhan yang cukup membantu pada library adalah :

1. Default searching
2. Pagination
3. Sorting
4. Custome Button dan Modal

berikut ini adalah bagaimana mengimplementasikan datatables pada springboot.

## HTML

```html
<table id="table_id" class="display">
<thead>
    <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Email</th>
    </tr>
</thead>
<tbody></tbody>
</table>
```

## Javascript

```js
<script type="text/javascript" th:inline="javascript">
$(document).ready(function() {
    var webRoot = /*[[@{/}]]*/;
    $('#table_id').DataTable({
        "processing": true,
        "serverSide": true,
        "ajax": {
            url : "department/findall",
            type: 'GET',
            data : function(d){

                var oTable = $('#table_id').DataTable();
                var info = oTable.page.info();
                var selectedColumn = oTable;

                /*-------- paging number and showing current data ----------- */
                d.page = info.page; // get current page
                d.size = d.length; // show entries

                /*--------- Sorting Data ------------*/
                //get index selected order
                var idxColumn = oTable.order()[0][0];
                //get type selected order
                var idxType = oTable.order()[0][1];
                d.sort = d.columns[idxColumn].data+ ',' + idxType;

                /*--------- search data ------------------- */
                d.search = d.search.value;
            }
        },
         "columns": [
                { "data": "id" },
                { "data": "departmentName" },
                { "data": "departmentEmail" }
            ]
    });

}); 
</script>
```

## Datatable POJO

```java
import java.util.List;

import org.springframework.stereotype.Component;

@Component
public class DataTablesPlugins {

    private int totalPages;
    private List<Department> data;
    private long recordsFiltered;

    public int getTotalPages() {
        return totalPages;
    }
    public void setTotalPages(int totalPages) {
        this.totalPages = totalPages;
    }
    public List<Department> getData() {
        return data;
    }
    public void setData(List<Department> data) {
        this.data = data;
    }
    public long getRecordsFiltered() {
        return recordsFiltered;
    }
    public void setRecordsFiltered(long recordsFiltered) {
        this.recordsFiltered = recordsFiltered;
    }

}
```

## Controller

```java
@GetMapping("/findall")
@ResponseBody
public DataTablesPlugins findAll(@RequestParam(value="search", defaultValue="", required=false) String search, Pageable pageable){
    Page page = deptServ.findAllBySearchInput(search, pageable);
    dataTables.setData(page.getContent());
    dataTables.setTotalPages(page.getTotalPages());
    dataTables.setRecordsFiltered(page.getTotalElements());

    return dataTables;
}
```

## Referensi

1. [https://datatables.net/manual/ajax](https://datatables.net/manual/ajax)



