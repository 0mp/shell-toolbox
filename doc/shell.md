SHELL(1) - General Commands Manual

# NAME

**shell** - Creates a temporary interactive shell session in a disposable working directory

# SYNOPSIS

**shell**
\[**-d**&nbsp;*directory*&nbsp;|&nbsp;**-k**]
\[*shell*]

# DESCRIPTION

The
**shell**
utility creates an interactive shell session with a clean environment
and with an empty working directory.

By specifying a specific
*shell*
on the command line, a shell other than the user's login shell may be
invoked.
If a specific shell is not requested, the
`SHELL`
environment variable will be used to infer what shell to start.

The basename of the named
*shell*
must correspond to a valid login shell and the actual shell that is
started will always be taken from the list of valid login shells (by
matching the basename of the specified
*shell*,
or
`$SHELL`,
against the basenames of
the allowed login shells).

The options are as follows:

**-d** *directory*

> Use the specified directory rather than a new temporary directory.
> If the directory does not already exist, it will be created.
> This directory will not be deleted when the shell session terminates.
> This option implies the
> **-k**
> option.

**-k**

> Keep the temprorary directory around after terminating the shell session.

# ENVIRONMENT

**shell**
uses the following environment variables:

`TMPDIR`

> Directory in which to create the working directory when the
> **-d**
> option is not used.

`SHELL`

> Used to determine what shell to start if a specific
> *shell*
> is not specified on the command line.

**shell**
clears the environment of the interactive shell that it starts, but
also sets the following environment variables:

`HOME`

> Set to the working directory where the shell is started.

`PATH`

> Set to the output of
> "**getconf PATH**".

`PS1`

> Set to the string
> '$&#160;'
> (dollar-sign and space).
> Note that some shells ignore this variable if passed from the parent
> environment.

`SHELL`

> Set to the absolute path of the real shell executable.
> This may be different from the
> *shell*
> mentioned on the command line as the actual shell used will always be
> picked from the list of valid login shells.

`TERM`

> Carried over from the parent environment.

# FILES

*/etc/shells*

> Used as a source for valid login shells on systems where
> "**getent shells**"
> does not work.

# EXAMPLES

Start a new shell in a new temporary directory:

	$ shell
	Starting /bin/ksh in /tmp/shell-ksh.lDv4uX48
	$ exit
	Removing /tmp/shell-ksh.lDv4uX48

Start a new
**ksh93**
shell in a temporary directory:

	$ shell ksh93
	Starting /usr/local/bin/ksh93 in /tmp/shell-ksh93.oct61lxx
	myself:/tmp/shell-ksh93.oct61lxx:1$ exit
	Removing /tmp/shell-ksh93.oct61lxx

Start a new
**bash**
shell in a specific directory:

	$ shell -d "$HOME/testing" bash
	Starting /usr/local/bin/bash in /home/myself/testing
	$ exit
	Leaving /home/myself/testing in place

# AUTHORS

Andreas Kusalananda K&#228;h&#228;ri &lt;[andreas.kahari@nbis.se](mailto:andreas.kahari@nbis.se)&gt;

# CAVEATS

For Solaris, the list of valid login shells is taken from the
shells(4)
manual on a Solaris 11.3 system.
This is because Solaris lacks
"**getent shells**"
and may also lack the
*/etc/shells*
file.

Unix - April 2, 2018