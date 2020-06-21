# Install Dependencies

```bash
$ virtualenv venv
$ source venv/bin/activate
$ pip install -r requirements.txt
```

# initialize the project

```bash
$ python manage.py migrate
$ python manage.py createsuperuser
$ python manage.py collectstatic
```

# Update the following in settings.py

```python
DEBUG = False

DATABASES = {
    "default": {
        "NAME": "postgres",
        "PASSWORD": "test123456",
        "HOST": "devops-db.cxky9eesblfs.eu-central-1.rds.amazonaws.com",
        "PORT": "5432",
    }
}
```

# Install systemd files

```bash
$ cp gunicorn.* /etc/systemd/system/
$ sudo systemctl start gunicorn.socket
$ sudo systemctl enable gunicorn.socket
```

# Configure nginx

```bash
$ rm /etc/nginx/sites-enabled/default

$ cp mo-sh.xyz /etc/nginx/sites-available
$ ln -s /etc/nginx/sites-available/mo-sh.xyz /etc/nginx/sites-enabled
```