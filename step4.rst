.. include:: cyverse_rst_defined_substitutions.txt

|CyVerse logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_


Fundamental objects in R
---------------------------

.. admonition:: learning-objectives

  - "Be able to create the most common R objects including vectors"
  - "Understand that vectors have modes, which correspond to the type of data
    they
    contain"
  - "Be able to use arithmetic operators on R objects"
  - "Be able to retrieve (subset), name, or replace, values from a vector"
  - "Be able to use logical operators in a subsetting operation"

Creating objects in R
~~~~~~~~~~~~~~~~~~~~~~~~~

What might be called a variable in many languages is called an **object**
in R.

**To create an object you need:**

- a name (e.g. 'a')
- a value (e.g. '1')
- the assignment operator ('<-')

In your script, "**r_basics.R**", using the R assignment operator '<-',
assign '1' to the object 'a' as shown. Remember to leave a comment in the line
above (using the '#') to explain what you are doing:

.. code-block:: R

  # this line creates the object 'a' and assigns it the value '1'

  a <- 1


Next, run this line of code in your script. You can run a line of code
by hitting the <KBDRun</KBD button that is just above the first line of your
script in the header of the Source pane or you can use the appropriate shortcut:

- Windows execution shortcut: :guilabel:`&Ctrl` + :guilabel:`&Enter`
- Mac execution shortcut: :guilabel:`&Cmd(⌘)` + :guilabel:`&Enter`

To run multiple lines of code, you can highlight all the line you wish to run
and then hit :guilabel:`&Run` or use the shortcut key combo listed above.

In the RStudio 'Console' you should see:

.. code-block:: R

  a <- 1


The 'Console' will display lines of code run from a script and any outputs or
status/warning/error messages (usually in red).

In the 'Environment' window you will also get a table:

.. list-table::
    :header-rows: 1

    * - Values
      -
    * - a
      - 1


The 'Environment' window allows you to keep track of the objects you have
created in R.

.. admonition:: Question

  **Create some objects in R**

   Create the following objects; give each object an appropriate name
   (your best guess at what name to use is fine):

   1. Create an object that has the value of number of pairs of human
      chromosomes
   2. Create an object that has a value of your favorite gene name
   3. Create an object that has this URL as its value: "ftp://ftp.ensemblgenomes.org/pub/bacteria/release-39/fasta/bacteria_5_collection/escherichia_coli_b_str_rel606/"
   4. Create an object that has the value of the number of chromosomes in a
      diploid human cell

 .. admonition:: Answer

     Here as some possible answers to the challenge:

     .. code-block:: R

         human_chr_number <- 23
         gene_name <- 'pten'
         ensemble_url <- 'ftp://ftp.ensemblgenomes.org/pub/bacteria/release-39/fasta/bacteria_5_collection/escherichia_coli_b_str_rel606/'
         human_diploid_chr_num <-  2 * human_chr_number


Naming objects in R
~~~~~~~~~~~~~~~~~~~~~~

Here are some important details about naming objects in R.

