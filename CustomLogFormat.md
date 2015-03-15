## Custom Log Format ##

### Overview ###

Logstalgia can be used to visualize other sources of data using a simple pipe ('|') delimited custom log format.

**Required fields**

  * **timestamp** - A [unix timestamp](http://en.wikipedia.org/wiki/Unix_time) of when the request occurred.
  * **hostname**  - hostname of the request.
  * **path**      - path being required.
  * **response code** - response code.
  * **response size** - The size of the response in bytes.

**Optional fields**

  * **success** - 1 or 0 to indicate if the response was successful.
  * **response colour** - colour to use for response code to use in hex (#FFFFFF) format.
  * **referrer url**    - the referrer url.
  * **user agent**      - the user agent.
  * **virtual host**    - the virtual host (to use with --paddle-mode vhost).
  * **pid/other**       - process id or some other identifier (--paddle-mode pid).

### Examples ###

Using the required fields:

```
1371769989|127.0.0.1|/index.html|200|1024
```

Including the optional fields:

```
1371769989|127.0.0.1|/index.html|200|1024|1|00FF00|http://www.example.com/|Mozilla/5.0|webserver|1234
```

### Usage ###

This format is detected by Logstalgia, so to use your custom log file:

```
logstalgia custom.log
```

You can also setup a script that prints custom log entries to STDOUT, and pipe this into logstalgia in real time:

```
custom-log-script.pl | logstalgia --sync -
```

(--sync will show all entries with timestamps from the current time onwards)