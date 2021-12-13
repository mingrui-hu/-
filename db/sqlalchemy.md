

## Documents

https://docs.sqlalchemy.org/en/14/intro.html

## 1.4/2.0 tutorials

https://docs.sqlalchemy.org/en/14/tutorial/index.html

### Core & ORM

>   **SQLAlchemy ORM** builds upon the Core to provide optional **object relational mapping** capabilities. The ORM provides an additional configuration layer allowing user-defined Python classes to be **mapped** to database tables and other constructs, as well as an object persistence mechanism known as the **Session**. It then extends the Core-level SQL Expression Language to allow SQL queries to be composed and invoked in terms of user-defined objects.

### metadata

https://docs.sqlalchemy.org/en/14/tutorial/metadata.html

### reflection

https://docs.sqlalchemy.org/en/14/core/reflection.html

### conjunction

https://docs.sqlalchemy.org/en/14/core/operators.html#using-conjunctions-and-negations

### Selectables, Tables

https://docs.sqlalchemy.org/en/14/core/operators.html#using-conjunctions-and-negations

### engine configuration

https://docs.sqlalchemy.org/en/14/core/engines.html#postgresql

-   [working with engines & connections](https://docs.sqlalchemy.org/en/14/core/connections.html#using-transactions)

### Cursor Result/ ResultProxy

-   https://docs.sqlalchemy.org/en/14/core/connections.html#sqlalchemy.engine.CursorResult

    ```python
    method sqlalchemy.engine.CursorResult.fetchmany(size=None)
    ```

-   related

    ```python
    method sqlalchemy.engine.Result.partitions(size=None)
    ```

### ORM basic use

-   https://docs.sqlalchemy.org/en/13/orm/extensions/declarative/basic_use.html

### refs

-   [jupyter notebook basic operations](https://towardsdatascience.com/sqlalchemy-python-tutorial-79a577141a91)

-   [Use SQLAlchemy ORMs to Access Hive Data in Python](https://www.cdata.com/kb/tech/hive-python-sqlalchemy.rst)

-   [sqlalchemy 读写分离简单封装](https://blog.csdn.net/qq_17612199/article/details/75945102)

-   pysheet https://www.pythonsheets.com/notes/python-sqlalchemy.html

### connection execution options

https://www.kite.com/python/docs/sqlalchemy.engine.Connection.execution_options