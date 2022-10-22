Real World base Django For TiDB Cloud
--

Thanks [danjac/realworld](https://github.com/danjac/realworld) project offer so great example.

This Project is created for Ti-Click project join PingCAP Hackathon 2022.

### 1. Ready the TiDB Cluster
You can create the TiDB Cluster on [TiDB Cloud](https://tidbcloud.com) which offer free TiDB Cluster.

### 2. Access Gitpod
Access [Real World base Django](https://gitpod.io/#/github.com/ti-click/realworld-base-django) link and open the online IDE.

Then input the `/realworld/settings.py` database setting info. *database name*, *username*, *password* and *host* is necessary.
Example
```
DATABASES = {
    "default": {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': '${DATABASE}', 
        'USER': '${USERNAME}', 
        'PASSWORD': '${PASSWORD}', 
        'HOST': '${HOST}', 
        'PORT': '4000'
    }
}
```


### 3. Setting the TiDB variable and security
#### 3.1 Remove *ONLY_FULL_GROUP_BY* setting 
The **real world** don't support ONLY_FULL_GROUP_BY. So it need to be removed from TiDB global variables.
```
mysql> SHOW GLOBAL VARIABLES LIKE 'sql_mode';
+---------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| Variable_name | Value                                                                                                                                     |
+---------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| sql_mode      | ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION |
+---------------+-------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.26 sec)

mysql> SET GLOBAL sql_mode='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION'
    -> ;
Query OK, 0 rows affected (0.19 sec)

mysql> SHOW GLOBAL VARIABLES LIKE 'sql_mode';
+---------------+------------------------------------------------------------------------------------------------------------------------+
| Variable_name | Value                                                                                                                  |
+---------------+------------------------------------------------------------------------------------------------------------------------+
| sql_mode      | STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION |
+---------------+------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.18 sec)
```

#### 3.2 Add Gitpod ip into TiDB Cloud access white list

You can get the ip by the command below. Please add it into your TiDB Cloud security.

`curl https://ipinfo.io/ip `

OR **You can add `0.0.0.0/0` into white list. Let all access is accepted**

### Referance
1. https://danjacob.net/posts/anatomyofdjangohtmxproject/
2. https://readthedocs.org/projects/django-conduit/downloads/pdf/latest/

[danjac/realworld](https://github.com/danjac/realworld) Readme.md
---
Implementation of real-world application: https://github.com/gothinkster/realworld/ using Django and HTMX.

An in-depth discussion of this implementation can be found [here](https://danjacob.net/posts/anatomyofdjangohtmxproject/).

Tech Stack:

* [Django](https://djangoproject.com)
* [HTMX](https://htmx.org)
* [Alpine](https://alpinejs.dev)

To install and run locally:

```bash
git clone https://github.com/danjac/realworld/ && cd realworld

python -m venv venv

source venv/bin/activate

pip install -r requirements.txt

./manage.py migrate && ./manage.py runserver
```


**Note: this is just a reference implementation and is not intended for production use.**
