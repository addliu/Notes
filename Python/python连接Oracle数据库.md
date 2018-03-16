## Python连接Oracle数据库

使用的Python库：`cx_Oracle`

基本代码如下：

```python
import cx_Oracle as oracle
# 连接数据库
db = oracle.connect('username', 'password', '[host]ip:port/SERVICE_NAME')
# 获取游标
cursor = db.cursor()
# 语句
sql = 'SQL statement'
# 执行语句
cursor.execute(sql)
# 如果是查询语句，则如下可以获得查询结果
result = cursor.fetchall()
# 遍历result
for row in result:
    print(row)
```

