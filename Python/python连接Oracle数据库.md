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

>注意：如果没有按照完整版的Oracle数据库，连接数据库时会报错找不到`oci.dll`，此时需要到Oracle客户端`oci.dll`所在的文件夹运行`python`脚本，这样比较麻烦，因为不能保证一直到那个目录执行执行脚本，所以我们可以将需要被调用的dll文件加载到`python`运行环境中,示例代码如下：
>
>```python
>import ctypes
># 加载Oracle oci.dll文件
>ctypes.windll.LoadLibrary('d:/instantclient_12_2/oci.dll')
>```