- **Avoid spaces and special characters**: Object names cannot contain spaces or
  the minus sign (`-`). You can use '_' to make names more readable. You should
  avoid using special characters in your object name (e.g. ! @ # . , etc.).
  Also, object names cannot begin with a number.
- **Use short, easy-to-understand names**: You should avoid naming your objects
  using single letters (e.g. 'n', 'p', etc.). This is mostly to encourage you
  to use names that would make sense to anyone reading your code (a colleague,
  or even yourself a year from now). Also, avoiding excessively long names will
  make your code more readable.
- **Avoid commonly used names**: There are several names that may already have a
  definition in the R language (e.g. 'mean', 'min', 'max'). One clue that a name
  already has meaning is that if you start typing a name in RStudio and it gets
  a colored highlight or RStudio gives you a suggested autocompletion you have
  chosen a name that has a reserved meaning.
- **Use the recommended assignment operator**: In R, we use '<- ' as the
  preferred assignment operator. '=' works too, but is most commonly used in
  passing arguments to functions (more on functions later). There is a shortcut
  for the R assignment operator:
  - Windows execution shortcut: :guilabel:`&Alt` + :guilabel:`&-`
  - Mac execution shortcut: :guilabel:`&Option` + :guilabel:`&-`

There are a few more suggestions about naming and style you may want to learn
more about as you write more R code. There are several "style guides" that
have advice, and one to start with is the |tidyverse R style guide|.

 .. Tip::

   **Pay attention to warnings in the script console**

   If you enter a line of code in your script that contains an error, RStudio
   may give you an error message and underline this mistake. Sometimes these
   messages are easy to understand, but often the messages may need some
   figuring out. Paying attention to these warnings will help you avoid
   mistakes. In the example below, our object name has a space, which is not
   allowed in R. The error message does not say this directly, but R is "not
   sure" about how to assign the name to "human\_ chr_number" when the object
   name we want is "human_chr_number".

   |rstudio_script_warning|


Reassigning object names or deleting objects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once an object has a value, you can change that value by overwriting it. R will
not give you a warning or error if you overwriting an object, which may or may
not be a good thing depending on how you look at it.

.. code-block:: R

    # gene_name has the value 'pten' or whatever value you used in the challenge.
    # We will now assign the new value 'tp53'
    gene_name <- 'tp53'


You can also remove an object from R's memory entirely. The `rm()` function
will delete the object.

.. code-block:: R

    # delete the object 'gene_name'
    rm(gene_name)


If you run a line of code that has only an object name, R will normally display
the contents of that object. In this case, we are told the object no longer
exists.

.. code-block:: R

  Error: object 'gene_name' not found

Understanding object data types (modes)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In R, **every object has two properties**:

- **Length**: How many distinct values are held in that object
- **Mode**: What is the classification (type) of that object.

We will get to the "length" property later in the lesson. The **"mode" property**
**corresponds to the type of data an object represents**. The most common modes
you will encounter in R are:

.. list-table::
    :header-rows: 1

    * - Mode (abbreviation)
      - Type of data
    * - Numeric (num)
      - Numbers such floating point/decimals (1.0, 0.5, 3.14),
        there are also more specific numeric types (dbl - Double,
        int - Integer). These differences are not relevant for
        most beginners and pertain to how these values are
        stored in memory
    * - Character (chr)
      - A sequence of letters/numbers in single '' or double " " quotes
    * - Logical
      - Boolean values - TRUE or FALSE

There are a few other modes (i.e. "complex", "raw" etc.) but these
are the three we will work with in this lesson.

Data types are familiar in many programming languages, but also in natural
language where we refer to them as the parts of speech, e.g. nouns, verbs,
adverbs, etc. Once you know if a word - perhaps an unfamiliar one - is a noun,
you can probably guess you can count it and make it plural if there is more than
one (e.g. 1 |Tuatara|, or 2 Tuataras). If something is a adjective, you can
usually change it into an adverb by adding "-ly" (e.g. |jejune| vs.
jejunely). Depending on the context, you may need to decide if a word is in one
category or another (e.g "cut" may be a noun when it's on your finger, or a verb
when you are preparing vegetables). These concepts have important analogies when
working with R objects.

.. admonition:: Question

  **Exercise: Create objects and check their modes**

   Create the following objects in R, then use the `mode()` function to verify
   their modes. Try to guess what the mode will be before you look at the solution

   1. `chromosome_name <- 'chr02'`
   2. `od_600_value <- 0.47`
   3. `chr_position <- '1001701'`
   4. `spock <- TRUE`
   5. `pilot <- Earhart`

   .. admonition:: Answer

    .. code-block:: R

       chromosome_name <- 'chr02'
       od_600_value <- 0.47
       chr_position <- '1001701'
       spock <- TRUE
       pilot <- Earhart

    .. code-block:: R

       mode(chromosome_name)
       mode(od_600_value)
       mode(chr_position)
       mode(spock)
       mode(pilot)


Notice from the solution that even if a series of numbers are given as a value
R will consider them to be in the "character" mode if they are enclosed as
single or double quotes. Also, notice that you cannot take a string of
alphanumeric characters (e.g. Earhart) and assign as a value for an object. In
this case, R looks for an object named `Earhart` but since there is no object,
no assignment can be made. If `Earhart` did exist, then the mode of `pilot`
would be whatever the mode of `Earhart` was originally. If we want to create an
object called `pilot` that was the **name** "Earhart", we need to enclose
`Earhart` in quotation marks.

.. code-block:: R

    pilot <- "Earhart"
    mode(pilot)

Mathematical and functional operations on objects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once an object exists (which by definition also means it has a mode), R can
appropriately manipulate that object. For example, objects of the numeric modes
can be added, multiplied, divided, etc. R provides several mathematical
(arithmetic) operators including:

.. list-table::
    :header-rows: 1

    * - Operator
      - Description
    * - \+
      - addition
    * - \-
      - subtraction
    * - \*
      - multiplication
    * - /
      - division
    * - ^ or **
      - exponentiation
    * - a%%b
      - modulus (returns the remainder after division)

These can be used with literal numbers:

.. code-block:: R

  (1 + (5 ** 0.5))/2


and importantly, can be used on any object that evaluates to (i.e. interpreted
by R) a numeric object:

.. code-block:: R

  human_chr_number <- 23


.. code-block:: R

  # multiply the object 'human_chr_number' by 2

  human_chr_number * 2


.. admonition:: Question

   **Compute the golden ratio**

   One approximation of the golden ratio (φ) can be found by taking the sum of 1
   and the square root of 5, and dividing by 2 as in the example above. Compute
   the golden ratio to 3 digits of precision using the `sqrt()` and `round()`
   functions. Hint: remember the `round()` function can take 2 arguments.

  .. admonition:: Answer

       .. code-block:: R

        round((1 + sqrt(5))/2, digits = 3)

       Notice that you can place one function inside of another.


Vectors
~~~~~~~~~

Vectors are probably the
most used commonly used object type in R. **A vector is a collection of values that are all of the same type (numbers, characters, etc.)**.
One of the most common ways to create a vector is to use the `c()` function -
the "concatenate" or "combine" function. Inside the function you may enter one
or more values; for multiple values, separate each value with a comma:

.. code-block:: R

  # Create the SNP gene name vector

  snp_genes <- c("OXTR", "ACTN3", "AR", "OPRM1")


Vectors always have a **mode** and a **length**. You can check these with the
`mode()` and `length()` functions respectively. Another useful function that
gives both of these pieces of information is the `str()` (structure) function.

.. code-block:: R

  # Check the mode, length, and structure of 'snp_genes'
  mode(snp_genes)
  length(snp_genes)


Vectors are quite important in R. Another data type that we will work with later
in this lesson, data frames, are collections of vectors. What we learn here
about vectors will pay off even more when we start working with data frames.

Creating and subsetting vectors
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Let's create a few more vectors to play around with:

.. code-block:: R

    # Some interesting human SNPs
    # while accuracy is important, typos in the data won't hurt you here

    snps <- c('rs53576', 'rs1815739', 'rs6152', 'rs1799971')
    snp_chromosomes <- c('3', '11', 'X', '6')
    snp_positions <- c(8762685, 66560624, 67545785, 154039662)


Once we have vectors, one thing we may want to do is specifically retrieve one
or more values from our vector. To do so, we use **bracket notation**. We type
the name of the vector followed by square brackets. In those square brackets
we place the index (e.g. a number) in that bracket as follows:

.. code-block:: R

  # get the 3rd value in the snp_genes vector
  snp_genes[3]

In R, every item your vector is indexed, starting from the first item (1)
through to the final number of items in your vector. You can also retrieve a
range of numbers:

.. code-block:: R

  # get the 1st through 3rd value in the snp_genes vector

  snp_genes[1:3]


If you want to retrieve several (but not necessarily sequential) items from
a vector, you pass a **vector of indices**; a vector that has the numbered
positions you wish to retrieve.

.. code-block:: R

  # get the 1st, 3rd, and 4th value in the snp_genes vector

  snp_genes[c(1, 3, 4)]


There are additional (and perhaps less commonly used) ways of subsetting a
vector (see [these
examples](https://thomasleeper.com/Rcourse/Tutorials/vectorindexing.html)).
Also, several of these subsetting expressions can be combined:

.. code-block:: R

  # get the 1st through the 3rd value, and 4th value in the snp_genes vector
  # yes, this is a little silly in a vector of only 4 values.
  snp_genes[c(1:3,4)]


Adding to, removing, or replacing values in existing vectors
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once you have an existing vector, you may want to add a new item to it. To do
so, you can use the `c()` function again to add your new value:

.. code-block:: R

  # add the gene 'CYP1A1' and 'APOA5' to our list of snp genes
  # this overwrites our existing vector
  snp_genes <- c(snp_genes, "CYP1A1", "APOA5")

We can verify that "snp_genes" contains the new gene entry

.. code-block:: R

  snp_genes


Using a negative index will return a version a vector with that index's
value removed:

.. code-block:: R

  snp_genes[-6]


We can remove that value from our vector by overwriting it with this expression:

.. code-block:: R

    snp_genes <- snp_genes[-6]
    snp_genes

We can also explicitly rename or add a value to our index using bracket
notation:

.. code-block:: R

  snp_genes[7]<- "APOA5"
  snp_genes


Notice in the operation above that R inserts an `NA` value to extend our vector
so that the gene "APOA5" is an index 7. This may be a good or not-so-good thing
depending on how you use this.

.. admonition:: Question


    **Examining and subsetting vectors**
     Answer the following questions to test your knowledge of vectors

     Which of the following are true of vectors in R?

     A) All vectors have a mode **or** a length
     B) All vectors have a mode **and** a length
     C) Vectors may have different lengths
     D) Items within a vector may be of different modes
     E) You can use the `c()` to one or more items to an existing vector
     F) You can use the `c()` to add a vector to an exiting vector

     .. admonition:: Answer

       A) False - Vectors have both of these properties
       B) True
       C) True
       D) False - Vectors have only one mode (e.g. numeric, character); all items in
          a vector must be of this mode.
       E) True
       F) True


