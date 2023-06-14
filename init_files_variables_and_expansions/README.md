	
The alias command makes it possible to launch any command or group of commands (inclusive of any options, arguments and redirection) by entering a pre-set string (i.e., sequence of characters).

That is, it allows a user to create simple names or abbreviations (even consisting of just a single character) for commands regardless of how complex the original commands are and then use them in the same way that ordinary commands are used.

A command is an instruction given by a user to tell a computer to do something. Commands are generally issued by typing them in at the command line (i.e., an all-text user interface) and then pressing the ENTER key, which passes them to the shell. A shell is a program that provides the traditional, text-only user interface for a Unix-like operating systems. Its primary function is to read commands and then execute (i.e., run) them.

The alias command is built into a number of shells including ash, bash (the default shell on most Linux systems), csh and ksh. It is one of several ways to customize the shell (another is setting environmental variables). Aliases are recognized only by the shell in which they are created, and they apply only for the user that creates them, unless that user is the root (i.e., administrative) user, which can create aliases for any user.

Listing and Creating Aliases

The general syntax for the alias command varies somewhat according to the shell. In the case of the bash shell it is

alias [-p] [name="value"]

When used with no arguments and with or without the -p option, alias provides a list of aliases that are in effect for the current user, i.e.,

alias

Some of the aliases listed are likely to be system-wide aliases that apply to all users and are created automatically for each new user for a particular shell. Aliases for any other shell can be seen by first switching to that shell and then using the alias command as above.

name is the name of the new alias and value is the command(s) which it initiates. The alias name and the replacement text can contain any valid shell input except for the equals sign ( = ).

The commands, including any options, arguments and redirection operators, are all enclosed within a single pair of quotation marks, which can be single quotes or double quotes. No spaces are permitted before or after the equals sign. Any number of aliases can be created simultaneously by enclosing the name in each name-value pair in quotes.

As a trivial example of alias creation, the alias p could be created for the commonly used pwd command, which shows the current location of the user in the directory structure (and which is an abbreviation for present working directory), by typing the following command and then pressing the ENTER key:

alias p="pwd"

Then, to show the current location, instead of typing pwd, the user would only have to type the letter p and press the ENTER key, i.e.,

p

An alias can be created with the same name as the core name of a command (i.e., a command without any options or arguments). In such case, it is the alias that is called (i.e., activated) first when the name is used, rather than the command with the same name. For example, an alias named ls could be created for the command ls -al as follows:

alias ls="ls -al"

ls is a commonly used command that by default lists the names of the files and directories within the current directory (i.e., the directory in which the user is currently working). The -a option instructs ls to also show any hidden files and directories, and the -l option tells it to provide detailed information about each file and subdirectory.

Such an alias can be disabled temporarily and the core command called by preceding it directly (i.e., with no spaces in between) with a backslash, i.e.,

\ls

It makes no difference whether double or single quotes are used when creating an alias. It can be slightly easier to use single quotes because this obviates the need to simultaneously use the shift key. Thus, the above example could have been written as

alias ls='ls -al'

This example could be simplified even further, again with no adverse effect on performance, by using a single character instead of two characters for the alias name, for example:

alias l='ls -al'

In addition to options, arguments can also be included in alias values. For example, to have the ls alias always display the contents of the /etc directory, it could be rewritten as:

alias l='ls -al /etc'

Multiple commands can be included in the same alias by inserting them within the same pair of quotation marks and separating them with semicolons. For example, the alias pl could be created to first launch pwd and then immediately launch ls:

alias pl='pwd; ls'

Aliases can even be created to call other aliases. For example, if the alias ls as shown earlier had already been created, then pl will launch it in the above example, otherwise it will launch the conventional ls command. If the aliases p and l shown in earlier examples have already been created, then the above example could alternatively be written as

alias pl='p; l'

The following is an example of creating two separate aliases simultaneously, as contrasted with creating a single alias that launches two separate commands:

alias p="pwd"; l="ls -al"

As an example of an alias for a series of commands linked by a pipe (represented by a vertical line), the alias dir can be created to generate a list of the names of and information about all of the subdirectories in the current directory:

alias dir="ls -al | grep ^d"

Here ls -al obtains a listing of all files and directories in the current directory. Its output is sent by the pipe to the filter grep, which then searches for lines beginning with the letter d (as all directories have a line returned by ls -al that begins with d). The caret (i.e., upward-pointing angular character) before d tells grep to search only for lines beginning with that letter.

Not only can options and arguments be used in the command(s) that an alias can substitute for, but they can also be used with an alias that has already been created. As a trivial example, supposing the alias l is created for the ls command:

alias l="ls -a"

Then, the alias l could be used with any argument that the command ls could be used with. For example, to list the files and directories in the the /etc directory:

l /etc

The alias l could also be used with any option that the command ls could be used with. For example:

l -l /etc

The alias command is unusual in that it only has a single option. That option, -p, tells it to display a list of the aliases for the current user on the current shell. This might be helpful if used when creating an alias, but it is, of course, redundant when the alias command is used without arguments.

Uses For Aliases

There are several types of uses for aliases. They include:

(1) Reducing the amount of typing that is necessary for commands or groups of commands that are long and/or tedious to type. These commands could include opening a file that is frequently used for studying or editing.

For example, if a user often accesses the Apache web server configuration file, which is /etc/httpd/conf/httpd.conf on Red Hat Linux 9, and uses the gedit text editor to read it, such user might type each time:

gedit /etc/httpd/conf/httpd.conf
