# Update system and Install nessesary things

```bash
$ sudo apt update
$ sudo apt upgrade -y
$ sudo apt install nginx virtualenv
```

# Install Dependencies

```bash
$ virtualenv venv --python=python3
$ source venv/bin/activate
$ pip install -r requirements.txt
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

# initialize the project

```bash
# these apply when the db is not initalized yet.
$ python manage.py migrate
$ python manage.py createsuperuser

# this should be run on every instance
$ python manage.py collectstatic
```

# Install systemd files

```bash
$ sudo cp deployment/gunicorn.* /etc/systemd/system/
$ sudo systemctl start gunicorn.socket
$ sudo systemctl enable gunicorn.socket
```

# Configure nginx

```bash
$ sudo rm /etc/nginx/sites-enabled/default

$ sudo cp deployment/mo-sh.xyz /etc/nginx/sites-available
$ sudo ln -s /etc/nginx/sites-available/mo-sh.xyz /etc/nginx/sites-enabled

$ sudo systemctl restart nginx.service
```

# Update _base.html to see what instance you are in

```bash
$ vim polls/templates/polls/_base.html
```