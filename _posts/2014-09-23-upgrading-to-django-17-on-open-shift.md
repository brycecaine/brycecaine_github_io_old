---
title: Upgrading to Django 1.7 on OpenShift
date:   2014-09-23
categories: django openshift web development
comments: true
---

Here are some key changes that I needed when upgrading to Django 1.7 on OpenShift.

Modify `app-root/repo/wsgi/openshift/settings.py`

Add:

```python
sys.path.insert(0, os.path.abspath(os.path.join(os.path.dirname(file), 'openshift/')))
```

Replace:

```python
import django.core.handlers.wsgi
application = django.core.handlers.wsgi.WSGIHandler()
```

... with

```python
from django.core.wsgi import getwsgiapplication
application = getwsgiapplication()
```

Modify `app-root/repo/wsgi/application`

Add:

```python
ALLOWED_HOSTS = ['.rhcloud.com',]
```
