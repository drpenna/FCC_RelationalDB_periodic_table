# FCC_RelationalDB_periodic_table

This is my solution for the [**Build a Periodic Table Database**](https://www.freecodecamp.org/learn/relational-database/build-a-periodic-table-database-project/build-a-periodic-table-database)
required project for the [**freeCodeCamp's Relational Databases Certification**](https://www.freecodecamp.org/learn/relational-database/) using PostgreSQL and bash. <br />

## Contents
- [Project Tasks Summary](#project-tasks-summary)
- [Files](#files)
  - [periodic_table.sql](#periodic_table.sql)
      - [table *elements*](#elements)
      - [table *properties*](#properties)
      - [table *types*](#types)
  - [element.sh](#element.sh)
- [Project tasks](#project-tasks)

## Project Tasks Summary
The project required the completion of the following steps:
1. Fix the existing database according to the user stories;
2. Create a git repository to track step 3;
3. Create a bash script that accepts an argument in the form of an `atomic number`, `symbol`, or `name` of an element and outputs some information about the given element.

[<sub>Back to top</sub>](#top)

## Files

### periodic_table.sql

Initial file provided by freeCodeCamp.\
The database can be rebuilt by entering `psql -U postgres < periodic_table.sql` in a terminal where the `.sql` file is.\
The file in this repository already has the corrections requested in the user stories. 

[<sub>Back to top</sub>](#top)

#### elements

|atomic_number <sup>1</sup>|	symbol <sup>2</sup>|	name <sup>3</sup>|
|:------------------------:|:-------------------:|:------------------:|
|1|H|Hydrogen|
|2|He|Helium|
|3|Li|Lithium|
|4|Be|Beryllium|
|5|B|Boron|
|6|C|Carbon|
|7|N|Nitrogen|
|8|O|Oxygen|
|9|F|Fluorine|
|10|Ne|Neon|

<sup>1</sup> serial, primary key, not null, unique\
<sup>2</sup> varchar(2), not null, unique\
<sup>3</sup> varchar(40), not null, unique

[<sub>Back to top</sub>](#top)


#### properties

|atomic_number <sup>4</sup>|	atomic_mass <sup>5</sup>|	 melting_point_celsius <sup>6</sup>| boiling_point_celsius <sup>7</sup>| type_id <sup>8</sup> |	
|:------------------------:|:------------------------:|:----------------------------------:|:---------------------------------:|:--------------------:|
|1| 1.008| -259.1| -252.9| 1|
|2| 4.0026| -272.2| -269| 1|
|3| 6.94| 180.54| 1342| 2|
|4| 9.0122| 1287| 2470| 2|
|5| 10.81| 2075| 4000| 3|
|6| 12.011| 3550| 4027| 1|
|7| 14.007| -210.1| -195.8| 1|
|8| 15.999| -218| -183| 1|
|9| 18.998| -220| -188.1| 1|
|10| 20.18| -248.6| -246.1| 1|

<sup>4</sup> int, primary key, not null, unique, foreign key REFERENCES public.elements(atomic_number)\
<sup>5</sup> num, not null\
<sup>6</sup> num, not null\
<sup>7</sup> num, not null\
<sup>8</sup> int, not null, foreign key REFERENCES public.types(type_id)

[<sub>Back to top</sub>](#top)


#### types

|type_id <sup>9</sup>|	type <sup>10</sup>|
|:------------------------:|:-------------------:|
|1| nonmetal|
|2| metal|
|3| metalloid|

<sup>9</sup> int, primary key, not null\
<sup>10</sup> varchar(10), not null

[<sub>Back to top</sub>](#top)




### element.sh
It can be started by inputting `./element.sh [element]` in the terminal, with [element] being either an `atomic number`, `symbol`, or `name` of an element. \
If the chosen element can be found in the database, the terminal will print the message:
> The element with atomic number [atomic_number] is [name] ([symbol]). It's a [type], with a mass of [atomic_mass] amu. [name] has a melting point of [melting_point_celsius] celsius and a boiling point of [boiling_point_celsius] celsius.

Otherwise, the terminal will print:
> I could not find that element in the database.

If the app is run without an argument, it'll print:
> Please provide an element as an argument.

[<sub>Back to top</sub>](#top)


## Project Tests
The goal was to modify a database in PostgreSQL and create a script in bash that passed the following tests\
(more details available on [**Build a Periodic Table Database**](https://www.freecodecamp.org/learn/relational-database/build-a-periodic-table-database-project/build-a-periodic-table-database)):

- You should rename the `weight` column to `atomic_mass`
- You should rename the `melting_point` column to `melting_point_celsius` and the `boiling_point` column to `boiling_point_celsius`
- Your `melting_point_celsius` and `boiling_point_celsius` columns should not accept null values
- You should add the `UNIQUE` constraint to the `symbol` and `name` columns from the `elements` table
- Your `symbol` and `name` columns should have the `NOT NULL` constraint
- You should set the `atomic_number` column from the `properties` table as a foreign key that references the column of the same name in the `elements` table
- You should create a `types` table that will store the three types of elements
- Your `types` table should have a `type_id` column that is an integer and the primary key
- Your `types` table should have a `type` column that's a `VARCHAR` and cannot be `null`. It will store the different types from the `type` column in the `properties` table
- You should add three rows to your `types` table whose values are the three different types from the `properties` table
- Your `properties` table should have a `type_id` foreign key column that references the `type_id` column from the `types` table. It should be an `INT` with the `NOT NULL` constraint
- Each row in your `properties` table should have a `type_id` value that links to the correct type from the `types` table
- You should capitalize the first letter of all the `symbol` values in the `elements` table. Be careful to only capitalize the letter and not change any others
- You should remove all the trailing zeros after the decimals from each row of the `atomic_mass` column. You may need to adjust a data type to `DECIMAL` for this. The final values they should be are in the `atomic_mass.txt` file
- You should add the element with atomic number `9` to your database. Its name is `Fluorine`, symbol is `F`, mass is `18.998`, melting point is `-220`, boiling point is `-188.1`, and it's a `nonmetal`
- You should add the element with atomic number `10` to your database. Its name is `Neon`, symbol is `Ne`, mass is `20.18`, melting point is `-248.6`, boiling point is `-246.1`, and it's a `nonmetal`
- You should create a `periodic_table` folder in the `project` folder and turn it into a git repository with `git init`
- Your repository should have a `main` branch with all your commits
- Your `periodic_table` repo should have at least five commits
- You should create an `element.sh` file in your repo folder for the program I want you to make
- Your script (`.sh`) file should have executable permissions
- If you run `./element.sh`, it should output only `Please provide an element as an argument.` and finish running.
- If you run `./element.sh 1`, `./element.sh H`, or `./element.sh Hydrogen`, it should output only `The element with atomic number 1 is Hydrogen (H). It's a nonmetal, with a mass of 1.008 amu. Hydrogen has a melting point of -259.1 celsius and a boiling point of -252.9 celsius.`
- If you run `./element.sh` script with another element as input, you should get the same output but with information associated with the given element.
- If the argument input to your `element.sh` script doesn't exist as an `atomic_number`, `symbol`, or `name` in the database, the only output should be `I could not find that element in the database.`
- The message for the first commit in your repo should be `Initial commit`
- The rest of the commit messages should start with `fix:`, `feat:`, `refactor:`, `chore:`, or `test:`
- You should delete the non existent element, whose `atomic_number` is `1000`, from the two tables
- Your `properties` table should not have a `type` column
- You should finish your project while on the `main` branch. Your working tree should be clean and you should not have any uncommitted changes

[<sub>Back to top</sub>](#top)
