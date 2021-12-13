-   db2 `EXPORT` https://www.ibm.com/docs/en/db2/11.1?topic=commands-export

-   导出*外表* to csv in hive

    -   ```SQL
        -- to csv, single file
        set map.reduce.tasks=1;
        
        insert overwrite directory ${hdoop_fs_path/file_name.csv} 
        row format delimited fields terminated by ',' 
        select * from ${table name}
        distribute by 8;
        ```

-    导入外表

    -   从hadoop fs

        ```sql
        insert into ${table_name} from ${hdoop_fs_path/file_name.csv} 
        ```

    -   local fs

        ```sql
        load data
        ```

        

-   sparkSQL `distribute by` clause

    https://spark.apache.org/docs/latest/sql-ref-syntax-qry-select-distribute-by.html