### L12 - p108

-   引用完整性

-   性能受操作类型、所使用的的DBMS、表中数据量、是否存在索引等条件影响

-   等值联结 == 内联结

    ```sql
    # 使用where 字句建立联结
    select vend_name, prod_name, prod_price 
    from Vendors, Products
    where Vendors.vend_id = Products.vend_id
    ```

    -   等价`INNER JOIN`语法

    ```sql
    select vend_name, prod_name, prod_price 
    from Vendors
    inner join Products on Vendors.vend_id = Products.vend_id
    ```

    

    -   联结多个表

    ```sql
    select prod_name, vend_name, prod_price, quantity 
    from OrderItems, Products, Vendors
    where Products.vend_id = Vendors.vend_id
    and OrderItems.prod_id = Products.prod_id
    
    -- 过滤条件
    and order_num = 2007; 
    ```

    

### L13 - p120

