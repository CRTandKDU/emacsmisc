# Getting gblogger #
`gblogger` is part of the `emacsmisc` project hosted at: [emacsmisc](http://code.google.com/p/emacsmisc).  It has been tested with Emacs 23.x on Windows and on Ubuntu.

# Installing gblogger #
gblogger requires that [curl](http://curl.haxx.se/) is properly installed. (curl is a command line tool for transferring data with URL syntax, supporting FTP, FTPS, HTTP, HTTPS, SCP, SFTP, TFTP, TELNET, DICT, LDAP, LDAPS, FILE, IMAP, SMTP, POP3 and RTSP.)

gblogger also requires [dom.el](http://www.emacswiki.org/emacs/XmlParser) to access the DOM of a parsed XML document.  Make sure that `dom.el` is in the Emacs `load-path`.

Once downloaded, install the `gblogger` files in your Emacs `load-path`.

Customize the user/password declaration section of this file to memorize your GMail address and password by making the appropriate changes to the `Email` and `Passwd` fields (leaving the others as they are):

```
(setq *gblogger-user*
      '(("Email" . "YOUR-LOGIN@gmail.com")
	("Passwd" . "YOUR-PASSWORD")
	("service" . "blogger")
	("accountType" . "GOOGLE")
	("source" . "gblogger-emacs-1"))
      *gblogger-service*
      '((auth . "https://www.google.com/accounts/ClientLogin")
	(blogs . "http://www.blogger.com/feeds/default/blogs")
	)
      *gblogger-auth* nil
      )
```

Alternatively set the "Email" and "Passwd" values to `nil` in the file, gblogger will then prompt for them interactively when required.

Now make gblogger available, for instance by adding:

```
(require 'gblogger)
```

in your `.emacs` initialization file.

# Using gblogger #
In the current version there are basically just two commands, the first one to login into the Google Blogger service, the second one to post the content of the current buffer as a new post to a Blogger-hosted blog.

Before posting anything, identification to Google Blogger services is required.  Based on the credentials as edited in the previous section, logging in is done by invoking `gblogger-login`:

```
M-x gblogger-login
```

This looks at the globales set up earlier and query Google ClientLogin services for an authorization token which is then stored locally.  Once identified post can be sent to Blogger by invoking the `gblogger-post` command with:

```
M-x gblogger-post
```

When invoked interactively in a buffer, `gblogger-post` extracts the first line of the buffer as the _title_ of the post and the following lines, to the end of the buffer, as the _body_ of the post.  (This initial release does not handle tags/categories yet.)  Then it sends the new post to Blogger, prompting for which blog to post it to (in the minibuffer, where completion is available).

# Advanced Usage #
gblogger can also be used with a (preliminary) simple forms-based user interface in Emacs.  In this setup, the posts are also stored locally in a text file used by the Emacs Forms feature.

The form itself is specified in the `gblogger-control.el`file which specifies, among other parameters of the form, the posts file it operates on.  (See the Emacs Forms info for a detailed presentation of Forms.)

In order to invoke the form-based GUI to Blogger posting:

```
M-x forms-find-file gblogger-control.el
```

In the form-mode, new posts are created, for instance, by typing `C-c C-o` and posted, after user confirmation, when saving them to file by `C-x C-s`.  Other commands to navigate the posts are available with the `C-c` prefix (see the forms-mode info).

# License #
gblogger is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

gblogger is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with gblogger; if not, write to the Free Software
Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA

