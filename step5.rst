.. include:: cyverse_rst_defined_substitutions.txt

|CyVerse_logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_


Importing data and working with data frames
-----------------------------------------------
.. admonition:: learning-objectives

  - "Explain the basic principle of tidy datasets"
  - "Be able to load a tabular dataset using base R functions"
  - "Be able to determine the structure of a data frame including its dimensions
    and the datatypes of variables"
  - "Be able to subset/retrieve values from a data frame"
  - "Understand how R may coerce data into different modes"
  - "Be able to change the mode of an object"
  - "Understand that R uses factors to store and manipulate categorical data"
  - "Be able to manipulate a factor, including subsetting and reordering"
  - "Be able to apply an arithmetic function to a data frame"
  - "Be able to coerce the class of an object (including variables in a data frame)"
  - "Be able to import data from Excel"
  - "Be able to save a data frame as a delimited file"

Working with spreadsheets (tabular data)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A substantial amount of the data we work with in genomics will be tabular data,
this is data arranged in rows and columns - also known as spreadsheets. We could
write a whole lesson on how to work with spreadsheets effectively
(|See this Data Carpentry Lesson|). For our purposes, we want to remind you of a
few principles before we work with our first set of example data:

**1) Keep raw data separate from analyzed data**

This is principle number one because if you can't tell which files are the
original raw data, you risk making some serious mistakes (e.g. drawing conclusion
from data which have been manipulated in some unknown way).

**2) Keep spreadsheet data Tidy**

The simplest principle of **Tidy data** is that we have one row in our
spreadsheet for each observation or sample, and one column for every variable
that we measure or report on. As simple as this sounds, it's very easily
violated. Most data scientists agree that significant amounts of their time is
spent tidying data for analysis.

**3) Trust but verify**

Finally, while you don't need to be paranoid about data, you should have a plan
for how you will prepare it for analysis. **This a focus of this lesson.**
You probably already have a lot of intuition, expectations, assumptions about
your data - the range of values you expect, how many values should have
been recorded, etc. Of course, as the data get larger our human ability to
keep track will start to fail (and yes, it can fail for small data sets too).
R will help you to examine your data so that you can have greater confidence
in your analysis, and its reproducibility.

 .. tip::

     **Keeping you raw data separate**

     When you work with data in R, you are not changing the original file you
     loaded that data from. This is different than (for example) working with
     a spreadsheet program where changing the value of the cell leaves you one
     "save"-click away from overwriting the original file. You have to purposely
     use a writing function (e.g. `write.csv()`) to save data loaded into R. In
     that case, be sure to save the manipulated data into a new file. More on this
     later in the lesson.

Importing tabular data into R
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are several ways to import data into R. For our purpose here, we will
focus on using the tools every R installation comes with (so called "base" R) to
import a comma-delimited file containing the results of our variant calling workflow.
We will need to load the sheet using a function called `read.csv()`.

.. admonition:: Question


   **Review the arguments of the `read.csv()` function**

   *Before using the `read.csv()` function, use R's help feature to answer the
   following questions*.

   *Hint*: Entering '?' before the function name and then running that line will
   bring up the help documentation. Also, when reading this particular help
   be careful to pay attention to the 'read.csv' expression under the 'Usage'
   heading. Other answers will be in the 'Arguments' heading.

   A) What is the default parameter for 'header' in the `read.csv()` function?

   B) What argument would you have to change to read a file that was delimited
   by semicolons (;) rather than commas?

   C) What argument would you have to change to read file in which numbers
   used commas for decimal separation (i.e. 1,00)?

   D) What argument would you have to change to read in only the first 10,000 rows
   of a very large file?

   .. admonition:: Answer

     A) The `read.csv()` function has the argument 'header' set to TRUE by default,
     this means the function always assumes the first row is header information,
     (i.e. column names)

     B) The `read.csv()` function has the argument 'sep' set to ",". This means
     the function assumes commas are used as delimiters, as you would expect.
     Changing this parameter (e.g. `sep=";"`) would now interpret semicolons as
     delimiters.

     C) Although it is not listed in the `read.csv()` usage, `read.csv()` is
     a "version" of the function `read.table()` and accepts all its arguments.
     If you set `dec=","` you could change the decimal operator. We'd probably
     assume the delimiter is some other character.

     D) You can set `nrow` to a numeric value (e.g. `nrow=10000`) to choose how
     many rows of a file you read in. This may be useful for very large files
     where not all the data is needed to test some data cleaning steps you are
     applying.

     Hopefully, this exercise gets you thinking about using the provided help
     documentation in R. There are many arguments that exist, but which we wont
     have time to cover. Look here to get familiar with functions you use
     frequently, you may be surprised at what you find they can do.


