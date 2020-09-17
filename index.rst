.. include:: cyverse_rst_defined_substitutions.txt

|CyVerse_logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

|condensedR|

**Condensed R: 240-Minute R Tutorial**
=========================================

Goal
----

This tutorial is designed for learners with little to no programming or R
experience and prepares them to learn more about R on their own. We'll introduce
some of the most useful features of R for the analysis of biological data.

 .. note::
	 This tutorial was prepared for presentation with an experienced R instructor.
	 Self-guided learners should also find this tutorial useful.



----

.. toctree::
	:maxdepth: 2

	Tutorial home <self>
	Introduction <step1.rst>
	R and RStudio basics <step2.rst>
	Understanding basic R functions <step3.rst>
	Fundamental objects in R <step4.rst>
  Importing data and working with data frames <step5.rst>
  Data cleaning with Tidyverse dplyr <step6.rst>
	Visualization basics <step7.rst>
	Getting help with R <step8.rst>



..
	#### Comment:This tutorial can have multiple pages. The table of contents assumes
	you have an additional page called 'Step One' with content located in 'step1.rst'
	Edit these titles and filenames as needed ####


Prerequisites
-------------

Downloads, access, and services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*In order to complete this tutorial you will need access to the following services/software*

..
	#### comment: delete any row not needed in this table ####

.. list-table::
    :header-rows: 1

    * - Prerequisite
      - Preparation/Notes
      - Link/Download
    * - CyVerse account
      - We will use CyVerse VICE to complete this tutorial. This will eliminate
        the time consuming step of having each learner install R on their own.
      - |CyVerse User Portal|
    * - [Optional] Install R
      - If not using the CyVerse VICE app, you will need to install R on your
        own computer. You can follow instructions at this link to install R on
        your own computer.
      - |Project R|
    * - [Optional] RStudio
      - If not using the CyVerse VICE app, you will need to install RStudio on
        your own computer. You can follow instructions at this link to install
        RStudio on your own computer. (Choose the free "RStudio Desktop")
      - |RStudio|

Platform(s)
~~~~~~~~~~~

*We will use the following CyVerse platform(s):*

 ..
   #### comment: delete any row not needed in this table ####

.. list-table::
    :header-rows: 1

    * - Platform
      - Interface
      - Link
      - Platform Documentation
      - Quick Start
    * - Data Store
      - GUI/Command line
      - |Data Store|
      - |Data Store Manual|
      - |Data Store Guide|
    * - Discovery Environment
      - Web/Point-and-click
      - |Discovery Environment|
      - |DE Manual|
      - |Discovery Environment Guide|


Application(s) used
~~~~~~~~~~~~~~~~~~~
..
	#### Comment: these tables are examples, delete whatever is unnecessary ####

**Discovery Environment App(s):**

.. list-table::
    :header-rows: 1

    * - App name
      - Version
      - Description
    * - rstudio-3.5.0
      - 3.5.0
      - RStudio


Credits and attributions
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Material for this tutorial is credited to the Data Carpentry Genomics R lessons
(https://datacarpentry.org/genomics-r-intro/index.html)
As well as materials from Jeff Holister's R Tutorial
(http://usepa.github.io/introR/2015/01/14/03-Clean/)


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
`Learning Center Home <http://learning.cyverse.org/>`__


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

 .. |condensedR| image:: ./img/condensed-r.png
    :width: 200
    :height: 275
.. Comment: Place URLS Below This Line

   # Use this example to ensure that links open in new tabs, avoiding
   # forcing users to leave the document, and making it easy to update links
   # In a single place in this document

   .. |Substitution| raw:: html # Place this anywhere in the text you want a hyperlink

      <a href="REPLACE_THIS_WITH_URL" target="blank">Replace_with_text</a>


.. |Github Repo Link|  raw:: html

   <a href="https://github.com/CyVerse-learning-materials/240-minute-r-tutorial" target="blank">Github Repo Link</a>

.. |Download Cyberduck| raw:: html

   <a href="https://cyberduck.io/" target="blank">Download Cyberduck</a>

.. |DE Application URL|  raw:: html

   <a href="https://de.cyverse.org/de/?type=apps&app-id=9b41c9e4-5031-4a49-b1cb-c471335df16e&system-id=de" target="blank">DE Application URL</a>

.. |Original App Documentation|  raw:: html

   <a href="http://www.drive5.com/muscle/manual/" target="blank">Original App Documentation</a>

.. |Atmosphere Image|  raw:: html

   <a href="https://atmo.cyverse.org/application/images/1384" target="blank">Atmosphere Image</a>

.. |Project R|  raw:: html

   <a href="https://cloud.r-project.org/" target="blank">Project R</a>

.. |RStudio|  raw:: html

   <a href="https://www.rstudio.com/products/rstudio/download/" target="blank">RStudio</a>
