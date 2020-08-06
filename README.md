# Chamnan App (Django + React js)

## complete core-banking solution and platform for business management

**Note** : Chamnan folder: root (Master Project)
    config: Django project
    frontweb: react project 
## The Backend    
### Create Django Project Install
1. Set up Virtual Environment and install Django with other dependencies and libraries later
2. Create django project with name 'config'
3. $ django-admin startproject config .
4. [Database configuration](#database)
5. [Add JWT-Authentication to Django](#add-jwt)

### Create React Js App
1. Install create-react-app system-wide
2. $ npm install -g create-react-app
3. Create React app with name 'frontweb', eject the config files so that we can edit them and run test it
4. $ create-react-app frontweb
5. $ cd frontweb
6. <del>$ npm run eject</del>
7. $ npm run start

## <a name="database"></a>Database configuration

```py
# File: ./Chamnan/config/settings.py**
DATABASES = {
    'default': {
        # 'ENGINE': 'django.db.backends.sqlite3',
        # 'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'your-db',
        'USER': 'postgres',
        'PASSWORD': 'your-password',
        'HOST': 'localhost',
        'PORT': 'your-port',
    }
}
```
 We need to create a user, and before do that, we need to apply our migrations. Run the following:

```bash
python manage.py migrate
```
Once that’s done, the easiest way to create a new user is with:
```bash
python manage.py createsuperuser
```
## <a name="add-jwt"></a>Add JWT-Authentication to Django

```py
# File: ./Chamnan/config/settings.py**

INSTALLED_APPS = [
    'django.contrib.staticfiles',
    'rest_framework',
    'corsheaders',
    'core.apps.CoreConfig',
]

REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': (
        'rest_framework.permissions.IsAuthenticated',
    ),
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_jwt.authentication.JSONWebTokenAuthentication',
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.BasicAuthentication',
    ),
}

CORS_ORIGIN_ALLOW_ALL = True

JWT_AUTH = {
    'JWT_RESPONSE_PAYLOAD_HANDLER': 'version1.utils.my_jwt_response_handler',
}
```
Now that Rest Framework is configured, we need to add a few URLs:

```py
# File: ./backend/backend/urls.py

[...]
from rest_framework_jwt.views import obtain_jwt_token
from rest_framework_jwt.views import refresh_jwt_token
from rest_framework_jwt.views import verify_jwt_token

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api-token-auth/', obtain_jwt_token),
    path('api-token-refresh/', refresh_jwt_token),
    path('api-token-verify/', verify_jwt_token),
    path('core/', include('core.urls'))
]
```

> At this point you should be able to get a token by sending this request: `curl -X POST -d "username=*****&password=*****" http://localhost:8000/api-token-auth/`
