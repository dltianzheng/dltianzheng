# Aggregation

* aggregate Generating aggregates over a QuerySet:为所有行统计聚合
* annotate Generating aggregates for each item in a QuerySet:为每一行单独获取聚合

## 问题

[extra and  annotate](https://stackoverflow.com/questions/28764381/django-querysets-using-annotate-after-extra)

## orm 与 sql

```python
from django.db.models import Avg,Max,Min
from django.db.models import Q
from django.
Book.objects.all().aggregate(Avg('price'))
aggregate 聚合和 svn sum 相关吧
"""
DEBUG 2022-07-02 15:10:13,733 utils 1528 13516 (0.068) SELECT AVG("queryset_book"."price") AS "price__avg" FROM "queryset_book"; args=()
"""
# Max price across all books.
Book.objects.all().aggregate(Max('price'))

pubs = Publisher.objects.annotate(num_books=Count('book'))
'''
DEBUG 2022-07-02 15:23:22,878 utils 1528 13516 (0.125) SELECT "queryset_publisher"."id", "queryset_publisher"."name", "queryset_publisher"."num_awards", COUNT("queryset_book"."id") AS "num_books" FROM "queryset_publisher" LEFT OUTER JOIN "queryset_book" ON ("queryset_publisher"."id" = "queryset_book"."publisher_id") GROUP BY "queryset_publisher"."id" LIMIT 21; args=()
'''
#Each publisher, with a separate count of books with a rating above and below 5
below_5 = Count('book', filter=Q(book__rating__lte=5))
above_5 = Count('book', filter=Q(book__rating__gt=5))

pubs = Publisher.objects.annotate(below_5=below_5).annotate(above_5=above_5)

"""
DEBUG 2022-07-02 15:33:33,608 utils 1528 13516 (0.170) SELECT "queryset_publisher"."id", "queryset_publisher"."name", "queryset_publisher"."num_awards", COUNT("queryset_book"."id") AS "below_5", COUNT("queryset_book"."id") AS "above_5" FROM "queryset_publisher" LEFT OUTER JOIN "queryset_book" ON ("queryset_publisher"."id" = "queryset_book"."publisher_id") GROUP BY "queryset_publisher"."id" LIMIT 21; args=()
"""
Book.objects.annotate(Avg('price'))
# django 可能不能通过jionon连接两个表
# 也有可能不能通过任意字段group by 
"""
DEBUG 2022-07-02 15:44:53,246 utils 1528 13516 (0.073) SELECT "queryset_book"."id", "queryset_book"."name", "queryset_book"."pages", "queryset_book"."price", "queryset_book"."rating", "queryset_book"."publisher_id", "queryset_book"."pubdate", AVG("queryset_book"."price") AS "price__avg" FROM "queryset_book" GROUP BY "queryset_book"."id" LIMIT 21; args=()
"""
# 通过values_list annotate达到了group 的目的
query.objects.filter(status='PRF').values_list( 'job_id', flat=True).order_by('job_id').annotate(count_status=Count('status')).filter(count_status__gt=1).distinct()
"""
DEBUG 2022-07-02 15:50:02,085 utils 1528 13516 (0.109) SELECT DISTINCT "queryset_query"."job_id", COUNT("queryset_query"."status") AS "count_status" FROM "queryset_query" WHERE "queryset_query"."status" = 'PRF' GROUP BY "queryset_query"."job_id" HAVING COUNT("queryset_query"."status") > 1 ORDER BY "queryset_query"."job_id" ASC LIMIT 21; args=('PRF', 1)

"""
#错误的查询
Book.objects.annotate(Count('authors'), Count('store'))
"""
DEBUG 2022-07-02 16:05:25,940 utils 1528 13516 (0.123) SELECT "queryset_book"."id", "queryset_book"."name", "queryset_book"."pages", "queryset_book"."price", "queryset_book"."rating", "queryset_book"."publisher_id", "queryset_book"."pubdate", COUNT("queryset_book_authors"."author_id") AS "authors__count", COUNT("queryset_store_books"."store_id") AS "store__count" FROM "queryset_book" LEFT OUTER JOIN "queryset_book_authors" ON ("queryset_book"."id" = "queryset_book_authors"."book_id") LEFT OUTER JOIN "queryset_store_books" ON ("queryset_book"."id" = "queryset_store_books"."book_id") GROUP BY "queryset_book"."id" LIMIT 21; args=()
"""
# 正确统计书类关联的作者和书店的数量
Book.objects.annotate(Count('authors', distinct=True), Count('store', distinct=True))

"""
DEBUG 2022-07-02 16:12:34,381 utils 1528 13516 (0.141) SELECT "queryset_book"."id", "queryset_book"."name", "queryset_book"."pages", "queryset_book"."price", "queryset_book"."rating", "queryset_book"."publisher_id", "queryset_book"."pubdate", COUNT(DISTINCT "queryset_book_authors"."author_id") AS "authors__count", COUNT(DISTINCT "queryset_store_books"."store_id") AS "store__count" FROM "queryset_book" LEFT OUTER JOIN "queryset_book_authors" ON ("queryset_book"."id" = "queryset_book_authors"."book_id") LEFT OUTER JOIN "queryset_store_books" ON ("queryset_book"."id" = "queryset_store_books"."book_id") GROUP BY "queryset_book"."id" LIMIT 21; args=()
"""
Store.objects.aggregate(min_price=Min('books__price'), max_price=Max('books__price'))
"""
DEBUG 2022-07-02 16:18:35,953 utils 1528 13516 (0.222) SELECT MIN("queryset_book"."price") AS "min_price", MAX("queryset_book"."price") AS "max_price" FROM "queryset_store" LEFT OUTER JOIN "queryset_store_books" ON ("queryset_store"."id" = "queryset_store_books"."store_id") LEFT OUTER JOIN "queryset_book" ON ("queryset_store_books"."book_id" = "queryset_book"."id"); args=()
"""

Publisher.objects.annotate(Count('book'))
"""
DEBUG 2022-07-02 16:24:22,476 utils 1528 13516 (0.104) SELECT "queryset_publisher"."id", "queryset_publisher"."name", "queryset_publisher"."num_awards", COUNT("queryset_book"."id") AS "book__count" FROM "queryset_publisher" LEFT OUTER JOIN "queryset_book" ON ("queryset_publisher"."id" = "queryset_book"."publisher_id") GROUP BY "queryset_publisher"."id" LIMIT 21; args=()
"""

Publisher.objects.aggregate(oldest_pubdate=Min('book__pubdate'))

"""
DEBUG 2022-07-02 16:27:51,293 utils 1528 13516 (0.216) SELECT MIN("queryset_book"."pubdate") AS "oldest_pubdate" FROM "queryset_publisher" LEFT OUTER JOIN "queryset_book" ON ("queryset_publisher"."id" = "queryset_book"."publisher_id"); args=()
"""
# 通过values或者values_list实现annotate group by字段替换
Author.objects.values('name').annotate(average_rating=Avg('book__rating'))

"""
424 DEBUG 2022-07-02 16:37:45,395 utils 1528 13516 (0.184) SELECT "queryset_author"."name", AVG("queryset_book"."rating") AS "average_rating" FROM "queryset_author" LEFT OUTER JOIN "queryset_book_authors" ON ("queryset_author"."id" = "queryset_book_authors"."author_id") LEFT OUTER JOIN "queryset_book" ON ("queryset_book_authors"."book_id" = "queryset_book"."id") GROUP BY "queryset_author"."name" LIMIT 21; args=()
"""
Author.objects.annotate(average_rating=Avg('book__rating')).values('name', 'average_rating')
"""
425 DEBUG 2022-07-02 16:40:25,555 utils 1528 13516 (0.175) SELECT "queryset_author"."name", AVG("queryset_book"."rating") AS "average_rating" FROM "queryset_author" LEFT OUTER JOIN "queryset_book_authors" ON ("queryset_author"."id" = "queryset_book_authors"."author_id") LEFT OUTER JOIN "queryset_book" ON ("queryset_book_authors"."book_id" = "queryset_book"."id") GROUP BY "queryset_author"."id" LIMIT 21; args=()
"""


```







## end

* [高级查询文档](https://docs.djangoproject.com/en/4.0/ref/models/conditional-expressions/#conditional-aggregation):when case exists 自关联等
    - `from django.db.models import F, Q, When`
    - `from django.db.models import Exists, OuterRef`
    - `from django.db.models.lookups import GreaterThan, LessThan`
    - `from django.db.models import Case, Value, When`
* [聚合查询](https://docs.djangoproject.com/en/4.0/topics/db/aggregation/):单个表的或者有关联关系的表之间的聚合查询