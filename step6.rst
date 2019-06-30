.. include:: cyverse_rst_defined_substitutions.txt

|CyVerse logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_


Data cleaning with Tidyverse dplyr
-----------------------------------

.. admonition:: learning-objectives

  - Describe what the dplyr package in R is used for.
  - Apply common dplyr functions to manipulate data in R.
  - Use the ‘pipe’ operator to link together a sequence of functions.
  - Use the ‘mutate’ function to apply other chosen functions to existing
    columns and create new columns of data.
  - Use the ‘split-apply-combine’ concept to split the data into groups,
    apply analysis to each group, and combine the results.

`dplyr` is a package for
making data manipulation easier.

Packages in R are basically sets of additional functions that let you do more
stuff in R. The functions we've been using, like `str()`, come built into R;
packages give you access to more functions. You need to install a package and
then load it to be able to use it.

.. code-block:: R

  install.packages("dplyr") ## install

You might get asked to choose a CRAN mirror -- this is basically asking you to
choose a site to download the package from. The choice doesn't matter too much;
The RStudio mirror is recommended.

.. code-block:: R

  library("dplyr") ## load

You only need to install a package once per computer, but you need to load it
every time you open a new R session and want to use that package.

What is dplyr?
~~~~~~~~~~~~~~~~

The package `dplyr` is a package that tries to provide easy tools for the most
common data manipulation tasks. It is built to work directly
with data frames. The thinking behind it was largely inspired by the package
`plyr` which has been in use for some time but suffered from being slow in some
cases.` dplyr` addresses this by porting much of the computation to C++. An
additional feature is the ability to work with data stored directly in an
external database. The benefits of doing this are that the data can be managed
natively in a relational database, queries can be conducted on that database,
and only the results of the query returned.

This addresses a common problem with R in that all operations are conducted in
memory and thus the amount of data you can work with is limited by available
memory. The database connections essentially remove that limitation in that you
can have a database of many 100s GB, conduct queries on it directly and pull
back just what you need for analysis in R.

Selecting columns and filtering rows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We're going to learn some of the most common `dplyr` functions: `select()`,
`filter()`, `mutate()`, `group_by()`, and `summarize()`. To select columns of a
data frame, use `select()`. The first argument to this function is the data
frame (`metadata`), and the subsequent arguments are the columns to keep.

.. code-block:: R

  select(metadata, sample, clade, cit, genome_size)


To choose rows, use `filter()`:

.. code-block:: R

  filter(metadata, cit == "plus")

Pipes
~~~~~~~~

But what if you wanted to select and filter? There are three ways to do this:
use intermediate steps, nested functions, or pipes. With the intermediate steps,
you essentially create a temporary data frame and use that as input to the next
function. This can clutter up your workspace with lots of objects. You can also
nest functions (i.e. one function inside of another).  This is handy, but can be
difficult to read if too many functions are nested as the process from inside
out. The last option, pipes, are a fairly recent addition to R. Pipes let you
take the output of one function and send it directly to the next, which is
useful when you need to many things to the same data set.  Pipes in R look like
`%>%` and are made available via the `magrittr` package installed as
part of `dplyr`.

.. code-block:: R

  metadata %>%
    filter(cit == "plus") %>%
    select(sample, generation, clade)


In the above we use the pipe to send the `metadata` data set first through
`filter`, to keep rows where `cit` was equal to 'plus', and then through `select` to
keep the `sample` and `generation` and `clade` columns. When the data frame is being passed to the
`filter()` and `select()` functions through a pipe, we don't need to include it
as an argument to these functions anymore.

If we wanted to create a new object with this smaller version of the data we
could do so by assigning it a new name:

.. code-block:: R

  meta_citplus <- metadata %>%
    filter(cit == "plus") %>%
    select(sample, generation, clade)

    meta_citplus


.. admonition:: Question

  Using pipes, subset the data to include rows where the clade is 'Cit+'.
  Retain columns: `sample`, `cit`, and `genome_size.`

  .. admonition:: answer

    .. code-block:: R

      metadata %>%
        filter(clade == "Cit+") %>%
        select(sample, cit, genome_size)

