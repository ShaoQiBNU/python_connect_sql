python连接mysql并做增删改查等操作
==============================

# 一. select操作

> Python查询Mysql使用 fetchone() 方法获取单条数据, 使用fetchall() 方法获取多条数据。
fetchone(): 该方法获取下一个查询结果集，结果集是一个对象
fetchall(): 接收全部的返回结果行.
rowcount: 这是一个只读属性，并返回执行execute()方法后影响的行数。

```python
import pymysql

# 打开数据库连接（ip/数据库用户名/登录密码/数据库名）
db = pymysql.connect("localhost","testuser","test123","TESTDB" )

# 使用 cursor() 方法创建一个游标对象 cursor
cursor = db.cursor()
 
# sql order by rand()作用是随机排序
sql="select * from testtable order by rand()"

# 使用 execute()  方法执行 SQL 查询 
cursor.execute(sql)
 
# 使用 fetchone() 方法获取单条数据.
data = cursor.fetchall()

# 遍历数据集查看结果
for row in data:
    id=row[0]
    first_name=row[1]
    last_name=row[2]
    insert_time=row[3]
    update_time=row[4]
    print(id,first_name,last_name,insert_time,update_time)


# 关闭游标连接
cursor.close()

# 关闭数据库连接
db.close()
```

# 二. insert操作

```python
import pymysql
 
# 打开数据库连接（ip/数据库用户名/登录密码/数据库名）
db = pymysql.connect("localhost","testuser","test123","TESTDB" )
 
# 使用cursor()方法获取操作游标 
cursor = db.cursor()
 
# SQL 插入语句
sql = "INSERT INTO EMPLOYEE(FIRST_NAME, \
       LAST_NAME, AGE, SEX, INCOME) \
       VALUES ('%s', '%s', '%d', '%c', '%d' )" % \
       ('Mac', 'Mohan', 20, 'M', 2000)
try:
   # 执行sql语句
   cursor.execute(sql)
   
   # 提交到数据库执行
   db.commit()
except:
   # 发生错误时回滚
   db.rollback()
 
# 关闭游标连接
cursor.close()

# 关闭数据库连接
db.close()
```

# 三. update操作

```python
import pymysql
 
# 打开数据库连接（ip/数据库用户名/登录密码/数据库名）
db = pymysql.connect("localhost","testuser","test123","TESTDB" )
 
# 使用cursor()方法获取操作游标 
cursor = db.cursor()
 
# SQL 更新语句
sql = "UPDATE EMPLOYEE SET AGE = AGE + 1 WHERE SEX = '%c'" % ('M')

try:
   # 执行SQL语句
   cursor.execute(sql)
   
   # 提交到数据库执行
   db.commit()
   
except:
   # 发生错误时回滚
   db.rollback()

# 关闭游标连接
cursor.close()

# 关闭数据库连接
db.close()
```

# 四. delete操作

```python
import pymysql
 
# 打开数据库连接
db = pymysql.connect("localhost","testuser","test123","TESTDB" )
 
# 使用cursor()方法获取操作游标 
cursor = db.cursor()
 
# SQL 删除语句
sql = "DELETE FROM EMPLOYEE WHERE AGE > '%d'" % (20)

try:
   # 执行SQL语句
   cursor.execute(sql)
   
   # 提交修改
   db.commit()
   
except:
   # 发生错误时回滚
   db.rollback()
 
# 关闭游标连接
cursor.close()

# 关闭连接
db.close()

```

