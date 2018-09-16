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
  * linux-ish kind of environment (terminal/command prompt)
  * [tmux](https://robots.thoughtbot.com/a-tmux-crash-course) is reccomended but not required

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
  $ cd lexometrica
  
  create venv
  $ python3 -m venv lexovenv
  -- on a different pc I ran into an error saying venv was not installed
  -- installing python3-venv was suggested
  -- but after some researching I ran
  $ python3 --version
  Python 3.6.5
  $ sudo apt-get install pyton3.6-venv 
  $ python3 -m create venv lexovenv
  -- it worked
  -- activate it
  . lexovenv/bin/activate
  
  python --version
  Python 3.5.2
  # Python 3.6.5 on the other PC
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
    # this repository:
    $ git clone https://github.com/eliasthor/lexo-django-guide.git
    
    # The website project:
    $ git clone https://github.com/eliasthor/lexometrica.git
    
    # As the website project progresses, other branches might be available
    # Switch to a different branch, e.g. LexoNews like this:
    $ git checkout LexoNews
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
This can be verified by opening [http://localhost:8000/](http://localhost:8000/) in browser

Now the terminal window is occupied running the server
To continue do one of the following
* Shut down the server by pressing Ctrl-c
* Open new terminal
* Split the terminal (which is possible when using tmux which I highly reccomend)

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
    (lexovenv)$ git add .
    # commit stuff
    (lexovenv)$ git commit -am "Adding project to git repo"
    # update remote repository
    (lexovenv)$ git push
    # branch can be merged on remote repository after pushing
    # consider continuing on branch until the branch is completely finished
    
    (lexovenv)$ git checkout -b LexoNews
    # creates a new branch based on current branch (master) and switches to it
    # new branch is called LexoNews
    # verify on which branch I am working
    (lexovenv)$ git branch
    * LexoNews
    master
    ```

# Start Development
Now it's time to move on and do some programming work

The DjanogGirls tutorial suggest adding a path to static files to settings.py but I guess it's mainly to demonstrate how settings can be changed.
It's probably best to get it done (saves some steps later I guess)

  ```
  (lexovenv)$ vim lexosite/settings.py
  # add STATIC_ROOT path at the end of the file (next to STATIC_URL)
  
  STATIC_URL = '/static/'
  STATIC_ROOT = os.path.join(BASE_DIR, 'static')
  ```

## Database setup
Set up a database as shown in DjangoGirls tutorial
Using default database, so no changes in settings.py

Create a database for the website project:
  ```
  (lexovenv)$ python manage.py migrate
  ```

## Create application
Create a new application which belongs to the project (on the same level as manage.py)
  ```
  (lexovenv)$ python manage.py startapp lexonews
  ```
This results in a new folder called lexonews
  ```
  (lexovenv)$ tree -L 2 lexonews
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

## Register the new application
The application/app needs to be registered in settings.py so that django knows it should be using it
  ```
  (lexovenv)$ vim lexosite/settings.py
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

## Create a model and database table
### Create a model (model is an object which maps to a table in database)
Edit lexonews/models.py (make sure indentation is correct)
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
          return self.headline
  ```

### Use the model to create a database table:
  ```
  (lexovenv)$ python manage.py makemigrations lexonews
  Migrations for 'lexonews':
    lexonews/migrations/0001_initial.py
      - Create model Article
  
  (lexovenv)$ python manage.py migrate lexonews
  ```

## Make the new model/table accessible via django admin page
So, now a database table has been created using model object describing the attributes of the table.
The data can be edited via admin site, but to be able to do that, the model needs to be registered as an admin thing

  ```
  (lexovenv)$ vim lexonews/admin.py

  from django.contrib import admin
  from .models import Article
  
  admin.site.register(Article) 
  ```

## Create superuser
A user is needed to be able to access the model via admin page

Each time the web is installed on a new server, a superuser needs to be created
  ```
  (lexovenv)$ python manage.py createsuperuser
  # follow the instructions
  # don't worry if you don't see your password, it's invisible
  ```

## View the new model via admin page
If the server is not already running in a seperate terminal, then start it (in a seperate terminal)
  ```
  (lexovenv)$ pwd
  /home/elias/LexoDjango/lexometrica
  (lexovenv)$ ./manage.py runserver
  ```
* Open the admin page in a browser [http://localhost:8000/admin/](http://localhost:8000/admin/)
* Log in using the superuser account

## Create the GUI
Until now, the user cannot see anything useful.

I need to do something to change that

### Configure URL to use
Follow [DjangoGirls instructions](https://tutorial.djangogirls.org/en/django_urls/) but adjust app names etc. as needed

My first lexonews/urls.py looks like this
```
from django.urls import path
from . import views

urlpatterns = [
    path('', views.articles, name='articles'),
]
```

### Create views
Views store most of the logic (!)

View connects models and templates

View holds the logic which decides what to show in templates

Continuing using [DjangoGirls instructions](https://tutorial.djangogirls.org/en/django_views/)

My first working version of lexonews/views.py looks like this

```
from django.shortcuts import render
from django.utils import timezone
from .models import Article

def articles(request):
    articles = Article.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
    return render(request, 'lexonews/articles.html', {'articles': articles})
```

### Create template
The actual html files are called templates and are stored in the app directory under templates, e.g. lexonews/templates/lexonews/articles.html

See the instructions mentioned above
#### Add css to make it look better
See [DjangoGirls](https://tutorial.djangogirls.org/en/css/) to see how

My first working template (lexonews/templates/lexonews/articles.html) looks like this (including bootstrap css stylesheet reference)
```
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
<div>
    <h1><a href="/">Lexometrica News</a></h1>
</div>

{% for article in articles %}
    <div>
        <p>published: {{ article.published_date }}</p>
        <h1><a href="">{{ article.headline }}</a></h1>
        <p>{{ article.text|linebreaksbr }}</p>
    </div>
{% endfor %}
```

### How the lexonews tree looks like after adding URLs, views and templates (omitting migrations and other stuff)
  ```
  lexonews
  ├── admin.py
  ├── apps.py
  ├── __init__.py
  ├── models.py
  ├── templates
  │   └── lexonews
  │       └── articles.html
  ├── tests.py
  ├── urls.py
  └── views.py
  ```

### Static files
Files which are not changing, static files, such as those who define the look on the web, belong in a special directory called "static"

DjangoGirls tutorial shows a bit about css so I'm not going through that here

Here is how the tree looks like after adding the css file:

  ```
  lexonews/
  ...
  ├── admin.py
  ├── apps.py
  ...
  ├── models.py
  ├── static
  │   └── css
  │       └── lexonews.css
  ├── templates
  │   └── lexonews
  │       └── articles.html
  ```
  
In addittion to css files, a base file can be added to the static directory.

It should contain the basic structure for the web, to be used to keep the structure consistent:
[Again, take a look at the DjangoGirls Turorial](https://tutorial.djangogirls.org/en/template_extending/#create-a-base-template)


## User administration/authentication
Now how can I make it possible for users to add new things to the site?
I guess I need some sort of user administration (sign up, log in) and a page to write articles
