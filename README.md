Tying It All Together
=====================
This repo contains a partially functioning version of the Ubermelon web app. While it is reasonably well constructed, there are a few bugs and unimplemented features, the repair of which will demonstrate some of the subtleties of working within a web framework.

Getting Set Up
--------------
The very first thing to do is clone this repository in the usual manner. Then, follow these steps to get set up.

1. Create and activate a new, empty virtual environment.
2. Use pip to install the packages required in requirements.txt ([full tutorial on pip/virtualenv](http://www.dabapps.com/blog/introduction-to-pip-and-virtualenv-python/))
3. Start the application by running `python melons.py`.

Navigate to [http://localhost:5000](http://localhost:5000) and start exploring the app.

How to Explore
--------------
Our application follows the [model-view-controller pattern](http://en.wikipedia.org/wiki/Model-view-controller). Briefly, the app is divided into three sections, each with its own responsibility. The model is our database, its chief function is to store and retrieve data from long-term permanent storage.

The view of our application is also sometimes called the 'presentation layer'. This code is primarily concerned with how to display data back to the user. These are our .html template files.

Lastly, the controller is the mechanism that listens for data requests from the user, asks the model for the appropriate data (or to store new data), then delivers its findings to the view. Our controllers are found in the file `melons.py`. In this case, our controllers also dictate which URLs are available to the user.

Because the controller is the piece that ties all of the components together, it will be our most important file. It will be the hub from which we explore the rest of the codebase. The gist of all of the above is that the code to generate any given page in our browser will be spread across three, or maybe even four files. However, it is straightforward enough to take a page and find the code that matches it.

1. Get the URL of the page.
2. Locate the function attached to the URL in `melons.py`.
3. Any model-related function calls will be made from this function, prefixed by the module `model`. (eg: `model.get_melons()`) These functions are located in `model.py`.
4. The template name (html file) will usually be located in the return statement for the function, as part of a `render_template()` call.
5. From the template, we can locate any .css files or images relevant to our problem.

Remember, each file has a specific responsibility, so even though you have more than one file open, it is straightforward enough to decide which file to be in.

Taking Stock
------------
Your first task is to explore the app from within your browser. For each page, try to identify the following (and write it down somewhere)

1. The controller function attached to each page
2. The model function calls (if any) for a given page
3. The template for a page

As you do this, watch out for a number of specific things.

### Variable Names in Templates
Try to make sure you understand the source of all the variables that are being used in the .html templates. Whenever you see a `{{ var }}` in a template, make sure that you can match the variable listed with one coming from your model.

### The Melon Detail Template
You'll notice that the melon detail page uses an `{% if %}` statement to display whether or not a given melon is seedless. This is a feature of the Jinja templating engine. In addition to giving us a mechanism for inserting placeholders into our HTML, it also gives us a few control structures, like if-statements and for-loops. We can use this to make the contents of our page a little more dynamic.

[Jinja if-statement documentation](http://jinja.pocoo.org/docs/templates/#if)

### The Melon List Template
The template for our melon list has an example of a Jinja `{% for %}` loop.

[Jinja for-loop documentation](http://jinja.pocoo.org/docs/templates/#for)

### Sparse Templates
You'll see that some of the provided templates are very sparse. This is because for the most part, each page has the same HTML as all the other pages. In the spirit of not repeating ourselves, Jinja provides a mechanism to take the common parts of a template out and move it to a 'skeleton' template that is shared across pages. In our case, the skeleton is `base.html`. As you fix various bugs, you may find that some of the bugs reside in the base template and not the page template.

[Jinja template inheritance documentation](http://jinja.pocoo.org/docs/templates/#template-inheritance)

### Static Files
If you try to access the html templates directly in your browser, ie: navigate over to [http://localhost:5000/templates/all_melons.html](http://localhost:5000/templates/all_melons.html), you will get a 404 error. This is because templates have to be preprocessed before they can be displayed. They have to be run through a controller for all the placeholder variables to be replaced.

However, you can access [http://localhost:5000/static/img/ubermelonsmall.png](http://localhost:5000/static/img/ubermelonsmall.png) without any issue. This is because the ubermelon logo resides in a special directory called `static`. Files that go in this directory are available to the browser without any preprocessing. This makes sense for files like images or stylesheets that don't change: static files.

Template Children/Fruitstrap
-----------------

The login page is unstyled, but the big 'melon list' and 'melon details' page have styles, even though they're not explicit. Explore the 'base.html' file and see how it relates to 'view source'. Use template inheritance to add style to the login page. 

http://flask.pocoo.org/docs/patterns/templateinheritance/

Template Parents
----------------
The login page isn't wired up to the 'log in' image is defined. Find out where that link is created and where it's pointing to. Update it to point to the login page from the above section. Notice how in every page that has the header, they now all go to the correct place.

Static
------
The watermelon.png file isn't displaying in the main template. Fix its URL to display correctly. Try to find the watermelon.png file.

CSS
---
Find where all the styles are defined. Find out where that stylesheet is linked. Add a height of 15px to the watermelon.png.

Directories
-----------
For funsies, create a file called "myfile.html" in the root of your project directory. Try to go to it in your browser. Discuss.

Sessions
--------
UGH
