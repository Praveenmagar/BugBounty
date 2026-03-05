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

    - 