Now, let's read in the file |Ecoli_metadata.csv|. Right-click to download this
file to your local computer, then in the files pane, use the upload function to
upload this file into your RStudio session.

Next, we need to import into RStudio and save it as a data frame object. We will
use the `read.csv` function to do so.

.. code-block:: R

    ## read in a CSV file and save it as 'variants'

    metadata <- read.csv("../r_learning/Ecoli.metadata.csv")

Alternatively, we can directly import it from a URL like this

.. code-block:: R

  metadata <- read.csv("https://de.cyverse.org/dl/d/48A1073E-88C9-42E6-B3D0-37D73810CC52/Ecoli_metadata.csv")


One of the first things you should notice is that in the Environment window,
you have the `metadata` object, listed as 30 obs. (observations/rows)
of 8 variables (columns). Double-clicking on the name of the object will open
a view of the data in a new tab.

Summarizing and determining the structure of a data frame
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A **data frame is the standard way in R to store tabular data**. A data fame
could also be thought of as a collection of vectors, all of which have the same
length. Using only two functions, we can learn a lot about out data frame
including some summary statistics as well as well as the "structure" of the data
frame. Let's examine what each of these functions can tell us:

.. code-block:: R

  ## get summary statistics on a data frame

  summary(metadata)


Our data frame had 7 variables, so we get 7 fields that summarize the data.
The generation`, and `genome_size` variables are numerical data and so you get
summary statistics on the min and max values for these columns, as well as mean,
median, and interquartile ranges. Other variables (e.g. `clade`) are treated as
categorical data (which have special treatment in R - more on this in a bit).

Before we operate on the data, we also need to know a little more about the
data frame structure to do that we use the `str()` function:

.. code-block:: R

  ## get the structure of a data frame

  str(metadata)


Ok, thats a lot up unpack! Some things to notice.

- the object type `data.frame` is displayed in the first row along with its
  dimensions, in this case 30 observations (rows) and 7 variables (columns)
- Each variable (column) has a name (e.g. `sample`). This is followed
  by the object mode (e.g. factor, int, num, etc.). Notice that before each
  variable name there is a `$` - this will be important later.

Introducing Factors
~~~~~~~~~~~~~~~~~~~~~~

Factors are the final major data structure we will introduce in our R genomics
lessons. Factors can be thought of as vectors which are specialized for
categorical data. Given R's specialization for statistics, this make sense since
categorial and continuous variables usually have different treatments. Sometimes
you may want to have data treated as a factor, but in other cases, this may be
undesirable.

Since some of the data in our data frame are factors, lets see how factors work.
First, we'll extract one of the columns of our data frame to a new object, so
that we don't end up modifying the `metadata` object by mistake.

.. code-block:: R

  ## extract the "sample" column to a new object

  samples <- metadata$sample

Let's look at the first few items in our factor using `head()`:

.. code-block:: R

  head(samples)

What we get back are the items in our factor, and also something called "Levels".
**Levels are the different categories contained in a factor**. By default, R
will organize the levels in a factor in alphabetical order. So the first level
in this factor is "REL606".

Lets look at the contents of a factor in a slightly different way using `str()`:

.. code-block:: R

  str(samples)

For the sake of efficiency, R stores the content of a factor as a vector of
integers, which an integer is assigned to each of the possible levels. Recall
levels are assigned in alphabetical order. In this case, the first item in our
"samples" object is "REL606", which happens to be the 7th level of our factor,
ordered alphabetically.

Subsetting data frames
~~~~~~~~~~~~~~~~~~~~~~~~

Next, we are going to talk about how you can get specific values from data
frames, and where necessary, change the mode of a column of values.

The first thing to remember is that a data frame is two-dimensional (rows and
columns). Therefore, to select a specific value we will will once again use
`[]` (bracket) notation, but we will specify more than one value (except in some cases
where we are taking a range).

.. admonition:: Question


  **Exercise: Subsetting a data frame**

  *Try the following indices and functions and try to figure out what they return*

  a. `metadata[1,1]`

  b. `metadata[2,4]`

  c. `metadata[29,7]`

  d. `metadata[2, ]`

  e. `metadata[-1, ]`

  f. `metadata[1:4,1]`

  g. `metadata[1:10,c("generation","clade")]`

  h. `metadata[,c("sample")]`

  i. `head(metadata)`

  j. `tail(metadata)`

  k. `metadata$sample_id`

  l. `metadata[metadata$sample == "REL10979",]`

The subsetting notation is very similar to what we learned for
vectors. The key differences include:

- Typically provide two values separated by commas: data.frame[row, column]
- In cases where you are taking a continuous range of numbers use a colon
  between the numbers (start:stop, inclusive)
- For a non continuous set of numbers, pass a vector using `c()`
- Index using the name of a column(s) by passing them as vectors using `c()`

Finally, in all of the subsetting exercises above, we printed values to
the screen. You can create a new data frame object by assigning
them to a new object name:

.. code-block:: R

  # create a new data frame containing only observations from cit+ strains

  cit_plus_strains <- metadata[metadata$cit == "plus",]

  # check the dimension of the data frame

  dim(cit_plus_strains)

  # get a summary of the data frame

  summary(cit_plus_strains)

Coercing values in data frames
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. Tip::

  **Coercion isn't limited to data frames**

  While we are going to address coercion in the context of data frames
  most of these methods apply to other data structures, such as vectors


Sometimes, it is possible that R will misinterpret the type of data represented
in a data frame, or store that data in a mode which prevents you from
operating on the data the way you wish. For example, a long list of gene names
isn't usually thought of as a categorical variable, the way that your
experimental condition (e.g. control, treatment) might be. More importantly,
some R packages you use to analyze your data may expect characters as input,
not factors. At other times (such as plotting or some statistical analyses) a
factor may be more appropriate. Ultimately, you should know how to change the
mode of an object.

First, its very important to recognize that coercion happens in R all the time.
This can be a good thing when R gets it right, or a bad thing when the result
is not what you expect. Consider:

.. code-block:: R

  snp_chromosomes <- c('3', '11', 'X', '6')
  typeof(snp_chromosomes)

Although there are several numbers in our vector, they are all in quotes, so
we have explicitly told R to consider them as characters. However, even if we removed
the quotes from the numbers, R would coerce everything into a character:

.. code-block:: R

  snp_chromosomes_2 <- c(3, 11, 'X', 6)
  typeof(snp_chromosomes_2)
  snp_chromosomes_2[1]


We can use the `as.` functions to explicitly coerce values from one form into
another. Consider the following vector of characters, which all happen to be
valid numbers:

.. code-block:: R

  snp_positions_2 <- c("8762685", "66560624", "67545785", "154039662")
  typeof(snp_positions_2)
  snp_positions_2[1]


Now we can coerce `snp_positions_2` into a numeric type using `as.numeric()`:

.. code-block:: R

  snp_positions_2 <- as.numeric(snp_positions_2)
  typeof(snp_positions_2)
  snp_positions_2[1]


Sometimes coercion is straight forward, but what would happen if we tried
using `as.numeric()` on `snp_chromosomes_2`

.. code-block:: R

  snp_chromosomes_2 <- as.numeric(snp_chromosomes_2)

If we check, we will see that an `NA` value (R's default value for missing
data) has been introduced.

.. code-block:: R

  snp_chromosomes_2


Trouble can really start when we try to coerce a factor. For example, when we
try to coerce the `sample_id` column in our data frame into a numeric mode
look at the result:

.. code-block:: R

  as.numeric(metadata$sample)


Strangely, it works! Almost. Instead of giving an error message, R returns
numeric values, which in this case are the integers assigned to the levels in
this factor. This kind of behavior can lead to hard-to-find bugs, for example
when we do have numbers in a factor, and we get numbers from a coercion. If
we don't look carefully, we may not notice a problem.

If you need to coerce an entire column you can overwrite it using an expression
like this one:

.. code-block:: R

  # make the 'sample' column a character type column

  metadata$sample <- as.character(metadata$sample)

  # check the type of the column
  typeof(metadata$sample)


StringsAsFactors = FALSE
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lets summarize this section on coercion with a few take home messages.

- When you explicitly coerce one data type into another (this is known as
  **explicit coercion**), be careful to check the result. Ideally, you should
  try to see if its possible to avoid steps in your analysis that force you to
  coerce.
- R will sometimes coerce without you asking for it. This is called
  (appropriately) **implicit coercion**. For example when we tried to create
  a vector with multiple data types, R chose one type through implicit
  coercion.
- Check the structure (`str()`) of your data frames before working with them!

Regarding the first bullet point, one way to avoid needless coercion when
importing a data frame using any one of the `read.table()` functions such as
`read.csv()` is to set the argument `StringsAsFactors` to FALSE. By default,
this argument is TRUE. Setting it to FALSE will treat any non-numeric column to
a character type. `read.csv()` documentation, you will also see you can
explicitly type your columns using the `colClasses` argument. Other R packages
(such as the Tidyverse "readr") don't have this particular conversion issue,
but many packages will still try to guess a  data type.

Data frame bonus material: math, sorting, renaming
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Here are a few operations that don't need much explanation, but which are good
to know.

There are lots of arithmetic functions you may want to apply to your data
frame, covering those would be a course in itself. Here are some additional
summary statistical functions.

You can use functions like `mean()`, `min()`, `max()` on an individual column.
Let's look at the "DP" or filtered depth. This value shows the number of filtered
reads that support each of the reported variants.

.. code-block:: R

  max(metadata$generation)


You can sort a data frame using the `order()` function:

.. code-block:: R

  metadata_sorted_by_genome_size<- metadata[order(metadata$genome_size), ]
  head(metadata_sorted_by_generation$genome_size)

Saving your data frame to a file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We can save data to a file. We will save our `metadata_sorted_by_genome_size`
object to a .csv file using the `write.csv()` function:

.. code-block:: R

  write.csv(metadata_sorted_by_genome_size, file = "metadata_sorted_by_genome_size.csv")


The `write.csv()` function has some additional arguments listed in the help, but
at a minimum you need to tell it what data frame to write to file, and give a
path to a file name in quotes (if you only provide a file name, the file will
be written in the current working directory).

Importing data from Excel
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Excel is one of the most common formats, so we need to discuss how to make
these files play nicely with R. The simplest way to import data from Excel is
to **save your Excel file in .csv format**. You can then import into R right
away. Sometimes you may not be able to do this (imagine you have data in 300
Excel files, are you going to open and export all of them?).

One common R package (a set of code with features you can download and add to
your R installation) is the |readxl package| which can open and import Excel
files. Rather than addressing package installation this second (we'll discuss
this soon!), we can take advantage of RStudio's import feature which integrates
this package. (Note: this feature is available only in the latest versions of
RStudio such as is installed on our cloud instance).

First, download this sample Excel file |sequencing_results.metadata.xls| to your
local computer.


In the RStudio menu go to **File**, select **Import Dataset**, and
choose **From Excel...** (notice there are several other options you can
explore). Say yes to install the required packages.

Next, under **File/Url:** click the Browse button and navigate to the
**sequencing_results.metadata.xls** file. You should now see a preview of the
data to be imported.

Notice that you have the option to change the data type of each variable by
clicking arrow (drop-down menu) next to each column title. Under **Import
Options** you may also rename the data, choose a different sheet to import, and
choose how you will handle headers and skipped rows. Under **Code Preview** you
can see the code that will be used to import this file. We could have written
this code and imported the Excel file without the RStudio import function, but
now you can choose your preference.

In this exercise, we will leave the title of the data frame as
**sequencing_results.metadata**, and there are no other options we need to
adjust. Click the Import button to import the data.

Finally, let's check the first few lines of the `sequencing_results.metadata.xls`
data frame:

.. code-block:: R

    head(sequencing_results_metadata)


The type of this object is 'tibble', a type of data
frame we will talk more about in the 'dplyr' section. If you needed
a true R data frame you could coerce with `as.data.frame()`.

----

**Fix or improve this documentation**

- Search for an answer:
  |CyVerse Learning Center|
- Ask us for help:
  click |Intercom| on the lower right-hand side of the page
- Report an issue or submit a change:
  |Github Repo Link|
- Send feedback: `Tutorials@CyVerse.org <Tutorials@CyVerse.org>`_




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

.. |See this Data Carpentry Lesson|  raw:: html

   <a href="https://datacarpentry.org/organization-genomics/" target="blank">See this Data Carpentry Lesson</a>

.. |Ecoli_metadata.csv| raw:: html

   <a href="https://de.cyverse.org/dl/d/48A1073E-88C9-42E6-B3D0-37D73810CC52/Ecoli_metadata.csv" target="blank">Ecoli_metadata.csv</a>

.. |readxl package| raw:: html

   <a href="https://CRAN.R-project.org/package=readxl" target="blank">readxl package</a>

.. |sequencing_results.metadata.xls| raw:: html

   <a href="https://de.cyverse.org/dl/d/5EA67A1B-69F8-4172-88C9-84EC668A3200/sequencing_results_metadata.xls" target="blank">sequencing_results.metadata.xls</a>
