# lexo-django-guide
A personal guide to creating a Python/Django Site

This Readme file will contain the steps I took towards a fully functional website for a small organisation.

The site needs to contain sections such as News, FAQ, About etc.
I like to use linux, so the instruction will be linux based, at least regarding the setup and programming.

## Create a git repository
1. Create git repository (assuming you have a github account since you're here already)
    - The name and description will appear as the first two lines in this document
2. Select "Public" unless you like to pay for privacy
3. Check "Initialize this repository with a README
    - Creates this file
4. Select Python from the "Add .gitignore".
    - It allows you to ignore files which do not need to be tracked (e.g. temporary files)
5. Read about formatting this file
    - E.g. [here](https://help.github.com/articles/basic-writing-and-formatting-syntax/)
6. Commit changes
    - I did not create a new branch for this commit as it is the first/initial commit.
    
## Clone the repository to local folder
I think it's better to get the git repository to the local computer before starting the project

1. Figure out if git is installed on yo
    - If not, figure out a way to install it
2. Clone the repository
    ```
    git clone https://github.com/eliasthor/lexo-django-guide.git
    ```

## Useful git info
* GitLab's "merge-request" is the same as GitHub's "pull-request"

## How to start the project
Now, how do I start the project it self?

It would also be nice to be able to have the project running in linux, but the coding could take place anywhere.

To make that work, every change would need to be committed and pushed to git, then pulled from git into the testing/running environment how it turns out.

To begin with I'll stick to linux. I will use Ubuntu Bash from within Windows 10 (search for instructions on how to run ubuntu on Windows 10)

1. Look for some how-to instructions
    - As soon as I know what I'm doing, I can update (or even remove) this step
    - I start by looking at [Django Girls Tutorial](https://tutorial.djangogirls.org/)
    - Django Girls Tutorial assumes python3.6 while my windows 10 version of ubuntu only has 3.5, I'll need to work around that
2. Start by creating a folder for the procect and move into that folder
    ```
    mkdir LexoDjango
    cd LexoDjango
    ```
3. Set up virtual environment within the new folder
    - Virtual environment (virtual env or just venv) seems to be the trend, I guess it "shields" the setup from unwanted changes in the enviromental settings
    ```
    python3 -m venv lexovenv
    ```
    Activate it (I find it easier to use alias for this)
    ```
    alias lexovenvstart=". lexovenv/bin/activate"
    lexovenvstart
    ```
4. Install Django
    - see [Django Girls](https://tutorial.djangogirls.org/en/installation/)

## Add stuff to git
1. Get the latest changes from git and then check the git status (on which branch am I, is there something that needs to be added)
    ```
    # refresh local repository
    git pull
    # on which branch am I, is there anything to be committed/added
    git status
    ```
2. Add everything to git
    ```
    # select every folder/file by referencing current directory (.)
    git add .
    # commit stuff
    git commit -am "Adding project to git repo"
    # update remote repository
    git push
    # branch can be merged on remote repository after pushing
    # consider continueing on branch until the branc is completely finished
    ```
    
## Create Django Project
Now it is possible to create the Django project it self
1. If venv is not active, activate it
    ```
    . lexovenv/bin/acitvate
    # or use alias
    ```
2. Run
    ```
    django-admin startproject lexosite
    ```
### I've twice run into problems when trying to run django-admin startproject
  * The second time was this:
    After creating venv using
    ```
    $ python3 -m venv lexovenv
    $ . lexovenv/bin/activate
    (lexovenv)$ python3 -m pip install --upgrade pip
    (lexovenv)$ vim requirements.txt
    (lexovenv)$ pip install -r requirements.txt
    (lexovenv)$ django-admin startproject lexosite
    # error
    (lexovenv)$ python --version
    Python 3.5.2
    (lexovenv)$ python3 -m pip install --upgrade pip
    (lexovenv)$ django-admin startproject lexosite .
    # error
    (lexovenv)$ apt install python-django-common
    # error
    (lexovenv)$ sudo apt install python-django-common
    (lexovenv)$ django-admin startproject lexosite .
    # error
    (lexovenv)$ pip install -r requirements.txt
    # django already installed
    (lexovenv)$ sudo pip install -r requirements.txt
    # more convincing stuff starts
    # but still get an error implying usage of Python2.7
    # error includes suggestions
    # a) python -m pip install --upgrade pip setuptools
    # b) python -m pip install django
    (lexovenv)$ python -m pip install --upgrade pip setuptools
    [...]
    Successfully installed setuptools-40.1.0
    (lexovenv)$ python -m pip install django
    Requirement already satisfied
    (lexovenv)$ django-admin startproject lexosite .
    # no error
    ```
  * The first time was this
### I ran into problems runnig the django-admin startproject, I got an error saying
```
The program 'django-admin' is currently not installed. You can install it by typing:
sudo apt install python-django-common
```
This seems strange and indicates that django is not installed
As I'm working on branch master, I'm going to try merging the other branch I was using to see what will happen

Found out that I hadn't completed the installation...
The installation starts by activating virtualenv
Then install pip
Then install django
This failed on ubuntu bash on my windows 10 because the venv was referencing python2.7

What I did to solve this
  * removed the venv directory (rm -rf lexovenv)
  * installed python3-venv
  * created the virtualenv again

  ```
  $ rm -rf lexovenv
  $ sudo apt install python3-venv
  $ python3 -m venv lexovenv
  $ . lexoxovenv/bin/activate
  (lexovenv)$ python --version
  Python 3.5.2pyt
  ```
Now I'm hoping to be able to proceed, next job is to install pip and django using requirement file
```
(lexovenv)$ python3 -m pip install --upgrade pip
(lexovenv)$ pip install -r requirements.txt
[...]
Successfully installed Django-2.0.8. pytz-2018.5
```

Start Django project
```
(lexovenv)$ django-admin startproject lexosite .
(lexovenv)$ tree -L 2
.
├── lexosite
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── lexovenv
│   ├── bin
│   ├── include
│   ├── lib
│   ├── lib64 -> lib
│   ├── pip-selfcheck.json
│   ├── pyvenv.cfg
│   └── share
├── manage.py
├── README.md
└── requirements.txt
```
Looks promising

Check if it works
```
$ pwd
/home/elias/LexoDjango/lexo-django-guide
$ ./manage.py runserver
[...]
Django version 2.0.8, using settings 'lexosite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```
It works!
This can be verified by opening http://localhost:8000/ in browser

Now, what's next?
Still using info from DjanogGirls
Add TO lexosite/settings.py:
STATIC_ROOT = os.path.join(BASE_DIR, 'static')

Next?
Set up a database as shown in DjangoGirls tutorial
Using default database, so no changes in settings.py

Create a database for the website project:
```
python manage.py migrate
```
Create a new applicationi which belongs to the project
On the same level as manage.py
```
python manage.py startapp lexonews
```
This results in a new folder called lexonews
```
$ tree -L 2 lexonews
lexonews
├── admin.py
├── apps.py
├── __init__.py
├── migrations
│   └── __init__.py
├── models.py
├── tests.py
└── views.py
```

The application/app needs to be registered in settings.py so that django knows it should be using it
```
vim lexosite/settings.py
[...]
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'lexonews',
]

[...]
```

Then what?
Create a model (model is an object which maps to a table in database)
This is how I started with lexonews/models.py:
```
from django.db import models
from django.utils import timezone

class Article(models.Model):
    author = models.ForeignKey('auth.User', on_delete=models.CASCADE)
    headline = models.CharField(max_length=200)
    text = models.TextField()
    created_date = models.DateTimeField(
        default=timezone.now)
    published_date = models.DateTimeField(
        blank=True, null=True)

def publish(self):
        self.published_date = timezone.now()
        self.save()

def __str__(self):
        return self.headlinew
```

Now use this to create a database table:
```
$ python manage.py makemigrations lexonews
Migrations for 'lexonews':
  lexonews/migrations/0001_initial.py
    - Create model Article

$ python manage.py migrate lexonews
```

So, now a database table has been created using model object describing the attributes of the table.
The data can be edited via admin site, but to be able to do that, I need to register the model as an admin thing:

Edit the lexonews/admin.py:
```
$ vim lexonews/admin.py

from django.contrib import admin
from .models import Article

admin.site.register(Article) 
```

Now I can work with the table (add, edit and delete article), or what?
First I need a user, a superuser to be precise.
```
$ python manage.py createsuperuser
```

At this point I wonder if I should have had this guide as a seperate project/repository in git and have the code elsewhere.
Probably it would be best to create a new repo for the website and remove the code from here

This is a good oportunity to test this guide.