Mutate
~~~~~~~~

Frequently you'll want to create new columns based on the values in existing
columns, for example to do unit conversions or find the ratio of values in two
columns. For this we'll use `mutate()`.

To create a new column of genome size in bp:

.. code-block:: R

  metadata %>%
    mutate(genome_bp = genome_size *1e6)


If this runs off your screen and you just want to see the first few rows, you
can use a pipe to view the `head()` of the data (pipes work with non-dplyr
functions too, as long as the `dplyr` or `magrittr` packages are loaded).

.. code-block:: R

  metadata %>%
    mutate(genome_bp = genome_size *1e6) %>%
    head

The row has a NA value for clade, so if we wanted to remove those we could
insert a `filter()` in this chain:

.. code-block:: R

  metadata %>%
    mutate(genome_bp = genome_size *1e6) %>%
    filter(!is.na(clade)) %>%
    head


`is.na()` is a function that determines whether something is or is not an `NA`.
The `!` symbol negates it, so we're asking for everything that is not an `NA`.

Split-apply-combine data analysis and the summarize() function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Many data analysis tasks can be approached using the "split-apply-combine"
paradigm: split the data into groups, apply some analysis to each group, and
then combine the results. `dplyr` makes this very easy through the use of the
`group_by()` function, which splits the data into groups. When the data is
grouped in this way `summarize()` can be used to collapse each group into
a single-row summary.  `summarize()` does this by applying an aggregating
or summary function to each group. For example, if we wanted to group by
citrate-using mutant status and find the number of rows of data for each
status, we would do:

.. code-block:: R

  metadata %>%
    group_by(cit) %>%
    summarize(n())

Here the summary function used was `n()` to find the count for each
group. We can also apply many other functions  to individual columns
to get other summary statistics.
For example, in the R base package we can use built-in functions like
`mean`, `median`, `min`, and `max`.  By default, all **R functions
operating on vectors that contains missing data will return NA**.
It's a way to make sure that users know they have missing
data, and make a conscious decision on how to deal with it. When
dealing with simple statistics like the mean, the easiest way to
ignore `NA` (the missing data) is to use `na.rm=TRUE` (`rm` stands for
remove).

So to view mean `genome_size` by mutant status:

.. code-block:: R

  metadata %>%
    group_by(cit) %>%
    summarize(mean_size = mean(genome_size, na.rm = TRUE))


You can group by multiple columns too:

.. code-block:: R

  metadata %>%
    group_by(cit, clade) %>%
    summarize(mean_size = mean(genome_size, na.rm = TRUE))

Looks like for one of these clones, the clade is missing. We could then discard those rows using `filter()`:

.. code-block:: R

  metadata %>%
    group_by(cit, clade) %>%
    summarize(mean_size = mean(genome_size, na.rm = TRUE)) %>%
    filter(!is.na(clade))


All of a sudden this isn't running off the screen anymore. That's because `dplyr`
has changed our `data.frame` to a `tbl_df`. This is a data structure that's very
similar to a data frame; for our purposes the only difference is that it won't
automatically show tons of data going off the screen.

You can also summarize multiple variables at the same time:

.. code-block:: R

  metadata %>%
    group_by(cit, clade) %>%
    summarize(mean_size = mean(genome_size, na.rm = TRUE),
              min_generation = min(generation))

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



.. Comment: Place URLS Below This Line

   # Use this example to ensure that links open in new tabs, avoiding
   # forcing users to leave the document, and making it easy to update links
   # In a single place in this document

   .. |Substitution| raw:: html # Place this anywhere in the text you want a hyperlink

      <a href="REPLACE_THIS_WITH_URL" target="blank">Replace_with_text</a>


.. |Github Repo Link|  raw:: html

   <a href="https://github.com/CyVerse-learning-materials/240-minute-r-tutorial" target="blank">Github Repo Link</a>
