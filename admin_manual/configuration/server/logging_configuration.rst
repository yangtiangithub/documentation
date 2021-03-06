=====================
Logging Configuration
=====================

Use your ownCloud log to review system status, or to help debug problems. You may adjust logging levels, and choose between using the ownCloud log or your syslog.

Parameters
----------

Logging levels range from **DEBUG**, which logs all activity, to **FATAL**, which logs only fatal errors.

* **0**: DEBUG: Debug, informational, warning, and error messages, and fatal issues.
* **1**: INFO:  Informational, warning, and error messages, and fatal issues.
* **2**: WARN:  Warning, and error messages, and fatal issues.
* **3**: ERROR: Error messages and fatal issues.
* **4**: FATAL: Fatal issues only.

By default the log level is set to **2** (WARN). Use **DEBUG** when you have a problem to diagnose, and then reset your log level to a less-verbose level, as **DEBUG** outputs a lot of information, and can affect your server performance.

Logging level parameters are set in the :file:`config/config.php` file, or on the Admin page of your ownCloud Web GUI.

ownCloud
~~~~~~~~

All log information will be written to a separate log file which can be
viewed using the log viewer on your Admin page. By default, a log
file named **owncloud.log** will be created in the directory which has
been configured by the **datadirectory** parameter in :file:`config/config.php`.

The desired date format can optionally be defined using the **logdateformat** parameter in :file:`config/config.php`.
By default the `PHP date function`_ parameter "*c*" is used, and therefore the
date/time is written in the format "*2013-01-10T15:20:25+02:00*". By using the
date format in the example below, the date/time format will be written in the format
"*January 10, 2013 15:20:25*".

::

    "log_type" => "owncloud",
    "logfile" => "owncloud.log",
    "loglevel" => "3",
    "logdateformat" => "F d, Y H:i:s",

syslog
~~~~~~

All log information will be sent to your default syslog daemon.

::

    "log_type" => "syslog",
    "logfile" => "",
    "loglevel" => "3",

Conditional Logging Level Increase
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can configure the logging level to automatically increase to ``debug`` when one of three conditions are met:

# ``shared_secret``: If a request parameter with the name ``log_secret`` is set to this value the condition is met.

# ``users``: If the current request is done by one of the specified users, this condition is met.

# ``apps``: If the log message is invoked by one of the specified apps, this condition is met.

The following example demonstrates what all three conditions look like::

 'log.condition' => [
	'shared_secret' => '57b58edb6637fe3059b3595cf9c41b9',
	'users' => ['sample-user'],
	'apps' => ['files'],
 ],

.. _PHP date function: http://www.php.net/manual/en/function.date.php
