# Creating project
- **Installing Django and creating project**
    - To activate virtual environment
    ```
    source env/Scripts/activate
    ```
    ```
    pip install Django
    ```
    ```
    python -m pip install --upgrade pip
    ```
    ```
    django-admin startproject Cybertechschool .
    ```
    ```
    python manage.py runserver
    ```

- **Creating SuperUser**
    - For creating superuser our database need to have default table and for that we run migrate command
    ```
    python manage.py migrate
    ```
    - This creates default database tables
    ```
    python manage.py createsuperuser
    ```
    - This creates superuser now run server and login to super user
    ```
    python manage.py runserver
    ```
    - go to /admin and login 


- **Implementing template**
    - Now lets remove default django page and create our own home page.
    - At first, create URL pattern, for first(home) page always use empty string URL pattern
    - Go to (urls.py) and create path
