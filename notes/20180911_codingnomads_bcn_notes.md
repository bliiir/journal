**Journal**

# 20181003



# 20180928

## Install mysql connector

`pip3 install mysql-connector`
`pip3 install psycopg2-binary`

# 20180926

## Ports
[Here](https://en.wikipedia.org/wiki/Port_(computer_networking)#Common_port_numbers) is a list of common port numbers

| Port | Standard usage |
| :-- | :-- |
| 3306 | Standard database port |
| 8000 | Web server |
| 22 | |


SSH/HTTP: 22



## Databases

## Structure

* Schema
    * Tables
        * Columns
            * Data type
                * int
                * char
                * ...
            * Primary keys
            * Foreign keys
        * Rows / Records / Observations

### Example: University

#### Tables

##### Student

| | | |
| :-- | :-- | :-- |
| _id | name_first | name_last |
| 001 | Rasmus | Groth |
| 002 | Martin | Breuss |


##### Courses

| | | | |
| :-- | :-- | :-- | :-- |
| _id | name | date_start | date_end |
| 001 | Python + Django + AWS | 20190207 | 20190419 |
| 002 | Javascript + React Native + Redux | 20190207 | 20190419 |


##### Facilities

| | | | |
| :-- | :-- | :-- | :-- |
| _id | name | latitude | longtitude |
| 001 | Betahaus Barcelona | 41.387920 | 2.169920 |
| 002 | Betahaus Berlin | 52.523430 | 13.411440 |
| 003 | Betahaus Hamburg | 53.553840 | 9.991650 |

##### Subtable - contact details

| __student_id | email | type |
| :-- | :-- | :-- |
| 001 | a_first_email@email.com | private |
| 001 | a_second_email@email.com | work |
| 002 | a_third_email@email.com | private |

##### Lookup - course_facility

| __course_id | __facility_id |
| :-- | :-- |
| 001 | 002 |
| 002 | 003 |

##### Lookup - course_student

| __student_id | __course_id |
| :-- | :-- |
| 001 | 001 |
| 001 | 002 |



### Database clients
MySQL Workbench - GUI


#### MySQL Client

Set the `PATH `to mysql in .bash_profile:

`export PATH=/usr/local/mysql-8.0.12-macos10.13-x86_64/bin:$PATH`

| command | description |
| :-- | :-- |
| mysql -u root -p | open mysql AS user root with password |

#### SQL Statements
| Statement | Description|
| :-- | :-- |
| SHOW DATABASES; | Show all databases |
| CREATE DATABASE first_db; | |
| USE first_db | Changes database to first_db |
| SHOW TABLES | Show tables in active datbase |
| DROP database first_db; | Drops (delete) |
| CREATE DATABASE university; | |
| DESCRIBE my_table; | pretty print the table my_table in the databas in USE |
| DESCRIBE first_db.my_table; | pretty print the table my_table in the databas first_db |

##### Create table

```sql
CREATE TABLE students (
    id INT NOT NULL AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    PRIMARY KEY (id)
    );
```

##### Create a new record

```sql
INSERT INTO students
    (first_name, last_name)
    VALUES
    ("josh", "smith"),("jake", "john");
```

##### Make a query

```sql
SELECT first_name, last_name FROM students;

```

##### Select AS
```sql
SELECT first_name AS first, last_name AS last FROM students;
```
Output
```
+-------+-------+
| first | last  |
+-------+-------+
| josh  | smith |
| jake  | john  |
+-------+-------+
```

##### Select / order
```sql
SELECT * FROM students ORDER BY first_name asc;
```

```
+----+------------+-----------+
| id | first_name | last_name |
+----+------------+-----------+
|  2 | jake       | john      |
|  1 | josh       | smith     |
+----+------------+-----------+
2 rows in set (0.00 sec)
```

##### Join

```sql
SELECT students.f_name, students.l_name, majors.name
FROM students
JOIN students_majors
ON students.id = students_majors.student_id
JOIN majors
ON students_majors.major_id = majors.id;

```
Result:
```
+----------+----------+------------------+
| f_name   | l_name   | name             |
+----------+----------+------------------+
| Peter    | Jackson  | Computer Science |
| Peter    | Jackson  | Management       |
| Ian      | Stewart  | Nursing          |
| Duffy    | Higgins  | Kinesiology      |
| Peter    | Frampton | Liberal Arts     |
| Benito   | Camelo   | Nursing          |
| Sumtin   | Wong     | Management       |
| Sumtin   | Wong     | Computer Science |
| Michael  | SchwartZ | Kinesiology      |
| Casimiro | Nada     | Liberal Arts     |
| Kevin    | Neag     | Computer Science |
+----------+----------+------------------+
11 rows in set (0.00 sec)
```
Again - harder:
```sql
SELECT t.f_name, t.l_name, t.isTenured,  c.name, r.building_id
FROM teachers AS t
JOIN teachers_courses AS tc
ON t.id = tc.teacher_id
JOIN courses AS c
ON c.id  = tc.course_id
JOIN courses_rooms AS cr
ON c.id = cr.course_id
JOIN rooms AS r
ON cr.room_id = r.id
```
Result:

```
+--------+----------+-----------+----------------+-------------+
| f_name | l_name   | isTenured | name           | building_id |
+--------+----------+-----------+----------------+-------------+
| Jose   | Martinez |         0 | Physics        |           1 |
| Donald | Duck     |         0 | Chemistry      |           2 |
| Jeff   | Goldblum |         1 | Poetry         |           3 |
| Hulk   | Hogan    |         0 | Basket Weaving |           1 |
| Ryan   | Desmond  |         1 | Linear Algebra |           2 |
+--------+----------+-----------+----------------+-------------+
5 rows in set (0.00 sec)
```

Harder yet:
```sql
SELECT c.name AS course_name, r.capacity, b.name, COUNT(s.id) AS count_of_students
FROM students AS s
JOIN students_courses AS sc
ON s.id = sc.student_id
JOIN courses AS c
ON c.id = sc.course_id
JOIN courses_rooms AS cr
ON cr.course_id = c.id
JOIN rooms AS r
ON r.id = cr.room_id
JOIN building AS b
ON r.building_id = b.id
GROUP BY course_name, r.capacity, b.name
HAVING COUNT(s.id) > r.capacity
ORDER BY course_name;
```

Much harder:

```sql

SELECT my.first_name, my.last_name, SUM(my.length) as my_sum

 FROM

 (SELECT a.first_name, a.last_name, a.actor_id, f.title, f.description, f.length, f.release_year, c.name
 FROM sakila.actor as a
 JOIN sakila.film_actor as fa
 ON a.actor_id = fa.actor_id
 JOIN sakila.film as f
 ON f.film_id = fa.film_id
 JOIN sakila.film_category as fc
 ON f.film_id = fc.film_id
 JOIN sakila.category as c
 ON c.category_id = fc.category_id) as my

 GROUP BY my.first_name, my.last_name, my.actor_id

 ORDER BY my_sum desc
```

Result:
```
+----------------+----------+--------------------------+-------------------+
| course_name    | capacity | name                     | count_of_students |
+----------------+----------+--------------------------+-------------------+
| Basket Weaving |        2 | Einstein Hall of Physics |                 5 |
+----------------+----------+--------------------------+-------------------+
1 row in set (0.00 sec)
```


## Import database schema

`mysql -u root -p <schema_name> < <path><sqlfile>`

Example:

`mysql -u root -p university < /Users/rg/Downloads/my_sql_file.sql`

## Export database schema

`mysqldump -u root -p <schema_name> > <path>`

Example:

`mysqldump -u root -p university > /Users/rg/Downloads/`




# Environment variables

1. Using the terminal, navigate to the folder you want your code in
2. go to terminal: `python3 -m venv env`
3. Open the “activate” file with text editor, add “unset” of your variable names at the deactivate() module.

```
deactivate () {
   unset TWITTER_API_KEY
   unset TWITTER_API_SECRET_KEY
   unset TWITTER_ACCESS_TOKEN
   unset TWITTER_ACCESS_SECRET
```

4. Add `export` at the bottom of activate file for each variable.

```
export TWITTER_API_KEY={enter_your_key}
export TWITTER_API_SECRET_KEY={enter_your_key}
export TWITTER_ACCESS_TOKEN={enter_your_key}
export TWITTER_ACCESS_SECRET={enter_your_key}
```

5. Import os and reference the variables in your settings.py file

```py
import os

consumer_key = os.environ[“TWITTER_API_KEY”]
consumer_secret = os.environ[“TWITTER_API_SECRET_KEY”]
access_token = os.environ[“TWITTER_ACCESS_TOKEN”]
access_token_secret = os.environ[“TWITTER_ACCESS_SECRET”]
```

# 20180924

### CRUD
| Command | Description |
| :--| :-- |
| **C**reate |  |
| **R**ead |  |
| **U**pdate |  |
| **D**elete |  |

## APIs

### REST apis
**Re**presentational **S**tate **T**ransfer API

#### HTTP Methods:
[wiki](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)


| Method | | Description | URL | Headers | Body |
| :-- | :-- | :-- | :-- | :-- | :-- |
| `GET` | Read | Get data from server |required | optional | unavailable |
| `PUT` | write | Replace date ON server | required | optional | optional |
| `POST` | Append | Create new entry |required | optional | optional |
| `PATCH` | Write | Update data ON server | required | optional | optional |
| `DELETE` | Write | Delete data ON server | required | optional | optional |


#### HTTP(S) Requests

* Protocol - HTTP or HTTPS
    * subdomain.
        * domain/
            * Path/
                * resource ?
                    * Query parameters &
                    * Query parameters
    * Headers
    * Body

Example request:

https://my.domain.com/my_path/more_of_my_path/resource?query_key=query_value&another_query_key=another_query_value


### JSON
```
Object {}
Array []
Value
    string
    number
    object
```

# 20180923

## Paths
|  | Path |
| :------------- | :------------- |
| `Sublime repl` | /Users/rg/Library/Application Support/Sublime Text 3/Packages/User/Ras Python3.sublime-build |


*20180920*

## Lambda functions
Generate a list of the squares for each of the items in the list below
```py
_list = [1,2,3]
```
#### Normal functions
```py
def square(x):
    return x**2

res = list(map(square, _list))
print(res)
```
Output
```
[1, 4, 9]
```

#### Lambda function
```py
res = list(map(lambda x: x**2, _list))
print(res)
```
Output
```
[1, 4, 9]
```

#### List comprehension
```py
res = [x**2 for x in _list]
print(res)
```
Output
```
[1, 4, 9]
```



## Time complexity / [Big O](https://en.wikipedia.org/wiki/Big_O_notation)
O(n)
For a list [1, 2, 3 ,4, .. n]

|Algo |Best case| Worst case |
|:--|:--|:--|
|For loop |O(1)| O(n) |
|Bubble sort | O(n-1) |  |

## Data structures
| Data structure | Description | Underlying |
| :-- | :-- | :-- |
| List | | |
| Dictionary | | Hashmap |
| Queue | First in first out | |
| Stack | First in last out |  |
| Hashmap | Fast lookup data structure | |

## Type Hinting
```py
def my_function(arg1: int, arg2: int) - str:
    pass
```
Whatever is between the ":" and the "," and between the ")" and end of line ":"will be ignored by Python

## Decorators
A decorator is a function that takes a function AS an argument and changes its behaviour
```py
def decorator_func(initial_func):

    def wrapper_func():
        print("wrapper function picked ome...")
        return initial_func()

    return wrapper_func

# Long version
def prettify():
    print("flowers for you")
prettify = decorator_func(prettify)

# Short version - means that you call decorator_func every time you call prettify
@decorator_func
def prettify():
    print("flowers for you")

@decorator_func
def feed():
    print("Apples and potatoes")

prettify()
feed()
```
Output
```
wrapper function picked ome...
flowers for you
wrapper function picked ome...
Apples and potatoes
```

*20180919*

## Scope

```py
name = "Mycroft"                #01
                                #02
def box():                      #03
    print(name)                 #04
                                #05
    def smaller_box():          #06
        name = "martin"         #07
        print(name)             #08
                                #08
        def smallest_box():     #09
            print(name)         #10
                                #11
        smallest_box()          #12
                                #13
    smaller_box()               #14
                                #15
box()                           #16
                                #17
print(name)                     #18
```

#### Result
```
>>> Mycroft
>>> martin
>>> martin
>>> Mycroft
```
#### Explanation
* Initialize
* 01: Set `name` to "Mycroft"
* 17: call `box()`
    * 03: execute `box()`
        * 04: `print(name)` > Mycroft
        * 15: call `smaller_box()`
            * 06: execute `smaller_box()`
                * 07: set `name` to "martin"
                * 08: `print(name)` > martin
                * 13: call `smallest_box()`
                    * 10: execute `smallest_box()`
                        * 11: `print(name)` > martin
* 19: `print(name)` > Mycroft (because we are in the global scope)

## \*args and \*\*kwargs

### Args - arguments

> args are used when you don't know how many arguments you are passing. The name of the args variable is preceeded with a * to tell python it is a tuple of arguments.
Args are a bit like lists

```py
def my_function(*unicorn):
    sum = 0
    for i in unicorn:
        sum += 1s
    print("count:", sum)
    #print(a,b)

my_function(1, 2, 3, 4, 10, 30)
```

`>>> count: 6`

### Kwargs - key-word-arguments
\*\*kwargs are used when you don't know how many arguments you are passing, but each argument is named unlike args
Kwargs are a bit like dictionaries
```py
def my_kwargs_function(**kwargs):
    print(kwargs)

my_kwargs_function(x=1, y=2, z=3, a=4, b=10, c=30)
```
`>>> {'x': 1, 'y': 2, 'z': 3, 'a': 4, 'b': 10, 'c': 30} `

## Iterators

I will use this list throughout these examples:

```py
num_list = list(range(1,20))
```

### `enumerate():`

```py
_list = ["plant", "animal", "bacteria", "funghi"]
for index, value in enumerate(_list, start=1):
    print(index, value)
```

```
0 plant
1 animal
2 bacteria
3 funghi
```

```py
for i in range(len(_list)):
    print(i, _list[i])
```

```
0 plant
1 animal
2 bacteria
3 funghi
```

### List comprehension

#### Long version
```py
new_list = []
for item in num_list:
    if item % 2 == 0:
        new_item = item ** 2
        new_list.append(new_item)
print(new_list)
```
`>>> [4, 16, 36, 64, 100, 144, 196, 256, 324]`

#### Short version
```py
new_list = [item**2 for item in num_list if item % 2 == 0]
print(new_list)
```
`>>> [4, 16, 36, 64, 100, 144, 196, 256, 324]`

### Generators
Generators creates an iterable that can be activated ON the fly, but does not keep a persistent object with values

```py
gen = (n**2 for n in nums)
for i in gen:
    print(i)
```

*20180918*
###String formatting

```py
hi = "Hello"
you = "Rasmus"
```

##### The old way
```py
print("I say %s" % hi)
>>> I say Hello
```
##### The new way - `.format`
```py
print("I say {:20s} to {}".format(hi, you))
>>> I say Hello                to Rasmus
```

##### The hip way - f strings
```py
print(f"I say {hi:20s} to {you}")
>>> I say Hello                to Rasmus
```

### Escape characters
| | |
| :-- | :-- |
| \ | Escapes the character after it. Useful if you want to not have the newline character |
| \t | Tab |
| \n | new line |

## Exception handling

| Command | Description |
| :-- | :-- |
| `try: \n\t statement` | try to execute the statement |
| `except: \n\t statement` | If there is an exception, execute statment |
| `except ZeroDivisionError AS zde: \n\t statement` | If there is a zero division error, execute statement |
| `else: \n\t statement` | Do this if there are no exceptions |
| `finally: \n\t statement` | Do this in all cases |
| `assert (statement), "message"` | Throws a custom statement when an exception happens |
| `raise Exceptionclass("message")` | Raises an error of Exceptionclass with a message |
|

```py
# Try this
try:
    _list = [1,2]
    print(_list[3])

# Catch index errors specifically
except IndexError AS ie:
    print("Cannot access that element")

# Catch all other exceptions
except Exception AS exc:
    print("There was an exception:", exc)

# Do this if no exceptions
else:
    print("There were no errors")
# Always do this
finally:
    print("Done")
```
```
Cannot access that element
Done
```

```py
try:
    if(10 > 0):
        my_exception = Exception("We are raising this exception")
        raise Exception

except Exception:
    print("There was an error", my_exception)
```
```
There was an error We are raising this exception
```

### Custom exception handling
```py
class MyException(Exception):

    status_codes = {404: "not found", 500: "server error"}

    def __init__(self, status_code, message):
        self.status_code = status_code
        self.message = message
        self.status_message = MyException.status_codes[status_code]

    def __str__(self):
        return "This is a new way to return the exception AS a string"

x = 10
y = 0

try:
    if (y == 0):
        raise MyException(404, "exception raised")
    print(x/y)
except MyException AS exc:
    print("error with status code: ", exc.status_code)
    print("with message: ", exc.message)
    print(exc.status_message)

```


## Packages
### Installing packages
From outside python

| command | Description |
| :-- | :-- |
| `pip install plotly` | Installs plotly ON the machine using pypip.org (Python pip installs packages) |

### Using Packages
From inside python

| Command | Description |
| :-- | :--
| `import packagename` | Imports the package | packagename.methodname()
| `from packagename import methodname` | imports the method so it is available without the packagename AS if it was a function writting in the local script| methodname() |
| `import packagename AS pn` | Imports packagename AS pn | `pn.methodname()` |
| `from packagename import methodname AS mn | Imports methodname from packagename into the alias mn | `mn()` |

*20180914*
## Objects, classes, inheritance

### Three tenets of Object Oriented Programming

| Concept | Explanation | Example |
| :-- | :-- | :-- |
| [Polymorphism](https://pythonspot.com/polymorphism/) | Polymorphism means that an object that inherits appears to be both kinds of object, the kind of object it is itself and the kind of object from which it inherits. | For example - files have a file.open() method ON them which enables me to open all kinds of files using the same methods - could be .pdf, .txt |
| [Encapsulation](https://pythonspot.com/encapsulation/) | Encapsulation in this sense means that a programmer can bundle data and methods into a single entity.| Private methods and variables |
| [Inheritance](https://pythonspot.com/inheritance/) | Inheritance is the ability to use the data and methods of one kind of object by another AS if they were defined in the other object to begin with. | Tiger is a child of Mammal which is a child of Animal |


### Inspecting classes

| Command | Effect |
|:--|:--|
| ```vars(obj)``` | returns all variables from the object obj |
| ```dir(obj)``` | returns all methods from the object obj |
| ```isinstance(obj, cl)``` | returns True if obj is an instance of cl |
| ```type(obj)``` | returns the type of the object |
| ```hasattr(obj, atr)``` | returns True if the object has |

### Dunder functions
| Function | Description |
| :-- | :-- |
| ```__init__``` | This method is run ON object instantiation. |
| ```__dict__``` | The convention (which can be overridden) is that the __dict__ method will return a dictionary of all the objects' variables and their values. |
| ```vars(obj)``` | is a wrapper/alias for ```obj.__dict__()``` |
| ```__str__``` | The convention (which can be overridden) is that the __str__ method will return the object's class name and memory allocation |
| ```print(obj)``` | calls ```obj.__str__()``` and return a dictionary of all the objects' variables and their values. |
| ```__repr__``` | The convention (which can be overridden) is that the __repr__ method will return the object's class name and memory allocation. If ```__str__``` isn't explicitly defined for the object, ```print(obj)``` will print ```__repr__``` |


### Conventions
* Classnames start with a capital letter
* It is considered a good idea to initialize all of an object’s attributes in the init method.
* Double underscore functions such AS __init__ are called dunder functions



*20180913*
## Tuples
An immutable sequence of values


*20180912*

## Lists
Mutable array of objects in an object

| Command | Effect |
|:--|:--|
| my_list.pop(n) | remove the nth item from the list my_list and return the item that was removed |
| my_list.remove(n) | remove the nth item from the list my_list |
|"".JOIN(my_list) | JOIN the elements of a list to a string |

## Tuples
Similar to lists, but they are imutable.

| command | result(print) |
|:--|:--|
| tup = 1,2,3 | (1,2,3)|
| tup = (1,2,3) | (1,2,3) |
| tup = tuple("ras") | ("r", "a", "s")

## Dictionary
Key-value pairs
### Create empty dictionary
```py
dict = dict()</br>
dict = {}</br>
dict = {"first":1, "second":2,"third":3}
```

*201800911*

## CodingNomads Codingcamp in Barcelona,
#### day 1

### CLI

[Cheat Sheets](https://github.com/WebDevStudios/CLI-Cheat-Sheet)

| Command | meaning | example |
| :--- | :--- | :--- |
| man <command> | View the manual for given command| |
| `pwd` | Print work directory | |
| `ls` | list files in current directory | |
| `ls -a` | List all files, including hidden files | |
| `ls -l` | List files in current directory AS a list | |
| `cd /` | Change directory to root | |
| `cd ~` | Change directory to home | |
| `cp [origin] [destination]` | copy | cp text.txt . | |
| `echo "hello" > file.txt` | print "hello" to file.txt | |
| `say "hello"` | Use the voice module to read the string "hello"| |
| `cat filename` | print filenamem | |
| `head filename` | print first x lines of filename | |
| `tail filename` | print last x line of filename | |
| `history > file1.txt` | replace contents of file1.txt with history | |
| `history >> file1.txt` | append contents of file1.txt with history | |
| `history \ grep "git" > file1.txt` | Find the word "git" in my history and replace the content of file1.txt with the result| |
| `find . -name "file*"` | find files and folders with the characters "file" AS part of the name | |
| `cd -` | go back to the most recent dir you've been in | |
| `chmod ----------` | change permissions | |
| `which python3` | Shows you where the python command is located | |
| `rm -rf folder_or_filename` | remove folder_filename forcefully recursively | |
| `history` | display past commands ||
| `touch scriptname.sh` | create shell script scriptname.sh | |
| `lsof -i tcp:8000` | List open files on tcp port 8000 | |
| `kill -9 pid` | kills the process with the pid | |
| `lsof -t -i tcp:8000 | xargs kill -9` | kill all processes on port 8000|

#### CLI options
| option | Effect     |
| :--- | :--- |
| `-r` | recursively |
| `-m` | message |


## Customization

Change `~/.bash_profile`, `.profile` or `~/.zscrc` to set custom command aliases

| alias | Resolves to | Description |
| :--- | :--- | :-- |
| `zshcf` | vim ~/.zshrc | Edit zsh profile settings|


#### Permissions

drwxr

rwx = Read Write Execute

| Directory | Owner | Group | User |
| :-- | :-- | :-- | :-- |
| - | - - - | - - - | - - - |
| d | rwx | rwx | rwx |
| 1 | 421 | 421 | 421 |

##### Examples
```py
chmod 777 = read(4), write(2) and execute(1) right for owner(7), group(7) and user(7)
chmod 777  = give owner, group and user read, write and execute rights
chmod 444 = give owner, group and user read access
```

### Shell Scripting
*Everything is a file!*
```
#!/bin/bash/
echo "starting script...
touch ~/Desktop/virus"
echo "creating virus"
echo "=============="
echo "adding to virus..."
find /Users/vkng/Dropbox/99_code/Python/CodingNomads -name "*week*" >> ~/Desktop/virus
open ~/Desktop/virus
```
```#!/bin/bash/``` is called the shbang


### Virtual environments


| command| Description |
| :-- | :-- |
| ```python3 -m venv env``` | Creates a virtual environment called my_first_env |
| ```source env/bin/activate``` | Activate the environment you have to ```source``` the activate file in the bin subfolder of the virtual environment |
| ```deactivate``` | Leave the venv |
| ```pip freeze > requirements.txt``` | Create a requirements.txt to store dependencies for the virtual environment in a textfile |
| ```pip install -r requirements.txt``` | Install the dependencies using the requirements.txt file |


## Git and Github

| Git Command | Description |
| :-- | :-- |
| ```git init``` | Initialize the folder AS a git repo |
| ```git status``` | Find out whats going ON |
| ```git add <filename>``` | Add a file to git |
| ```git add .``` | Add all changed files |
| ```git add -a```| Add all changed files |
| ```git add *```| Add all changed files |
| ```git commit -m "Created file using echo command" ``` | Commit changes |
| ```git remote add origin https://github.com/bliiir/git-test.git``` | Add remote origin |
| ```git push origin master``` | Push changes to master branch ON origin |
| ```git push -u origin master```    | push to origin master and set the default to origin master |
| ```git pull origin master``` | Pull from master branch ON origin |
| ```git branch BRANCH_NAME``` | Create a new branch |
| ```git checkout -b BRANCH_NAME``` | Creates a new branch BRANCH_NAME and checks it out at the same time |
| ```git checkout BRANCH_NAME``` | Change branch |
| ```git merge BRANCH_NAME``` | Merge branch with current branch |
| ```git rebase BRANCH_NAME``` | Add current branch after BRANCH_NAME  |
| ```git clone REMOTE_NAME```| Clone remote |
| ```git rm --cached filname.txt``` | remove filename.txt from staging |
| ```git remote -v``` | List remotes |
| ```git remote rm REMOTE_NAME``` | Remove remote REMOTE_NAME |
| ```git log``` | Print git log to console |


### Create a new repository ON the command line
```
echo "# gitFromStart" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/bliiir/gitFromStart.git
git push -u origin master
```
### push an existing repository from the command line
```
```
git remote add origin https://github.com/bliiir/gitFromStart.git
git push -u origin master
```



### Collaboration
Make your commit messages standardized. Here is a [styleguide](https://udacity.github.io/git-styleguide/) from udacity

### Client - Server architecture

#### HTTP protocol
##### Request/response pattern

| Direction | Start line | Headers | Body | Available methods |
| :-- | :-- | :-- | :-- | :-- |
| Request | GET /test/hi-there.txt HTTP/1.0 | Accept: text/*</br>Accept-language: en, fr| | PUT</br>GET</br>POST</br>DELETE |
| Response | HTTP/1.0 200 OK | Content-type: text/plain</br>Content-length: 19 | Hi! I am a message! |
