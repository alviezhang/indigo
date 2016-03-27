---
layout: post
title: 升级Django 1.3 -> 1.7
date: 2015-03-03
description:
tags: Python, Django
blog: true
---

Django 1.3 >> Django 1.7

-------------

* ### `ImportError: cannot import name execute_manager` ###

修改前`manage.py`:

    #!/usr/bin/env python
    from django.core.management import execute_manager
    import imp
    try:
        imp.find_module('settings') # Assumed to be in the same directory.
    except ImportError:
        import sys
        sys.stderr.write("Error: Can't find the file 'settings.py' in the directory containing %r. It appears you've customized things.\nYou'll have to run django-admin.py, passing it your settings module.\n" % __file__)
        sys.exit(1)

    import settings

    if __name__ == "__main__":
        execute_manager(settings)

错误的原因是`execute_manager`在Django 1.4版本后废弃，并在1.6版本后移除，根据[Django 1.4 升级说明]()，
只需把`manage.py`改成如下即可：

    #!/usr/bin/env python
    import os, sys

    if __name__ == "__main__":
        os.environ.setdefault("DJANGO_SETTINGS_MODULE", "settings")

        from django.core.management import execute_from_command_line

        execute_from_command_line(sys.argv)


[Django 1.4 升级说明](https://docs.djangoproject.com/en/1.4/releases/1.4/#updated-default-project-layout-and-manage-py)

* ### 模版、静态文件目录相关 ###

`settings.py`变动如下：

    STATIC_URL = '/static/'                             # 从空格改为空
    
    TEMPLATE_DIRS = (
        os.path.join(ROOT_PATH, 'template'),    # 添加一个逗号
    )

    STATIC_ROOT = './static'

* ### messages消息不显示 ###

`settings.py`变动如下：

    TEMPLATE_CONTEXT_PROCESSORS = {
        ...
        'django.contrib.messages.context_processors.messages',  # fix django messages when upgrade to django 1.7
    }

[Enabling messages](https://docs.djangoproject.com/en/1.7/ref/contrib/messages/#enabling-messages)

