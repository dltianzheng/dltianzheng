# get

## 在model中定义方法及调用

```ipython

In [2]: tvm_manager_models.ProvincialOperator().get_label('1213')
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-2-5f20835242ef> in <module>()
----> 1 tvm_manager_models.ProvincialOperator().get_label('1213')

/home/tz/ISOP/apps/tvm_manager/core/api/v1/models/provincial_operator.py in get_label(self, id)
     20     def get_label(self,id):
     21         try:
---> 22             value = self.objects.get(id=id).value
     23         except ProvincialOperator.DoesNotExist:
     24             value = '未知运营商'

/home/master/python-2.7.10/lib/python2.7/site-packages/django/db/models/manager.pyc in __get__(self, instance, type)
    250     def __get__(self, instance, type=None):
    251         if instance is not None:
--> 252             raise AttributeError("Manager isn't accessible via %s instances" % type.__name__)
    253         return self.manager
    254 

AttributeError: Manager isn't accessible via ProvincialOperator instances

```

