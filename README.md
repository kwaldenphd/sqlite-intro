# Lab #5B: Getting Started With SQLite

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

## Acknowledgements

The author consulted the following resources when building this tutorial:
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Library Carpentry "SQL"](https://librarycarpentry.org/lc-sql/)

# Table of Contents

# What is SQLite

SQL stands for Structured Query Language. 

SQL "is a domain-specific language used in programming and designed for managing data held in a relational database management system (RDBMS)...It is particularly useful in handling structured data, i.e. data incorporating relations among entities and variables" ([Wikipedia, "SQL"](https://en.wikipedia.org/wiki/SQL)).

SQL was developed by IBM in the early 1970s.

Relational Software, Inc. (now Oracle Corporation) released the first commercial implementations of SQL in the late 1970s.

The American National Standards Institute (ANSI) and the International Organization for Standardization (ISO) adopted SQL as the official database query language in 1986.

SQL is maintained by the ISO and is updated semi-regularly (typically every three years).
- [Link to official SQL documentation](https://standards.iso.org/ittf/PubliclyAvailableStandards/index.html)

For more on SQL history:
- Codd, Edgar F. (June 1970). "A Relational Model of Data for Large Shared Data Banks". *Communications of the ACM.* 13 (6): 377–87. https://doi.org/10.1145%2F362384.362685
- Chamberlin, Donald (2012). "Early History of SQL". *IEEE Annals of the History of Computing.* 34 (4): 78–82. https://doi.org/10.1109%2FMAHC.2012.61
- Chamberlin, Donald D; Boyce, Raymond F (1974). "SEQUEL: A Structured English Query Language." *Proceedings of the 1974 ACM SIGFIDET Workshop on Data Description, Access and Control. Association for Computing Machinery*: 249–64. https://doi.org/10.1145/800296.811515

We'll be using an implementation of SQL known as SQLite.

"SQLite is a C-language library that implements a small, fast, self-contained, high-reliability, full-featured, SQL database engine. SQLite is the most used database engine in the world. SQLite is built into all mobile phones and most computers and comes bundled inside countless other applications that people use every day" ([SQLite, "What Is SQLite?"](https://www.sqlite.org/index.html)).

SQLite drives many commonly used programs and applications, including:
- Chrome, Firefox, and Safari web browsers
- Django
- Drupal
- Ruby on Rails
- Adobe Systems
- Evernote
- Skype
- iPhone text messages

Taking a quick look at SQLite's [Download](https://www.sqlite.org/download.html) and [Documentation](https://www.sqlite.org/docs.html) pages would suggest setting up a full implementation of STLite in your local computer environment is a tall order.
- *All hail the work of compilers*

So we're going to use a graphical-user interface (GUI) browser application that runs on top of SQLite.

[Database Browser for SQLite (DB Browser)](https://sqlitebrowser.org/) is an open-source application that provides a graphical user interface for connecting to and interacting with a SQLite database. 

The DB Browser application bundles SQLite, so you won’t need to install SQLite separately.

# Installing DB Browser for SQLite

Navigate to https://sqlitebrowser.org/ in a web browser.

Select the download version for your operating system:
- Windows: OOP Coders, ["Install DB Browser SQLite and create database"](https://youtu.be/CDen1TavGQ8) *YouTube* (2 September 2020)
- Mac: Cool IT Help, ["Sqlite Browser Installation on Mac OS"](https://youtu.be/SkXxnasbrFY) *YouTube* (3 October 2019)
- Google Chromebook: Follow the instructions for the Debian varation of Linux. 
  * See also: Dave McKay, ["How to Use DB Browser for SQLite on Linux"](https://www.howtogeek.com/704243/how-to-use-db-browser-for-sqlite-on-linux/), *How-To Geek* (16 September 2020)

Follow the installation instructions.

Once the installation is complete, launch the program.

# Getting started with DB Browser for SQLite

FIGURE 1

You should now be seeing the GUI (graphical user interface) window for the DB Browser application.

We're going to create a relational database using the `.csv` files from the first part of this lab.

Click the "New Database" icon in the top-left hand menu bar, or select "New Database" under "Files."

Save this database with a `.sql` file extension in a dedicated location on your computer.

## Importing tables from `.csv` files

FIGURE 2

Add each of the `.csv` files by going to "Import table from CSV" under "Import" under "Files."

FIGURE 3

Modify the table name if needed.

Make sure the "Column names in first line" box is checked.

Make sure comma is set as "Field separator," double quotation is set as "Quote character," and UTF-8 is set as "Encoding."

Click "OK" to import the table from the `.csv` file.

FIGURE 5

Click on the "SQL Log" button on the bottom right-hand corner of the window to see the SQL commands used to import this data.

These SQL commands are the programmatic expression of the steps we are taking using the graphical user interface.

Once we've done this for all of our `.csv` tables, our data should now be loaded into SQLite.

FIGURE 4

Click on the "Browse Data" tab to explore the data in each table (and make sure data imported correctly).

## Setting Keys and Building Table Relationships

Now we need to set data types and identify our keys.
- Go back to [the first part of this lab](https://github.com/kwaldenphd/data-models) if you're fuzzy on keys

Select the `Team_Locations` table and click on "Modify Table" icon. PC users can right-click on the selected table to see the "Modify Table" option.

FIGURE 6

Check the "Type" for each field and change as needed.

For fields that do not have null values, check `NN.`

For fields that have unique values, check `U`.

We also want to make sure we check `PK` for this table's primary key field.

The bottom half of the "Edit table definition" window shows these steps in SQL syntax.
- Scroll down to the bottom of this embedded window if needed.

Click "OK" to apply these changes.

Go through the same process for the `Player_DoB` table.
- Check data types
- Mark not null values
- Mark unique values
- Set primary key

We'll go through a similar process for the `Combined_Transactions` table, but remember this table does not include a primary key--it has two foreign keys.
- *player_id or id_person*
- *team_id*

Before we can set the foreign keys, we have to change a foreign key constraint within the DB Browser application.

FIGURE 4

Select the "Edit Pragmas" tab.

FIGURE 7

Uncheck the box next to "Foreign Keys."

Click "Save."

Now we can modify the `Combined_Transactions` table and set our foreign key fields.

FIGURE 8

You will need to extend or widen the "Edit table definition" window to see the "Foreign Key" option.

FIGURE 9

Select the first foreign key field (`id_person`) and double click the blank space under "Foreign Key."

You should see the option to specify a primary key reference table and field for the foreign key.

Go through the same process for the other foreign key field, `team_id`.

Remember the bottom half of the "Edit table definition" window shows these steps in SQL syntax.
- Scroll down to the bottom of this embedded window if needed.

Huzzah! The ERD and relational schema we built in the first part of this lab exist in our newly-created database.

Save all of these changes and close the program. We will use this newly-created database in an upcoming lab.

# Project Prompt



# Lab Notebook Questions





Import CSV

Modify table types

Do we have a relational database?

# Project Prompt



# Lab Notebook Questions
