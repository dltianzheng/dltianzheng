```
当Django提供的Field无法满足我们的需求时，可以通过自定义Field来解决这个问题。
每个自定义的Field,都需要继承django.db.models.Field,

如果mysql有相应的字段，则直接设置db_field属性即可，如下文的SmallIntegerField字段。
如果mysql没有相应的字段，则需要重写父类的from_db_value方法，to_python方法，get_prep_value方法。如下文的PasswordFieldCustom字段。
db_field指明数据库列的类型
from_db_value方法返回从数据库中取出数据。
to_python方法把数据写入数据库
get_prep_value方法是与to_python方法共同使用，作用为将Python对象进行处理，确保数据库可以保存其对象。（如果不写这个方法，无法调用to_python,所以用to_python时一定要写get_prep_value)
```



```
django携带的field都无from_db_value,from_db_value是将从数据库转成python的方法
自携带的无因为从数据库取出的类型就是想要的类型
https://docs.djangoproject.com/en/1.8/ref/models/fields/#django.db.models.Field.from_db_value
```

