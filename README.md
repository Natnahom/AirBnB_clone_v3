
---

I hope this helps clear things up. I apologize for the confusing versioning, but
the takeaway is that I've been directly involved in coding at least _an_ implementation
of everything.

Please let me know if you have any questions!

---

### Static :page_facing_up:

The front-end was designed from scratch using HTML5/CSS3 pages
integrated using Flask. While the front-end has not yet been officially deployed,
screenshots are viewable in the README of the [web_flask](./web_flask) directory.

## Storage :baggage_claim:

The above classes are handled by one of either two abstracted storage engines,
depending on the call - [FileStorage](./models/engine/file_storage.py) or
[DBStorage](./models/engine/db_storage.py).

### FileStorage

The default mode.

In `FileStorage` mode, every time the backend is initialized, HolbertonBnB
instantiates an instance of `FileStorage` called `storage`. The `storage`
object is loaded/re-loaded from any class instances stored in the JSON file
`file.json`. As class instances are created, updated, or deleted, the
`storage` object is used to register corresponding changes in the `file.json`.

### DBStorage

Run by setting the environmental variables `HBNB_TYPE_STORAGE=db`.

In `DBStorage` mode, every time the backend is initialized, HolbertonBnB
instantiates an instance of `DBStorage` called `storage`. The `storage` object
is loaded/re-loaded from the MySQL database specified in the environmental variable
`HBNB_MYSQL_DB`, using the user `HBNB_MYSQL_USER`, password `HBNB_MYSQL_PWD`, and
host `HBNB_MYSQL_HOST`. As class instances are created, updated, or deleted, the
`storage` object is used to register changes in the corresponding MySQL database.
Connection and querying is achieved using SQLAlchemy.

Note that the databases specified for `DBStorage` to connect to must already be
defined on the MySQL server. This repository includes scripts
[setup_mysql_dev.sql](./setup_mysql_dev.sql) and [setup_mysql_test.sql](./setup_mysql_test.sql)
to set up `hbnb_dev_db` and `hbnb_test_db` databases in a MySQL server,
respectively.

## Console :computer:

The console is a command line interpreter that permits management of the backend
of HolbertonBnB. It can be used to handle and manipulate all classes utilized by
the application (achieved by calls on the `storage` object defined above).

### Using the Console

The HolbertonBnB console can be run both interactively and non-interactively.
To run the console in non-interactive mode, pipe any command(s) into an execution
of the file `console.py` at the command line.

Alternatively, to use the HolbertonBnB console in interactive mode, run the
file `console.py` by itself:

Remember, the console can be run with `storage` instantiated in either `FileStorage`
or `DBStorage` mode. The above examples instantiate `FileStorage` by default, but
`DBStorage` can be instantiated like so:

The console functions identically regardless of the `storage` mode.

While running in interactive mode, the console displays a prompt for input:

To quit the console, enter the command `quit`, or input an EOF signal
(`ctrl-D`).

### Console Commands

#### create
* Usage: `create <class> <param 1 name>=<param 1 value> <param 2 name>=<param 2 value> ...`

Creates a new instance of a given class. The class' ID is printed and
the instance is saved to the file `file.json`. When passing parameter key/value
pairs, any underscores contained in value strings are replaced by spaces.


#### show
* Usage: `show <class> <id>` or `<class>.show(<id>)`

Prints the string representation of a class instance based on a given id.


#### destroy
* Usage: `destroy <class> <id>` or `<class>.destroy(<id>)`

Deletes a class instance based on a given id.

#### all
* Usage: `all` or `all <class>` or `<class>.all()`

Prints the string representations of all instances of a given class. If no
class name is provided, the command prints all instances of every class.

```


#### count
* Usage: `count <class>` or `<class>.count()`

Retrieves the number of instances of a given class.

```


#### update
* Usage: `update <class> <id> <attribute name> "<attribute value>"`

Updates a class instance based on a given id with a given key/value attribute
pair or dictionary of attribute pairs. If `update` is called with a single
key/value attribute pair, only "simple" attributes can be updated (ie. not
`id`, `created_at`, and `updated_at`).

```


## Authors :
Natnahom Asfaw 
Ephrem Gebretsion
