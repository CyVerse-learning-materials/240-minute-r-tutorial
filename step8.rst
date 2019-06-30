.. include:: cyverse_rst_defined_substitutions.txt

|CyVerse logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

Getting help with R
-----------------------

.. admonition:: learning-objectives

  - Be able to ask effective questions when searching for help on forums or using web
    searches
  - Check the version of R and display session info
  - Know important learning resources

Getting help with R
~~~~~~~~~~~~~~~~~~~~~~

|oreilly_book_covers.png|

No matter how much experience you have with R, you will find yourself
needing help. There is no shame in researching how to do something in R, and
most people will find themselves looking up how to do the same things that
they "should know how to do" over and over again. Here are some tips to make
this process as helpful and efficient as possible.

.. tip::

    Never memorize something that you can look up"
    - A. Einstein

Finding help on Stackoverflow and Biostars
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Two popular websites will be of great help with many R problems. For **general**
**R questions**, |Stack Overflow| is probably the most popular online community
for developers. If you start your question "How to do X in R" results from Stack
Overflow are usually near the top of the list. For **bioinformatics specific questions**,
|Biostars| is a popular online forum.

.. tip::

    **Asking for help using online forums**

  - When searching for R help, look for answers with the |r| tag
  - Get an account; not required to view answers but to required to post
  - Put in effort to check thoroughly before you post a question; folks get
    annoyed if you ask a very common question that has been answered multiple
    times
  - Be careful. While forums are very helpful, you can't know for sure if the
    advice you are getting is correct
  - See the |How to ask for R help| blog post for more useful tips



Help people help you
~~~~~~~~~~~~~~~~~~~~~

Often, in order to duplicate the issue you are having, someone may need to see
the data you are working with or verify the versions of R or R packages you
are using. The following R functions will help with this:

You can **check the version of R** you are working with using the `sessionInfo()`
function. Actually, it is good to save this information as part of your notes
on any analysis you are doing. When you run the same script that has worked fine
a dozen times before, looking back at these notes will remind you that you
upgraded R and forget to check your script.


.. code-block:: R

  sessionInfo()


Many times, there may be some issues with your data and the way it is formatted.
In that case, you may want to share that data with someone else. However, you
may not need to share the whole dataset; looking at a subset of your 50,000 row,
10,000 column data frame may be TMI (too much information)! You can take an
object you have in memory such as data frame (if you don't know what this means
yet, we will get to it!) and save it to a file. In our example we will use the
`dput()` function on the `iris` data frame which is an example dataset that is
installed in R:


.. code-block:: R

  dput(head(iris)) # iris is an example data.frame that comes with R
                   # the `head()` function just takes the first 6 lines of the iris dataset


This generates some output (below) which you will be better able to interpret
after covering the other R lessons. This info would be helpful in understanding
how the data is formatted and possibly revealing problematic issues.

Alternatively, you can also save objects in R memory to a file by specifying
the name of the object, in this case the `iris` data frame, and passing a
filename to the `file=` argument.

.. code-block:: R

    saveRDS(iris, file="iris.rds") # By convention, we use the .rds file extension


Final FAQs on R
~~~~~~~~~~~~~~~~~

Finally, here are a few pieces of introductory R knowledge that are too good to
pass up. While we won't return to them in this course, we put them here because
they come up commonly:

**Do I need to click Run every time I want to run a script?**

- No. In fact, the most common shortcut key allows you to run a command (or
  any lines of the script that are highlighted):

  - Windows execution shortcut: :guilabel:`&Ctrl` + :guilabel:`&Enter`
  - Mac execution shortcut: :guilabel:`&Cmd(⌘)` + :guilabel:`&Enter`

  To see a complete list of shortcuts, click on the :guilabel:`&Tools` menu and
  select :guilabel:`&Keyboard Shortcuts Help`

**What's with the brackets in R console output?**

R returns an index with your result. When your result contains multiple values,
the number tells you what ordinal number begins the line, for example:

.. code-block:: R

  1:101 # generates the sequence of numbers from 1 to 101


In the output, `[81]` indicates that the first value on that line is the
81st item in your result


**Can I run my R script without RStudio?**

- Yes, remember - RStudio is running R. You get to use lots of the enhancements
  RStudio provides, but R works independent of RStudio. See |these tips|
  for running your commands at the command line

**Where else can I learn about RStudio?**
- Check out the :guilabel:`&Help` menu, especially "Cheatsheets" section

**What are some other important resources for learning R?**

 - |Data Carpentry| has lessons and you can request or help organize a workshop
 - |R for Data Science| is an excellent introduction to R and Tidyverse


----

**Fix or improve this documentation**

Search for an answer:
|CyVerse Learning Center| or
|CyVerse Wiki|

----

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

.. Comment: Place Images Below This Line
   use :width: to give a desired width for your image
   use :height: to give a desired height for your image
   replace the image name/location and URL if hyperlinked


 .. |Clickable hyperlinked image| image:: ./img/IMAGENAME.png
    :width: 500
    :height: 100
 .. _CyVerse logo: http://learning.cyverse.org/

 .. |Static image| image:: ./img/IMAGENAME.png
    :width: 25
    :height: 25

.. |oreilly_book_covers.png| image:: ./img/oreilly_book_covers.png
    :width: 600

.. Comment: Place URLS Below This Line

   # Use this example to ensure that links open in new tabs, avoiding
   # forcing users to leave the document, and making it easy to update links
   # In a single place in this document

   .. |Substitution| raw:: html # Place this anywhere in the text you want a hyperlink

      <a href="REPLACE_THIS_WITH_URL" target="blank">Replace_with_text</a>


.. |Github Repo Link|  raw:: html

   <a href="https://github.com/CyVerse-learning-materials/240-minute-r-tutorial" target="blank">Github Repo Link</a>

.. |r|  raw:: html

   <a href="https://stackoverflow.com/questions/tagged/r" target="blank">r</a>

.. |Stack Overflow|  raw:: html

   <a href="https://stackoverflow.com/" target="blank">Stack Overflow</a>

.. |Biostars|  raw:: html

   <a href="https://www.biostars.org/" target="blank">Biostars</a>

.. |How to ask for R help|  raw:: html

   <a href="http://blog.revolutionanalytics.com/2014/01/how-to-ask-for-r-help.html" target="blank">How to ask for R help</a>

.. |these tips|  raw:: html

   <a href="https://support.rstudio.com/hc/en-us/articles/218012917-How-to-run-R-scripts-from-the-command-line" target="blank">these tips</a>

.. |Data Carpentry|  raw:: html

   <a href="https://datacarpentry.org/" target="blank">Data Carpentry</a>

.. |R for Data Science|  raw:: html

   <a href="https://r4ds.had.co.nz/" target="blank">R for Data Science</a>