Logical Subsetting
~~~~~~~~~~~~~~~~~~~~

There is one last set of cool subsetting capabilities we want to introduce.
It is possible within R to retrieve items in a vector based on a logical
evaluation or numerical comparison. For example, let's say we wanted get
all of the SNPs in our vector of SNP positions that were greater than
100,000,000. We could index using the '' (greater than) logical operator:

.. code-block:: R

  snp_positions[snp_positions  100000000]

In the square brackets you place the name of the vector followed by the
comparison operator and (in this case) a numeric value. Some of the most
common logical operators you will use in R are:

  .. list-table::
      :header-rows: 1

      * - Operator
        - Description
      * - <
        - less than
      * - <=
        - less than or equal to
      * - \>
        - greater than
      * - \>=
        - greater than or equal to
      * - \==
        - exactly equal to
      * - \!=
        - not equal to
      * - \!x
        - not x
      * - a \| b
        - a or b
      * - a \& b
        - a and b

The magic of programming
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The reason why the expression `snp_positions[snp_positions  100000000]` works
can be better understood if you examine what the expression "snp_positions  100000000"
evaluates to:

.. code-block:: R

  snp_positions  100000000


The output above is a logical vector, the 4th element of which is TRUE. When
you pass a logical vector as an index, R will return the true values:

