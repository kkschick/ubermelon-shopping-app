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

Task 1: Taking Stock
--------------------
Your first task is to explore the app from within your browser. The goal is to understand how the app is laid out. For each page, try to identify the following (and write it down somewhere)

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

### The Checkout Button
Checking out our shopping cart is outside the scope of our task, but it is worth noting the 'message flash' mechanism that is used when you try to check out. It is a way to display one-time messages to the user. This is a great place to place error, warning, or success messages. Flashed messages only display once, if you reload the page, you will see that it disappears on the second view.

[Flask Message Flashing documentation](http://flask.pocoo.org/docs/patterns/flashing/)

### Styling
Most of the style work in our app was not written manually. Instead, we used [bootstrap](http://getbootstrap.com/getting-started/#examples), a css framework. The bootstrap framework specifies 'components', higher level UI components composed of more basic HTML tags. Notably, we use the `navbar` component and the `well` component.

[Bootstrap component list](http://getbootstrap.com/components/)

Task 2: The Login Page
----------------------
If you click on the 'Log In' link in the nav bar at the top of the screen, you'll see that it does nothing. However, if you peruse the list of routes available in your `melons.py` file, you will find that there is a login route that is inaccessible by clicking. You can, however, browse on over to the URL directly in your browser.

###Fixing this bug
1.  Wire up the link to go to the page. 

    Your first task is to locate the `<a href>` tag that is used in the black bar at the top of the page. This section of the page is typically called the navbar. It may be tricky at first to find where in the code this tag exists. Remember to use the browser's element inspector to see exactly what lines of HTML you're looking for. Also remember that this part of the page is shared across multiple pages.

2.  Style the page. 

    When you _do_ have the login page 'wired up', you'll notice that it's styled pretty terribly. We want it to use the same style as all the other pages. We could try to add bootstrap to the HTML directly, but it is easier to make this page a child of our `base.html` template. Check either `melon_details.html` or `all_melons.html` for an example on how to do that.

Task 3: The Melon Cart Icon
---------------------------
The melon cart link at the top of the page has a broken image. If you browse around our directory tree, you'll find that the file exists, but isn't linked properly.

###Fixing this bug
1.  First, fix the link. 

    Make sure you understand why it's not displaying in the first place.

2.  Style this component. 

    Find the stylesheet that's being used and fiddle with the style to make it display correctly. A height of 15px on this image should do it. Try to figure out a CSS selector that targets just that image without affecting others. Here's a [css selector guide](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_started/Selectors) if you need help.

Task 4: The Melon Cart Functionality
------------------------------------
When you view the shopping cart, you'll notice that all the items in it are placeholder dummy items. We'll need to replace these items with actual melons. In addition, the 'Add to Cart' button on the melon detail page is wired up but the controller currently' doesn't do anything.

We need a way to temporarily hold information that the user generates (ie: which melons are in the cart). We could commit this to the database, but it would be cumbersome. Instead, we'll use a storage mechanism called 'the session' to carry information from clicking the 'Add to Cart' button all the way to the shopping cart page.

[Session documentation](http://flask.pocoo.org/docs/quickstart/#sessions)

###Implementing this feature
This feature is two-part. The order in which you build the feature doesn't matter, but it may be helpful to write both in conjunction.

1.  Add things to the cart. 

    When you click the `add to cart` button, the fact that a melon has been added to a cart needs to be recorded somewhere. This isn't long-term information, nor is it information that's attached to any particular user. It's short-term information that's attached to the browser you're currently using. This kind of information is best stored in the session.

    For now, we can use a list as our 'cart' and just put our Melon objects inside it to represent the idea of them being added. Breaking down the process, here are the steps you should go through:

    1. On adding an item, check to see if the session contains a cart already
    2. If not, add a new cart (empty) list to the session
    3. Append the melon id under consideration to our cart list
    4. Flash a message indicating the melon was successfully added to the cart
    5. Redirect the user to the shopping cart page

2.  Display the cart contents.
    
    Displaying the contents of the cart is a little simpler, but is an exercise in fiddling with Jinja templates and HTML tags. Essentially, in our shopping cart page, we will loop through all the melons in our cart and display them in a table.
    1. In our cart controller, get a list of melon ids in the cart out of the session (if it exists)
    2. Query the database for all melons that match the ids in the list
    3. Pass the list of melons on to the shopping cart template
    4. In the shopping cart template, delete the placeholder rows
    5. Use a jinja for loop to iterate through the melon list, outputting each melon to the table in place of the original placeholders.

With each part of the feature being reasonably complex, it makes sense to do them in stages. For example, you might go through this sequence instead:

1. On adding an item, add some arbitrary string to the session
2. In the shopping cart page, add some code to display the string from the session.
3. Going back to the `add_to_cart` controller, replace the string with the actual melon object
4. Going back to the shopping cart page, rewrite the page to display the single melon object
5. In the `add_to_cart` controller, replace the single melon with a melon list...

And so on.

Extra Credit: Log In
--------------------
We'll implement a very simple login feature (that doesn't do anything) using all the same mechanisms we've seen until now. Exactly 'which user is logged in right now' is a good candidate for being stored in the session, as it's very browser-specific information. The general procedure is as follows

1. When the user submits the login form, the email address and password get sent to the `process_login` controller.
2. From the `process_login` controller, we can extract the form fields from the [request object](http://flask.pocoo.org/docs/quickstart/#the-request-object).
3. We can use the submitted email to look up whether or not that user exists in the database (fill in the details of the `Customer` class and the `get_customer_by_email` function).
4. If the customer exists, store the customer in the session. For this exercise, we will ignore whether or not the password matches.
5. In our templates, if a customer is logged in (ie: they exist in the session), display their name and an option to log out instead of the login link.
6. Flash a login successful message.
7. Redirect the user to the main melon listings.
