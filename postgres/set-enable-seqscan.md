When you have small dataset and want test your index (usally locally) postgres won't use it given amount data. With following pro tips you can tell postgres that use index

 ```SQL
 SET enable_seqscan TO off;
 ```
 
[More details](https://www.postgresql.org/docs/9.5/static/runtime-config-query.html)
