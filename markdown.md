Diagnostic Server for Common Data Identifiers
========


### Table of Contents
**[Functional Overview](#Functional-Overview)**<br>
**[Usage Instructions](#usage-instructions)**<br>
**[Troubleshooting](#troubleshooting)**<br>
**[Compatibility](#compatibility)**<br>
**[Notes and Miscellaneous](#notes-and-miscellaneous)**<br>
**[Building the Extension Bundles](#building-the-extension-bundles)**<br>
**[Next Steps, Credits, Feedback, License](#next-steps)**<br>

Functional Overview
------------


Initialization
-----------------------------

Markdown requires Perl 5.6.0 or later. Welcome to the 21st Century.
Markdown also requires the standard Perl library module `Digest::MD5`. 


### Movable Type ###

Markdown works with Movable Type version 2.6 or later (including 
MT 3.0 or later).

1.  Copy the "Markdown.pl" file into your Movable Type "plugins"
    directory. The "plugins" directory should be in the same directory
    as "mt.cgi"; if the "plugins" directory doesn't already exist, use
    your FTP program to create it. Your installation should look like
    this:

        (mt home)/plugins/Markdown.pl

2.  Once installed, Markdown will appear as an option in Movable Type's
    Text Formatting pop-up menu. This is selectable on a per-post basis.
    Markdown translates your posts to HTML when you publish; the posts
    themselves are stored in your MT database in Markdown format.

3.  If you also install SmartyPants 1.5 (or later), Markdown will offer
    a second text formatting option: "Markdown with SmartyPants". This
    option is the same as the regular "Markdown" formatter, except that
    automatically uses SmartyPants to create typographically correct
    curly quotes, em-dashes, and ellipses. See the SmartyPants web page
    for more information: <http://daringfireball.net/projects/smartypants/>

4.  To make Markdown (or "Markdown with SmartyPants") your default
    text formatting option for new posts, go to Weblog Config ->
    Preferences.

Note that by default, Markdown produces XHTML output. To configure
Markdown to produce HTML 4 output, see "Configuration", below.


### Blosxom ###

Markdown works with Blosxom version 2.x.

1.  Rename the "Markdown.pl" plug-in to "Markdown" (case is
    important). Movable Type requires plug-ins to have a ".pl"
    extension; Blosxom forbids it.

2.  Copy the "Markdown" plug-in file to your Blosxom plug-ins folder.
    If you're not sure where your Blosxom plug-ins folder is, see the
    Blosxom documentation for information.

3.  That's it. The entries in your weblog will now automatically be
    processed by Markdown.

4.  If you'd like to apply Markdown formatting only to certain posts,
    rather than all of them, see Jason Clark's instructions for using
    Markdown in conjunction with Blosxom's Meta plugin:
    
    <http://jclark.org/weblog/WebDev/Blosxom/Markdown.html>


### BBEdit ###

Markdown works with BBEdit 6.1 or later on Mac OS X. (It also works
with BBEdit 5.1 or later and MacPerl 5.6.1 on Mac OS 8.6 or later.)

1.  Copy the "Markdown.pl" file to appropriate filters folder in your
    "BBEdit Support" folder. On Mac OS X, this should be:

        BBEdit Support/Unix Support/Unix Filters/

    See the BBEdit documentation for more details on the location of
    these folders.

    You can rename "Markdown.pl" to whatever you wish.

2.  That's it. To use Markdown, select some text in a BBEdit document,
    then choose Markdown from the Filters sub-menu in the "#!" menu, or
    the Filters floating palette



Configuration
-------------

By default, Markdown produces XHTML output for tags with empty elements.
E.g.:

    <br />

Markdown can be configured to produce HTML-style tags; e.g.:

    <br>


### Movable Type ###

You need to use a special `MTMarkdownOptions` container tag in each
Movable Type template where you want HTML 4-style output:

    <MTMarkdownOptions output='html4'>
        ... put your entry content here ...
    </MTMarkdownOptions>

The easiest way to use MTMarkdownOptions is probably to put the
opening tag right after your `<body>` tag, and the closing tag right
before `</body>`.

To suppress Markdown processing in a particular template, i.e. to
publish the raw Markdown-formatted text without translation into
(X)HTML, set the `output` attribute to 'raw':

    <MTMarkdownOptions output='raw'>
        ... put your entry content here ...
    </MTMarkdownOptions>


### Command-Line ###

Use the `--html4tags` command-line switch to produce HTML output from a
Unix-style command line. E.g.:

    % perl Markdown.pl --html4tags foo.text

Type `perldoc Markdown.pl`, or read the POD documentation within the
Markdown.pl source code for more information.



Bugs
----

To file bug reports or feature requests please send email to:
<markdown@daringfireball.net>.







Donations
---------

Donations to support Markdown's development are happily accepted. See:
<http://daringfireball.net/projects/markdown/> for details.



Copyright and License
---------------------

Copyright (c) 2003-2004 John Gruber   
<http://daringfireball.net/>   
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:

* Redistributions of source code must retain the above copyright notice,
  this list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright
  notice, this list of conditions and the following disclaimer in the
  documentation and/or other materials provided with the distribution.

* Neither the name "Markdown" nor the names of its contributors may
  be used to endorse or promote products derived from this software
  without specific prior written permission.

This software is provided by the copyright holders and contributors "as
is" and any express or implied warranties, including, but not limited
to, the implied warranties of merchantability and fitness for a
particular purpose are disclaimed. In no event shall the copyright owner
or contributors be liable for any direct, indirect, incidental, special,
exemplary, or consequential damages (including, but not limited to,
procurement of substitute goods or services; loss of use, data, or
profits; or business interruption) however caused and on any theory of
liability, whether in contract, strict liability, or tort (including
negligence or otherwise) arising in any way out of the use of this
software, even if advised of the possibility of such damage.

# Einleitung

Siehe \ref{fig:diagramm}, die folgendes zeigt: 

- eine Sache,
- zweite Sache,
- dritte Sache.

![Diagramm\label{fig:diagramm}](/doc/images/runnable_measure_overview.png)

# Interfaces

Lorem

## Module Inputs

| Spalte linksbündig | Spalte zentriert | Spalte rechtsbündig |
| :---               | :--:             | ---:                |
| Zeile 1 a          | Zeile 1 b        | Zeile 1 c           |
| Zeile 2 a          | Zeile 2 b        | Zeile 2 c           |

## Module Outputs

| Spalte linksbündig | Spalte zentriert | Spalte rechtsbündig |
| :---               | :--:             | ---:                |
| Zeile 1 a          | Zeile 1 b        | Zeile 1 c           |
| Zeile 2 a          | Zeile 2 b        | Zeile 2 c           |


# Internal Data

Ipsum

| Spalte linksbündig | Spalte zentriert | Spalte rechtsbündig |
| :---               | :--:             | ---:                |
| Zeile 1 a          | Zeile 1 b        | Zeile 1 c           |
| Zeile 2 a          | Zeile 2 b        | Zeile 2 c           |


# Configuration Details

Lorem

| Spalte linksbündig | Spalte zentriert | Spalte rechtsbündig |
| :---               | :--:             | ---:                |
| Zeile 1 a          | Zeile 1 b        | Zeile 1 c           |
| Zeile 2 a          | Zeile 2 b        | Zeile 2 c           |


# Calibration Details

Ipsum

| Spalte linksbündig | Spalte zentriert | Spalte rechtsbündig |
| :---               | :--:             | ---:                |
| Zeile 1 a          | Zeile 1 b        | Zeile 1 c           |
| Zeile 2 a          | Zeile 2 b        | Zeile 2 c           |

Version History
---------------

1.0.1 (14 Dec 2004):

+	Changed the syntax rules for code blocks and spans. Previously,
	backslash escapes for special Markdown characters were processed
	everywhere other than within inline HTML tags. Now, the contents
	of code blocks and spans are no longer processed for backslash
	escapes. This means that code blocks and spans are now treated
	literally, with no special rules to worry about regarding
	backslashes.

	**NOTE**: This changes the syntax from all previous versions of
	Markdown. Code blocks and spans involving backslash characters
	will now generate different output than before.