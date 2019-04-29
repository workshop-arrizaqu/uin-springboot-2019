## Searching Data

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



