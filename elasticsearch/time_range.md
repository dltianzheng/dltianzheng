```json
{"query":{"bool":{"must":[{"range":{"start_time":{"gte":"now+8h-1h","lte":"now+8h"}}},{"term":{"id":"6db9031e2b682f5116a7c64a29ffa8ed"}}],"must_not":[],"should":[]}},"from":0,"size":10,"sort":[],"aggs":{}}
时间查询问题
当前时间为now,不用加8h

```

https://www.cnblogs.com/shoufeng/p/11266136.html

