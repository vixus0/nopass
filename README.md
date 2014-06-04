nopass
======

A password database that doesn't store passwords.
It just stores usernames, URLs and other details.
No need to store an encrypted database file or worry about safe syncing in the cloud.
At the moment this is only useful for *nix users.

Requirements
----------

* Python 3
* `xdotool` and `dmenu` for X interaction (eg. autotyping)

How to use
----------

Run `nop` for basic usage info. The main commands are:

* `[a]dd`: Add a new entry to the database.
* `[d]el`: Delete an entry from the database.
* `[p]rint`: Print an entry's fields to stdout.
* `[x]do`: Autotype username, password, etc. using xdotool.

Running any of these commands with the `-h` flag will display help for those commands. There is only one global flag `-f` which defines the location of the database file.

If you're not going to use autotyping, or it doesn't work for your situation you can easily combine *nopass* with `dmenu` and a clipboard tool like `xclip`.

```
nop p -d --pw | xclip -i
```

Autotyping
---------

The power of *nopass* is in its X interaction capabilities, leaving out the need to mess around with clipboards.

The command you'll use, probably bound to a hotkey, is:
```
nop x [--entry name]
```

The `win` and `type` entry fields are the most important here, as they help *nopass* autotype your details.

`win` is the substring used to match against window titles in the X environment. Make sure this is unique to the application/web site you want to match.

`type` defines how your details are entered. It has a simple syntax. Here's an example string for websites in Pentadactyl:
```
gi(user)[tab](pass)[return]
```
This means 'gi' will be typed into the active window, followed by the username defined in the entry, a Tab, the password and finally the Return key.

The `--entry` flag allows you to specify an entry, in which case *nopass* tries to find a matching window and focuses it for you before autotyping.
