---
title: '[django快速上手(1/6)] 創建Django項目'
date: 2023-01-31 12:49:36
tags:
  - django
categories:
  - Python
cover: https://miro.medium.com/max/1200/1*slHeZngyeUr7ypEz7MNL5w.png
feature: true
---

# 創建Django項目


- [Django小白入门到实战教程(2020)](https://www.bilibili.com/video/BV1KJ41117HL?p=1&share_medium=android&share_source=copy_link&bbid=XZ4F40A496A2159E1F162FA86D246C96605B5&ts=1603100541043)



## 1. 創建項目


### 創建項目後會產生 manage.py(主要的管理程式，用來運行此項目的程式)和mysite目錄

```bash
(base) [cabie@centosclean 01_Django]$ django-admin startproject mysite
(base) [cabie@centosclean 01_Django]$ ls
mysite
(base) [cabie@centosclean 01_Django]$ cd mysite/
(base) [cabie@centosclean mysite]$ ls
manage.py  mysite

```

### 了解mysite目錄下東西

- settings.py: 整個專案的設定工作<br>
- urls.py: 網址對應工作，可定義伺服器收到什麼網址後，要把工作交給哪一個函數處理<br>
- wsgi.py: 部屬到主機時才用的到<br>
- __init__.py: 代表文件夾下的東西可以被其他東西引入<br>
- asgi.py: `Django`官方正式发布了`Django 3.0`版本，其中最重要的更新莫过于对`ASGI`的支持，為`ASGI`的服务的入口文件了，内容基本同`wsgi.py`。<br>
**參考網站**: [# Django3.0 异步功能尝鲜](https://juejin.im/post/5df32661e51d4558096d5686)<br>
- __pycache__: python解釋器會將 *.py 腳本文件進行編譯，並將編譯結果保存到__pycache__目錄中。下次再執行工程時，若解釋器發現這個 *.py 腳本沒有修改過，就會跳過編譯這一步，直接運行以前生成的保存在 __pycache__文件夾裡的 *.pyc 文件。這樣工程較大時就可以大大縮短項目運行前的準備時間；如果你只需執行一個小工程，沒關係 忽略這個文件夾就行。<br>
**參考**: <br>[https://blog.csdn.net/index20001/article/details/73501375](# 运行Python脚本时生成的__pycache__文件夹)<br>



```bash
(base) [cabie@centosclean mysite]$ pwd
/home/cabie/01_python/01_Django/mysite/mysite
(base) [cabie@centosclean mysite]$
(base) [cabie@centosclean mysite]$
(base) [cabie@centosclean mysite]$ ll
總計 16
-rw-rw-r--. 1 cabie cabie  389  2月 21 03:15 asgi.py
-rw-rw-r--. 1 cabie cabie    0  2月 21 03:15 __init__.py
drwxrwxr-x. 2 cabie cabie   95  2月 21 03:21 __pycache__
-rw-rw-r--. 1 cabie cabie 3088  2月 21 03:15 settings.py
-rw-rw-r--. 1 cabie cabie  748  2月 21 03:15 urls.py
-rw-rw-r--. 1 cabie cabie  389  2月 21 03:15 wsgi.py

```





## 2. 產生對應資料庫

會產生db.sqlite3(使用資料庫所依賴的東西)

```j
(base) [cabie@centosclean mysite]$ python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying sessions.0001_initial... OK




(base) [cabie@centosclean mysite]$ ls
db.sqlite3  manage.py  mysite

```



## 3. 啟動項目

```bash
(base) [cabie@centosclean mysite]$ python manage.py runserver 0.0.0.0:8000
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
February 20, 2020 - 19:44:11
Django version 3.0.3, using settings 'mysite.settings'
Starting development server at http://0.0.0.0:8000/
Quit the server with CONTROL-C.

```
![](https://images2.imgbox.com/60/50/h2UBRBLx_o.png)

因為未將此ip加入ALLOWED_HOSTS，更改settings.py<br>

```
ALLOWED_HOSTS = ["192.168.1.108"]
```

![](https://images2.imgbox.com/d7/ab/8BzYg4nr_o.png)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA3NTAyNzUzNywxMTYzNDg2MTA2XX0=
-->