.. code-block:: R

  snp_positions[c(FALSE, FALSE, FALSE, TRUE)]


If you have never coded before, this type of situation starts to expose the
"magic" of programming. We mentioned before that in the bracket notation you
take your named vector followed by brackets which contain an index:
**named_vector[index]**. The "magic" is that the index needs to *evaluate to*
a number. So, even if it does not appear to be an integer (e.g. 1, 2, 3), as
long as R can evaluate it, we will get a result. That our expression
`snp_positions[snp_positions  100000000]` evaluates to a number can be seen
in the following situation. If you wanted to know which **index** (1, 2, 3, or
4) in our vector of SNP positions was the one that was greater than
100,000,000?

We can use the `which()` function to return the indices of any item that
evaluates as TRUE in our comparison:

.. code-block:: R

    which(snp_positions  100000000)


**Why this is important**

Often in programming we will not know what inputs
and values will be used when our code is executed. Rather than put in a
pre-determined value (e.g 100000000) we can use an object that can take on
whatever value we need. So for example:

.. code-block:: R

  snp_marker_cutoff <- 100000000
  snp_positions[snp_positions  snp_marker_cutoff]


Ultimately, it's putting together flexible, reusable code like this that gets
at the "magic" of programming!


A few final vector tricks
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Finally, there are a few other common retrieve or replace operations you may
want to know about. First, you can check to see if any of the values of your
vector are missing (i.e. are `NA`). Missing data will get a more detailed treatment later,
but the `is.NA()` function will return a logical vector, with TRUE for any NA
value:

