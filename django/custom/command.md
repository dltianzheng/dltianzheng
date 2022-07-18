# 自定义command

## 路径

* app/management/commands/command_name.py

```python
from django.contrib.auth.models import User
from django.core.management.base import BaseCommand
from django.db import transaction
from django.core import management

from blog.models import Category, Article


class Command(BaseCommand):
    help = 'Populates the database with some testing data.'

    def handle(self, *args, **options):
        self.stdout.write(self.style.SUCCESS('Started database population process...'))

        with transaction.atomic():
            management.call_command('flush', verbosity=0, interactive=False)
    

            # Create users
            zhangsan = User.objects.create_user(username='zhangsan', password='zhangsan')

            lisi = User.objects.create_user(username='lisi', password='lisi')

            wangwu = User.objects.create_user(username='wangwu', password='wangwu')


            # Create categories
            system_administration = Category.objects.create(name='系统管理')
            seo_optimization = Category.objects.create(name='SEO 优化')
            programming = Category.objects.create(name='程序语言')

            # Create articles
            website_article = Article.objects.create(
                title='如何编写和部署一个网站?',
                author=zhangsan,
                type='TU',
                content='部署一个网站的方式有很多种……',
            )
            website_article.save()
            website_article.categories.add(programming, system_administration, seo_optimization)

            google_article = Article.objects.create(
                title='如何提高谷歌评分?',
                author=lisi,
                type='TU',
                content='首先，添加正确的SEO标签…',
            )
            google_article.save()
            google_article.categories.add(seo_optimization)

            programming_article = Article.objects.create(
                title='哪种编程语言最好?',
                author=wangwu,
                type='RS',
                content='最好的编程语言是:\n1) Python\n2) Java\n3) C/ c++…',
            )
            programming_article.save()
            programming_article.categories.add(programming)

            ubuntu_article = Article.objects.create(
                title='安装Ubuntu最新版本',
                author=zhangsan,
                type='TU',
                content="在本教程中，我们将看看如何设置最新版本的Ubuntu。Ubuntu"
                        "(/ʊˈbʊntuː/是一个基于Debian的Linux发行版，主要由免费和开源组成。)"
                        "软件。Ubuntu正式发布了三个版本:桌面版、服务器版和核心版。"
                        "物联网设备和机器人。",
            )
            ubuntu_article.save()
            ubuntu_article.categories.add(system_administration)

            django_article = Article.objects.create(
                title='Django REST Framework and Elasticsearch',
                author=lisi,
                type='TU',
                content="In this tutorial, we'll look at how to integrate Django REST Framework with Elasticsearch. "
                "We'll use Django to model our data and DRF to serialize and serve it. Finally, we'll index the data "
                "with Elasticsearch and make it searchable.",
            )
            django_article.save()
            django_article.categories.add(system_administration)

            self.stdout.write(self.style.SUCCESS('Successfully populated the database.'))
```

* 然后添加INSTALL_APP 就可以用了

## 参考

* [es/model](https://www.modb.pro/db/404535)
