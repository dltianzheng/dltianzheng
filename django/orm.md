**raw**

```
raw_queryset = query.raw("sql")
raw_queryset 没有 values 这些方法

```



**extra**

```，
queryset = query.extra()
queryset是Queryset对象，可以执行filter方法
```



```python

ModelB.objects.filter(id__in=RawSQL(
    'SELECT unnest(a.pk_values) FROM app_modela a WHERE a.id = %s',
    [index_id]
)) #b


ModelB.objects.extra(
    tables=['foo_modela'],
    where=[
        '"app_modelb"."id" = ANY("app_modela"."pk_values")',
        '"app_modela"."id" = %s',
    ],
    params=[index_id],
)

```

