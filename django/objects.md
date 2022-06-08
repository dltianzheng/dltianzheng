模型的objects是通过Manager添加

```
class model(Model):
	objects = Manager()
```

可以重写objects或者添加另外的objects

[(24条消息) Django Manager_安然_随心的博客-CSDN博客](https://blog.csdn.net/youyou1543724847/article/details/88193356)

感觉可以通过objects重写实现pg schema问题

