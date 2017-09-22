---
title: New Relic on Open Shift
date:   2014-09-19
categories: newrelic openshift web development
comments: true
---

Here is how I implemented New Relic on an app I'm hosting on Open Shift.

From my home directory after ssh'ing to my openshift box:

Activate the python virtual environment

```bash
source ./app-deployments/2014-04-06_04-22-25.079/dependencies/python/virtenv/bin/activate
```

Install the newrelic python package

```bash
pip install newrelic
```

Generate agent config file

```bash
newrelic-admin generate-config NEW-RELIC-LICENSE-KEY ./app-root/runtime/dependencies/python/virtenv/lib/python2.7/site-packages/newrelic-2.30.0.27/newrelic/newrelic.ini
```

Test that it's working

```bash
newrelic-admin validate-config ./app-root/runtime/dependencies/python/virtenv/lib/python2.7/site-packages/newrelic-2.30.0.27/newrelic/newrelic.ini
```

Modify the wsgi script

```bash
cd app-root/runtime/repo/wsgi/
vim application
```

Add these two lines to the top:

```python
import newrelic.agent
newrelic.agent.initialize('./app-root/runtime/dependencies/python/virtenv/lib/python2.7/site-packages/newrelic-2.30.0.27/newrelic/newrelic.ini')
```

Reference:
[New Relic](https://docs.newrelic.com/docs/agents/python-agent/getting-started/python-agent-quick-start)
