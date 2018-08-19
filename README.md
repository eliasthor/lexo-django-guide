# lexo-django-guide
A personal guide to creating a Python/Django Site
Thanks a lot to [Django Girls Tutorial](https://tutorial.djangogirls.org/) for providing most of the info I need

# Objective
This Readme file will contain the steps I took towards a fully functional website for a small organisation.

The site I plan to build needs to contain sections such as News, FAQ, About etc.
I like to use linux, so the instruction will be linux based, at least regarding the setup and programming.

Furthermore, I'm usin ubuntu-bash on windows 10, which sometimes requires a different approach than in other setups

The guide requires
  * some knowledge of linux (e.g. how to navigate between folders)
  * some knowledge of how git works
  * installed git
  * linux-ish kind of environment

# What needs to be done
After iterating several times through the process, experiencing errors and clumsyness, I figured these major steps out
  * Create a git repository and clone it to local computer
  * Create virtual environment/virtualenv/venv within the folder from git
  * install pip and setuptools in an activated venv
  * Install Django using a requirements file
  
  This is how my glossary looked like (the last time I went through the steps)
  ```
  Going through steps:
  
  github, create repository
  locally, in some generic folder (e.g. DjangoStuff), clone the git repository
  move into the new folder from git
  cd lexometrica
  
  create venv
  python3 -m venv lexovenv
  
  . lexovenv/bin/activate
  
  python --version
  Python 3.5.2
  python -m pip install --upgrade pip setuptools
  Successfully installed pip-18.0 setuptools-40.1.0
  
  vim requirements.txt --> added one line: Django~=2.0.6
  pip install -r requirements.txt
  Successfully installed Django-2.0.8 pytz-2018.5
  
  django-admin startproject lexosite .
  ```


## Git
### Create a git repository
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
    
### Clone the repository to local folder
I think it's better to get the git repository to the local computer before starting the project

1. Figure out if git is installed locally
    - If not, figure out a way to install it
2. Create a folder for all this stuff, e.g.
    ```
    $ mkdir DjangoStuff
    $ cd DjangoStuff
    ```
3. Clone the repository
    ```
    git clone https://github.com/eliasthor/lexo-django-guide.git
    ```

### Useful git info
* GitLab's "merge-request" is the same as GitHub's "pull-request"

## Virtualenv
The usage of virtualenv(virtual environment) makes it easier to isolate the setup from other projects which migth have different setup requirements (different versions of software etc.)
I like to have the virtualenv inside the projects folder for clarity, but I guess it can be anywhere
Perhaps it's also best to add the venv folder to gitignore, no need to track its changes
  ```
  $ cd lexometrica
  
  create venv
  $ python3 -m venv lexovenv
  
  add venv to .gitignore
  vim .gitignore
  Find the #Environment section and add
  /lexovenv
  
  activate venv
  $ . lexovenv/bin/activate
  (lexovenv)$
  ```

## Install pip and setuptools in an activated venv
This part caused me a lot of problems, probably because I'm working in a linux-bash within Windows 10
The following worked for me at last
  ```
  #with lexovenv activated, make sure the python is 3.x (not 2.7)
  (lexovenv)$ python --version
  Python 3.5.2
  
  # make sure you're located in the same directory as the README.md file
  (lexovenv)$ pwd
  /home/elias/LexoDjango/lexometrica
  
  # The tutorial I used did not include "setuptools"
  # and that cost me a lot of time
  # eventually the following worked for me:
  (lexovenv)$ python -m pip install --upgrade pip setuptools
  Successfully installed pip-18.0 setuptools-40.1.0
  ```
## Install Django
It is reccomended to use a requirements file to install Django
As a start, the requirements file can be created manually
It is possible to recreate a requirement file using complete setup
  ```
  vim requirements.txt
  # added one line: Django~=2.0.6
  
  pip install -r requirements.txt
  Successfully installed Django-2.0.8 pytz-2018.5
  ```

## Start/create the project itself
Now everything should be ready to create the website project
  ```
  (djangovenv)$ django-admin startproject lexosite .
  ```
Some files and folders have now been created
  ```
  # I use tree to show the folderstructure
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

## Check if it works
```
(lexovenv)$ pwd
/home/elias/LexoDjango/lexometrica
(lexovenv)$ ./manage.py runserver
[...]
Django version 2.0.8, using settings 'lexosite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```
It works!
This can be verified by opening http://localhost:8000/ in browser

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
