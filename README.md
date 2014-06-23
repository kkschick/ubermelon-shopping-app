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

if statement in melon details
for loop in melon list

(we navigate by URL)
There's a page that's unattached. Check out line 52 of melons.py

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
