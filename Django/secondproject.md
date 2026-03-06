# Creating Django project

## First Step: Creating virtual Environment
- Everytime create Virtual Environment for all project
- To create Virtual Environment, We just need to activate it because it is already installed inside python
    ```
    python -m venv env
    ```
    ```
    source env/Scripts/activate
    ```

**Use following to check installed content**

```
pip freeze
```

## Second Step: Installing django framework
- To install it
    ```
    pip install django
    ```
- To check it installed content
    ```
    pip freeze
    ```


## Third step: Creating Django project
- To start project
    ```
    django-admin startproject mysite .
    ```
        - Using dot(.) symbol means project should be created inside root folder

## Fourth Step: Run Django server
- Run the server
    ```
    python manage.py runserver
    ```


# Some important code
- **For running server**
    ```
    python manage.py runserver
    ```

- **For creating New App**
    ```
    python manage.py startapp app_name
    ```

- **For creating Super User**
    ```
    python manage.py createsuperuser
    ```

- **For changing the password**
    ```
    python manage.py changepassword User_name
    ```

- **For creating tables**
    ```
    python manage.py makemigrations
    ```


## Some important in Django
- **init.py**
    - we can ignore this file because we don't need to do anything with this file.
    - Then why this is created?
        - It is not simple folder, it is python package. 
    - Can we delete this?
        - No, because deleting this make unable to import modules from one package to another
        - Being, software developer we need to reuse code again and again. So we need to import function and this is possible because of this init.py file

- **wsgi.py**
    - Wsgi stand for web server gateway interface
    -  Concern with wsgi server and it is used for deployment on server like apache or nginix


- **asgi.py**
    - It works similar to wsgi  but it comes with some additional functionality.
    - Stands for Asynchronouse Server Gateway Interface


- **urls.py**
    - It is universal resource locator
    - It contains all endpoints we need to have for our website
    - Provides address of resources(images, webpages, websites)


- **settings.py**
    - Most important file used for adding all configuration in django project

    - BASE_DIR
        - Getting root directory dynamically

    - SECRET_KEY
        - Used to generate hashes

    - ALLOWED_HOSTS
        - Here enter domain name of website where you want to run project
        - In development server if you leave blank then there will be no error
        - But in development server we need to add either IP or domain name

    - INSTALLED_APPS
        - Package with django module which perform business logic
        - Django project can have multiple apps and can create reusable components based on logic
        - So, whenever you create an APPs you need to register here

    - MIDDLEWARE
        - It performs different functions in Application like security, sessions, form production, authentication
        - Django provides inbuilt middleware and also allow us to create custom made middleware

    - ROOT_URLCONF
        - Tells main url configuration reside here
        
    - TEMPLATES
        - Responsible for rendering front-end templates
        - it tells django from where  wsgi application should run

    - DATABASES
        - default will be sqlite3 configuration but we can always change it MYSQL or POSTGRESQL or any other

    - AUTH_PASSWORD_VALIDATORS
        - Built in password validators comes bydafult
        - Checks strength of user password

    - Internationalization
        - different language code, time zone are available
        - USE_I18N means if you want internationalization then set it TRUE. Internationalization is way of changing languages like with multiple english, arabic, chineese and so on

    - STATIC_URL
        - For static content like CSS, JS, images




## How Django actually works?
- It follows MVT(Model View Template) software design pattern


## Lets start our first project
- At first go to url.py and go to urlpatterns and create path 
    - path('home/', views.home, name='home'),
- Since we hadn't create views.py file yet so now create that

## Creating Template
- Instead of using HttpResponse lets render Template
- Lets create now new folder called templates in root
- Now lets create home.html inside template


## Creating static file

## Creating App
```
python manage.py startapp employee
```
- Here employee app is created
- Put name in settings.py installed app

## Login in /admin
- We need to create superuser before login it
    ```
    python manage.py createsuperuser
    ```

## To create database table
- At first go to employee models.py and make the fieldname of table
- After making fieldname now run two commands
    ```
    python manage.py makemigrations
    ```
    ```
    python manage.py migrate
    ```
