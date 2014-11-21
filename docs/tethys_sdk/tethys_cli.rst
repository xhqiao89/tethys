**********************
Command Line Interface
**********************

**Last Updated:** November 18, 2014

The Tethys Command Line Interface (CLI) provides several commands that are used for managing Tethys Platform and Tethys apps. The :term:`Python virtual environment` must be activated to use the command line tools. This can be done using the following command:

::

    $ ./usr/lib/tethys/bin/activate

The following article provides and explanation for each command provided by Tethys CLI.

Usage
=====

::

    $ tethys <command> [options]

Options
-------

* **-h, --help**: Request the help information for Tethys CLI or any command.


Commands
========

scaffold <name>
---------------

This command is used to create new Tethys app projects via the scaffold provided by Tethys Platform. You will be presented with several interactive prompts requesting metadata information that can be included with the app. The new app project will be created in the current working directory of your terminal.

**Arguments:**

* **name**: The name of the new Tethys app project to create. Only lowercase letters, numbers, and underscores are allowed.

**Examples:**

::

    $ tethys scaffold my_first_app

gen <type>
----------

Aids the installation of Tethys by automating the creation of supporting files. Currently, the :command:`gen` command is only capable of creating settings files.


**Arguments:**

* **type**: The type of object to generate. The only valid value for type is "settings".

    * *settings*: When this type of object is specified, :command:`gen` will generate a new :file:`settings.py` file. It generates the :file:`settings.py` with a new ``SECRET_KEY`` each time it is run.

**Optional Arguments:**

* **-d DIRECTORY, --directory DIRECTORY**: Destination directory for the generated object.

**Examples:**

::

    $ tethys gen settings
    $ tethys gen settings -d /path/to/destination

manage <subcommand> [options]
-----------------------------

This command contains several subcommands that are used to help manage Tethys Platform.

**Arguments:**

* **subcommand**: The management command to run. Either "start" or "syncdb".

    * *start*: Starts the Django development server. Wrapper for ``manage.py runserver``.
    * *syncdb*: Initialize the database during installation. Wrapper for ``manage.py syncdb``.

**Optional Arguments:**

* **-p PORT, --port PORT**: Port on which to start the development server. Default port is 8000.
* **-m MANAGE, --manage** MANAGE: Absolute path to :file:`manage.py` file for Tethys Platform installation if different than default.

**Examples:**

::

    # Start the development server
    $ tethys manage start
    $ tethys manage start -p 8888

    # Sync the database
    $ tethys manage syncdb

syncstores <app_name, app_name...> [options]
--------------------------------------------

Management command for Persistent Stores. To learn more about persistent stores see :doc:`./persistent_store`.

**Arguments:**

* **app_name**: Name of one or more apps to target when performing persistent store sync OR "all" to sync all persistent stores on this Tethys Platform instance.

**Optional Arguments:**

* **-r, --refresh**: Drop databases prior to performing persistent store sync resulting in a refreshed database.
* **-f, --firsttime**: All initialization functions will be executed with the ``first_time`` parameter set to ``True``.
* **-d, DATABASE, --database** DATABASE: Name of the persistent store database to target.
* **-m MANAGE, --manage** MANAGE: Absolute path to :file:`manage.py` file for Tethys Platform installation if different than default.

**Examples:**

::

    # Sync all persistent store databases for one app
    $ tethys syncstores my_first_app

    # Sync all persistent store databases for multiple apps
    $ tethys syncstores my_first_app my_second_app yet_another_app

    # Sync all persistent store databases for all apps
    $ tethys syncstores all

    # Sync a specific persistent store database for an app
    $ tethys syncstores my_first_app -d example_db

    # Sync persistent store databases with a specific name for all apps
    $ tethys syncstores all -d example_db

    # Sync all persistent store databases for an app and force first_time to True
    $ tethys syncstores my_first_app -f

    # Refresh all persistent store databases for an app
    $ tethys syncstores my_first_app -r


