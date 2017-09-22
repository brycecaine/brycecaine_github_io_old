---
title: Sentry on Open Shift
date:   2014-09-19
categories: sentry openshift web development
comments: true
---

Here is how I implemented Sentry on an app I'm hosting on Open Shift.

From my home directory after ssh'ing to my Open Shift box:

Activate the python virtual environment

```bash
source ./app-deployments/2014-04-06_04-22-25.079/dependencies/python/virtenv/bin/activate
```

Install the sentry python package

```bash
pip install raven
```

Add this to `app-root/repo/wsgi/openshift/settings.py`

```python
RAVEN_CONFIG = {
    'dsn': 'https://veryverylonghashfromsentry@app.getsentry.com/fivedigitnumber',
}

# Add to INSTALLED_APPS
'raven.contrib.django.raven_compat',
```

Add this to the wsgi script (app-root/repo/wsgi/application)

```python
from raven.contrib.django.raven_compat.middleware.wsgi import Sentry
from django.core.handlers.wsgi import WSGIHandler

application = Sentry(WSGIHandler())
```

Test that it's working

```python
cd app-root/runtime/repo/wsgi/openshift
python manage.py raven test
```

References:

[Sentry](https://app.getsentry.com/project-name/app-name/docs/django)

[Raven](http://raven.readthedocs.org/en/latest/config/django.html)
