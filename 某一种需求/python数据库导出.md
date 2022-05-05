# 数据库备份

```python
#coding=utf-8
from isop_for_renshoucai.drf import pg_client
from psycopg2 import sql
# query = sql.SQL("select {0} from {1}").format(
# sql.SQL(', ').join([sql.Identifier('foo'), sql.Identifier('bar')]),
# sql.Identifier('table'))

con,cur = pg_client.getConnect()
# print(query.as_string(con)
sele = "select id, name, type, content, create_at, update_at from t_davinci_visual_resource where id in %s"

ids = ("819f6d16-23bf-42ff-9a5c-6ef430a7c454","60cc53f6-0b38-408b-a924-095b715a85e6")
# print(cur.mogrify(sele,(ids,)))
# ids = sql.SQL(', ').join([sql.Literal(i) for i in ids]).as_string(con)
# # query = sql.SQL(sele).format(sql.Identifier(ids,))

# # print(query.as_string(con))


# # print("select id, name, type, content, create_at, update_at from t_davinci_visual_resource where id in %s"%ids)

import os
# print(__file__)
os.chdir(os.path.dirname(__file__)) # 切换到当前执行文件文件夹


with open("./data.sql", "w") as f:
    # cur.copy_expert
    f.write("COPY t_davinci_general_template from STDIN;\n")
    cur.copy_expert("COPY ({0}) TO STDOUT".format(cur.mogrify(sele,(ids,))), f) # 支持在文件末尾append操作
    f.write(cur.mogrify("\.\nupdate t_davinci_general_template set type='internal' where id in %s;\n",(ids,)),)
    f.write("COPY t_davinci_visual_resource_img from STDIN;\n")
    cur.copy_expert("COPY t_davinci_visual_resource_img to stdout", f)
    f.write('\.\n')
    # f.truncate(0)
    # f.seek(0)
    # f.write("COPY t_davinci_visual_resource from STDIN;\n") # seek后在某一位置不支持append操作

"""

COPY t_davinci_visual_resource from STDIN;

csv 数据
\. <-以此为结束,后续可加sql 

可以执行导致数据
"""
#https://www.psycopg.org/docs/cursor.html
#https://blog.csdn.net/junbujianwpl/article/details/73194846
#https://groups.google.com/g/python-cn/c/QB3sgLA7IBk *没太看懂 文件seek*
#https://www.postgresql.org/docs/current/sql-copy.html  
#https://www.psycopg.org/docs/sql.html 生成sql
#https://stackoverflow.com/questions/5243596/python-sql-query-string-formatting
#https://stackoverflow.com/questions/1563967/generate-sql-statements-with-python
#https://www.psycopg.org/docs/usage.html#values-containing-backslashes-and-like
```

