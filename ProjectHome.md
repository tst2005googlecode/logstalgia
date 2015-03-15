![http://logstalgia.googlecode.com/svn/trunk/screenshots/logstalgia.png](http://logstalgia.googlecode.com/svn/trunk/screenshots/logstalgia.png)

Logstalgia (aka ApachePong) is a website access log visualization tool.

<a href='http://www.youtube.com/watch?feature=player_embedded&v=HeWfkPeDQbY' target='_blank'><img src='http://img.youtube.com/vi/HeWfkPeDQbY/0.jpg' width='425' height=344 /></a>

## Description ##

Logstalgia is a website traffic visualization that replays or streams web-server access logs as a pong-like battle between the web server and an never ending torrent of requests.

Requests appear as colored balls (the same color as the host) which travel across the screen to arrive at the requested location. Successful requests are hit by the paddle while unsuccessful ones (eg 404 - File Not Found) are missed and pass through.

The paths of requests are summarized within the available space by identifying common path prefixes. Related paths are grouped together under headings. For instance, by default paths ending in png, gif or jpg are grouped under the heading Images. Paths that don’t match any of the specified groups are lumped together under a Miscellaneous section.

## Requirements ##

Logstalgia requires a video card supporting OpenGL. For this reason you should typically run Logstalgia on your workstation rather than on the web-server itself (unless your workstation is the web-server).

As Logstalgia is designed to playback logs in real time you will need a log from a fairly  busy  web-server to achieve interesting results (eg 100s of requests each minute).

An example access log is included.

## Supported Log Formats ##

Logstalgia supports several standardized access.log formats used by web servers such as **Apache** and **Nginx**:

```
NCSA Common Log Format (CLF)
    "%h %l %u %t \"%r\" %>s %b"

NCSA Common Log Format with Virtual Host
    "%v %h %l %u %t \"%r\" %>s %b"

NCSA extended/combined log format
    "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\""

NCSA extended/combined log format with Virtual Host
    "%v %h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\""
```

The process id (%P), or some other identifier, may be included as an additional
field at the end of the entry. This can be used with '--paddle-mode pid' where
a separate paddle will be created for each unique value in this field.

Also supported a pipe delimited [Custom Log Format](http://code.google.com/p/logstalgia/wiki/CustomLogFormat) (more details on the Wiki):

```
1371769989|127.0.0.1|/index.html|200|1024|1|00FF00
```

## Controls ##

The simulation can be paused at any time by pressing space. While paused, individual requests can be inspected by passing over them with the mouse.

## Donations ##

If you like Logstalgia and would like to show your appreciation and encourage future work on this and other open source projects by the author, please consider making a donation!

[![](https://www.paypal.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=TZYLY4VTKC9TN&lc=NZ&item_name=Logstalgia&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donate_LG%2egif%3aNonHosted)

<a href='Hidden comment: 

*Bitcoin*: 1134j93heQZ8GVYCjY1g6C8Un65LfctbdM

http://logstalgia.googlecode.com/svn/trunk/logstalgia-qr.png

'></a>

## Related Software ##

If you like Logstalgia you may also want to check out [Gource](http://code.google.com/p/gource/), a software version control visualization tool.

## News ##

### 16 October 2014 ###

Logstalgia **1.0.6** has been released.

Changes since 1.0.5:

  * Display invalid requests as having the path '???'.
  * Updated the boost autoconf macro.

Downloads:

  * [logstalgia-1.0.6.tar.gz](https://github.com/acaudwell/Logstalgia/releases/download/logstalgia-1.0.6/logstalgia-1.0.6.tar.gz)

### 3 April 2014 ###

Well this hasn't happened in a while: a new Logstalgia release!

Logstalgia now uses SDL 2.0 when available, providing  much better multi-monitor support.

You can also now date ranges on the command line using the --from and --to ISO\_DATETIME options.

Various other improvements are listed below:

  * Performance improvements.
  * Multi-monitor support using SDL 2.0.
  * SDL 1.2 support is deprecated.
  * Can now specify the attribute to match the group regex (-g) against.
  * When using --sync, now catches back up after resuming from pause.
  * Added --pitch-speed option (control how fast balls travel).
  * Made default group matches case-insensitive (Sebastian Krzyszkowiak).
  * Display tokens in multi-paddle modes (Sebastian Krzyszkowiak).
  * Added window resizing and a full-screen toggle (alt-enter).
  * Take screenshots (F12).
  * Summarizer component content is now sorted.
  * IPv6 addresses now anonymized by default as well (last 64 bits).
  * New dependencies on libpng, GLEW.
  * Now requires GLM and Boost header-only libraries to build.

Downloads are now hosted on Github as Google Code no longer accepts adding new downloads:

  * [logstalgia-1.0.5.tar.gz](https://github.com/acaudwell/Logstalgia/releases/download/logstalgia-1.0.5/logstalgia-1.0.5.tar.gz)
  * [logstalgia-1.0.5-setup.exe](https://github.com/acaudwell/Logstalgia/releases/download/logstalgia-1.0.5/logstalgia-1.0.5-setup.exe)
  * [logstalgia-1.0.5.win32.zip](https://github.com/acaudwell/Logstalgia/releases/download/logstalgia-1.0.5/logstalgia-1.0.5.win32.zip)

If you package Logstalgia for a distro, please update the dependencies to use SDL 2 instead of SDL 1.2.

### 16 February 2011 ###

Logstalgia **1.0.3** has been released.

Changes since 1.0.2:

  * Added automatic skipping of empty periods (--disable-auto-skip to turn off).
  * Updated docs to reflect support for NCSA log formats, not just 'Apache'.
  * Support log entry dates with a valid numeric month in place of MMM.

### 18 January 2011 ###

Logstalgia **1.0.2** is finally out!

Request throughput in this version is been vastly improved. Log entry processing is no longer framerate limited and several bottlenecks have been optimized out, so this should finally do justice to your busy web server logs.

Log entry timezone offsets are now handled, so the --sync command should behave correctly if your webserver is in a different timezone.

Streaming over SSH on Windows should work reliably now.

This version has been tested and builds on Mac OS 10.6. There should be a formula for 1.0.2 in [Homebrew](https://github.com/mxcl/homebrew) really soon now.

Full changes since 1.0.0:

  * Performance improvements.
  * Stopped frame-rate being a bottle neck for the number of requests shown.
  * Improved STDIN input reliability on windows.
  * Handle log entry timezone offsets.
  * Made STDIN non-blocking on Windows using PeekNamedPipe (thanks Rui Lopes).
  * Removed arbitrary 1024 maximum length limit for log entries.
  * Fixed custom log format not working when optional fields are omitted.
  * Added --paddle-position option (to allow more space for URLs).
  * Added --font-size option.
  * Added --hide-url-prefix option to remove protocol and hostname from requests.

### 10 March 2010 ###

Logstalgia **1.0.0** has been released.

Changes since **0.9.9**:
  * Every 60 minutes fade static text out and back in over a period of a minute.

### 1 March 2010 ###

Logstalgia **0.9.9** has been released.

Changes since **0.9.8**:
  * Support for more common Apache access log formats.
  * Added --paddle-mode (vhost,pid,single) which spawns separate paddles.
  * Fixed PPM exporter producing blank images on some video cards.

### 9 Feb 2010 ###

Logstalgia **0.9.8** has been released.

Changes since **0.9.7**:

  * Added --background option to control the background colour.
  * Filter hostnames from URLs before displaying them.
  * Fixed command line option documentation.

### 4 Feb 2010 ###

Logstalgia **0.9.7** has been released.

This release adds the --sync option. This will synchronize Logstalgia with the next entry received on STDIN, so you can actually watch the log in real time:

```
tail -f /var/log/apache2/access.log | logstalgia --sync
```

### 31 Jan 2010 ###

Logstalgia **0.9.6** has been released. This adds quite a few new features, many ported from [Gource](http://code.google.com/p/gource/). This includes adding PPM output support for [recording videos](http://code.google.com/p/logstalgia/wiki/Videos), adding controls to seek to a point in the log file, improving the fonts, and adding some new effects.

Logstalgia also now builds on **Mac OS**!

Changes since **0.9.2**:
  * Adjust time scale with <> keys.
  * Added seekbar for log files (not available from STDIN).
  * Added glow on impact with paddle (turn off using --disable-glow).
  * PPM output for videos using --output-ppm-stream option.
  * Custom log file format support.
  * Changed font library to FTGL.
  * --stop-position and --start-position options.
  * Open a file selector if no log file supplied (on Windows).

### Example Command Lines ###

Watch an example access.log file using the default settings:

```
logstalgia data/example.log
```

Watch the live access.log, starting from the most recent batch of entries in the log (requires tail). Note than '-' at the end is required for logstalgia to know it needs to read from STDIN:

```
tail -f /var/log/apache2/access.log | logstalgia -
```

To follow the log **in real time**, use the --sync option. This will start reading from the next entry received on STDIN:

```
tail -f /var/log/apache2/access.log | logstalgia --sync
```

Watch a remote access.log via ssh. The '-g' option is used here to group together URLs requested containing the string '/adclick.php' under the heading 'Ad Clicks':

```
ssh user@yourserver.com tail -f /var/log/apache2/access.log | logstalgia -g "Ad Clicks,/adclick.php,30" -
```

**NOTE**: tailing remote logs is not currently recommended on the Windows version due to buffering issues.