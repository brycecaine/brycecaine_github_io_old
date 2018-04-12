---
title: Running Selenium in Headless Mode with Firefox
date:   2018-04-11
categories: django python selenium headless test-driven web development
comments: true
---

There's something super satisfying about having a development VM in the cloud. I can ssh to it from any device, tmux to persist sessions, and develop with vim virtually anywhere.

So I decided to start learning more about test-driven development. I saw good reviews for "Test-Driven Development with Python, 2nd Edition" by Harry J.W. Percival, so I thought I'd start reading it to augment side projects and other learning.

To merge the two ideas--a VM in the cloud and test-driven development with Django and Selenium--I needed to go headless. So here's how I set up my Ubuntu 17.10 environment.

These notes are based on Chapter 1. "Getting Django Set Up Using a Functional Test", and the package versions match the book requirements.

### Set up the needed python environment and packages

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install python3-pip
sudo pip3 install virtualenv
virtualenv tddp
source tddp/bin/activate
pip3 install Django==1.11.8
pip3 install selenium==3.9.0
wget https://github.com/mozilla/geckodriver/releases/download/v0.19.1/geckodriver-v0.19.1-linux64.tar.gz
tar -xvzf geckodriver-v0.19.1-linux64.tar.gz
sudo cp geckodriver /usr/local/bin/
```

### Modify the functional_tests.py script

#### From the book

```python
from selenium import webdriver

browser = webdriver.Firefox()
browser.get('http://localhost:8000')

assert 'Django' in browser.title
```

#### Modified version to support headless

```python
from selenium import webdriver
from selenium.webdriver.firefox.options import Options

options = Options()
options.add_argument("--headless")
browser = webdriver.Firefox(firefox_options=options)
browser.get('http://localhost:8000')

assert 'Django' in browser.title
```
