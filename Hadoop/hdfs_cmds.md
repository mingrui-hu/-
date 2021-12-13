#### copy to local

-   https://stackoverflow.com/questions/17837871/how-to-copy-file-from-hdfs-to-the-local-file-system

```shell
bin/hadoop fs -get /hdfs/source/path /localfs/destination/path
bin/hadoop fs -copyToLocal /hdfs/source/path /localfs/destination/path
```

-   https://community.cloudera.com/t5/Support-Questions/How-do-you-force-the-number-of-reducers-in-a-map-reduce-job/td-p/104635

-   merge multiple files(e.g.)

    ```shell
    hdfs dfs -cat /path/to/files/* > /local/fs/path
    ```

    