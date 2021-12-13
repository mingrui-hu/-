-   pandas.read_sql 中的sql语句不能加分号

-   https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-sql

    ### to_sql

    -   about schema:https://stackoverflow.com/questions/30994707/specifying-the-schema-in-pandas-to-sql
    -   如果不需要index， 注意设置 `index=False, index_label=None`， default=True