.. code-block:: R

  # current value of 'snp_genes':
  # chr [1:7] "OXTR" "ACTN3" "AR" "OPRM1" "CYP1A1" NA "APOA5"

  is.na(snp_genes)


Sometimes, you may wish to find out if a specific value (or several values) is
present a vector. You can do this using the comparison operator `%in%`, which
will return TRUE for any value in your collection that is in
the vector you are searching:

.. code-block:: R

  # current value of 'snp_genes':
  # chr [1:7] "OXTR" "ACTN3" "AR" "OPRM1" "CYP1A1" NA "APOA5"

  # test to see if "ACTN3" or "APO5A" is in the snp_genes vector
  # if you are looking for more than one value, you must pass this as a vector

  c("ACTN3","APOA5") %in% snp_genes

.. admonition:: Question

    **Review Exercise 1**

   What data types/modes are the following vectors?
      a. `snps`
      b. `snp_chromosomes`
      c. `snp_positions`

   .. admonition:: Answer

    .. code-block:: R

       typeof(snps)
       typeof(snp_chromosomes)
       typeof(snp_positions)

.. admonition:: Question

  **Review Exercise 2**

   Add the following values to the specified vectors:
      a. To the `snps` vector add: 'rs662799'
      b. To the `snp_chromosomes` vector add: 11
      c. To the `snp_positions` vector add: 	116792991

   .. admonition:: Answer

     .. code-block:: R

       snps <- c(snps, 'rs662799')
       snps
       snp_chromosomes <- c(snp_chromosomes, "11") # did you use quotes?
       snp_chromosomes
       snp_positions <- c(snp_positions, 116792991)
       snp_positions


.. admonition:: Question

   **Review Exercise 3**

   Make the following change to the `snp_genes` vector:

   Hint: Your vector should look like this in 'Environment':

   `chr [1:7] "OXTR" "ACTN3" "AR" "OPRM1" "CYP1A1" NA "APOA5"`

   If not, recreate the vector by running this expression:

   `snp_genes <- c("OXTR", "ACTN3", "AR", "OPRM1", "CYP1A1", NA, "APOA5")`

      a. Create a new version of `snp_genes` that does not contain CYP1A1 and then
      b. Add 2 NA values to the end of `snp_genes`

   .. admonition:: Answer

     .. code-block:: R

       snp_genes <- snp_genes[-5]
       snp_genes <- c(snp_genes, NA, NA)
       snp_genes

.. admonition:: Question

  **Review Exercise 4**

   Using indexing, create a new vector named `combined` that contains:

      - The the 1st value in `snp_genes`
      - The 1st value in `snps`
      - The 1st value in `snp_chromosomes`
      - The 1st value in `snp_positions`

  .. admonition:: Answer

    .. code-block:: R

       combined <- c(snp_genes[1], snps[1], snp_chromosomes[1], snp_positions[1])
       combined

.. admonition:: Question

   **Review Exercise 5**

   What type of data is `combined`?

  .. admonition:: Answer

    .. code-block:: R

       typeof(combined)

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

.. |rstudio_script_warning| image:: ./img/rstudio_script_warning.png
    :width: 600


.. Comment: Place URLS Below This Line

   # Use this example to ensure that links open in new tabs, avoiding
   # forcing users to leave the document, and making it easy to update links
   # In a single place in this document

   .. |Substitution| raw:: html # Place this anywhere in the text you want a hyperlink

      <a href="REPLACE_THIS_WITH_URL" target="blank">Replace_with_text</a>


.. |Github Repo Link|  raw:: html

   <a href="https://github.com/CyVerse-learning-materials/240-minute-r-tutorial" target="blank">Github Repo Link</a>

.. |tidyverse R style guide|  raw:: html

   <a href="http://style.tidyverse.org/index.html" target="blank">tidyverse R style guide</a>

.. |jejune|  raw:: html

   <a href="https://www.merriam-webster.com/dictionary/jejune" target="blank">jejune</a>

.. |Tuatara|  raw:: html

   <a href="https://en.wikipedia.org/wiki/Tuatara" target="blank">Tuatara</a>
