
# Java-JDBC返回查询结果集条数
在建立`Statement`对象是加入参数
`(ResutlSet.TYPE_SCROLL_INSENSITIVE,ResultSet.CONCUR_UPDATABLE)`  
`建立连接省略...`
```
stmt =
conn.creatStatement(ResutlSet.TYPE_SCROLL_INSENSITIVE,ResultSet.CONCUR_UPDATABLE)  
rs = stmt.executeQuery(sql);
rs.last();
```  
此时可以使用`rs.getRow();`获取结果集的条数。
