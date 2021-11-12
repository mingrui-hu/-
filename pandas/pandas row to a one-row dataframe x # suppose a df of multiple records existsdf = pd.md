1.  pandas row to a one-row dataframe

    ​	

    ```python
    # suppose a df of multiple records exists
    df = pd.DataFrame()
     
    # select a row
    r = df.loc[df['col1'] == col1_value, :]
    # if printed, r is a pd.Series of len(#columns) in df
    # to convert it to a one-row dataframe in order to concatenate with other df
    r_t = pd.DataFrame(r).transpose()
    new_df = pd.concat([r_t, r_t2, ....])
    ```

2.  Dataframe row repeat

    ```python
    pd.concat([df]*n, ignore_index=True)
    ```

3.  Concatenate two data frame: **Align Index!!!**

    ```python
    pd.concat(df1.reset_index(drop=True), df2.reset_index(drop=True))
    ```

    

4.  Write to multiple excel sheets

    -   two packages need to be installed `xlwt` and `xlsxwriter`

    ```python
    writer = pd.ExcelWriter("dataframe.xlsx", engine='xlsxwriter')
    
    df.to_excel(writer, sheet_name="Sheet1")
    df2.to_excel(writer, sheet_name="Sheet2")
    
    writer.save()
    writer.close()
    ```

5.  Selecting those rows whose **column value is present in the list** using `isin()` method of the dataframe.

    ```python
    rslt_df = df[df['col1'].isin(col_list)]
    
    # is not in 
    rslt_df = df.loc[~df['col1'].isin(col_list)]
    
    ```

6.  Subgroup count & percent

    ```python
    subgroup_count = df.groupby("group_col")["some_index"].count()
    subgroup_count = subgroup_count / subgroup_count.sum()
    ```

    

    