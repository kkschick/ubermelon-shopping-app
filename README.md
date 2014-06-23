A More Fully Fleshed Web App
============================


Taking Stock
------------
1. Create and activate a new, empty virtual environment
2. Use pip to install the packages required in requirements.txt
3. Run the application with melons.py
4. Explore the application

Things to check out
melons page, for loop

melon detail page, if statement

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
