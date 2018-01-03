======
evcape
======

``evcape`` makes your <kdb>caps lock</kdb> key work as both
<kbd>ctrl</kdb> and an <kbd>esc</kbd> key, depending on whether you
combine it with another key (acts as <kbd>ctrl</kbd>) or release it
immediately (acts as <kbd>esc</kbd>). this is ideal for vim bindings.

in general, ``evcape`` simulates an additional key press (e.g. escape
or backspace) when a modifier key (e.g. shift or control) is pressed
and immediately released.

``evcape`` is a small daemon that listens to keyboard events using the
linux input subsystem, and uses simple rules to detects patterns and
take corresponding actions.

it uses ``evdev``, ``udev`` and ``uinput`` and hence works with
wayland and on the console, unlike ``evcape``'s inspiration,
``xcape``.

crrent status
==============

*WARNING*: this is alpha quality software, use at your own risk!

- simple rule language for configuration works
- keyboard input event detection works
- keyboard simulation works
- monitoring of hotplug events (external keyboards) works

installation
============

``evcape`` is written using python 3.

make sure you have the python (3) libraries installed for:

- evdev
- pyudev
- six

on debian/ubuntu this would be::

  apt install python3-evdev python3-pyudev python3-six

alternatively, use a `virtualenv` for isolation::

  virtualenv --python=python3 venv
  source venv/bin/activate
  pip install -r requirements.txt

usage
=====

use your desktop environment (gnome has a ui for it in gnome-tweak-tool)
to make caps lock an extra control so that it becomes harmless.
alternatively, use something like this::

  setxkbmap -option "caps:ctrl_modifier"

then run evcape::

  ./evcape.py

you may need to run with root permissions to access raw input devices::

  sudo ./evcape.py

or, if you use a virtualenv::

  source venv/bin/activate
  python ./evcape.py

pass ``--help`` for usage options.

by default, the built-in rules make caps/control act as escape.
alternatively, specify your own rules on the command line.

to start upon login, one option is to use a systemd user service,
e.g. ``~/.config/systemd/user/evcape.service``.
here is an example with some custom rules::

  [Unit]
  Description=evcape

  [Service]
  ExecStart=/path/to/evcape.py \
      press:leftctrl,release:leftctrl=press:esc,release:esc \
      press:capslock,release:capslock=press:esc,release:esc \
      press:rightshift,release:rightshift=press:backspace,release:backspace \
      press:rightctrl,release:rightctrl=press:backspace,release:backspace
  Restart=always

  [Install]
  WantedBy=default.target

who wrote this?
===============

wouter bolsterlee. wbolster.

https://github.com/wbolster on github. star my repos. fork them. and so on.

https://twitter.com/wbolster on twitter. follow me. or say hi.

similar projects
================

* ``evcape`` is inspired by ``xcape`` (https://github.com/alols/xcape),s
  but is not limited to xorg.

* ``caps2esc`` (https://gitlab.com/interception/linux/plugins/caps2esc)s
  is a c implementation of ``xcape`` without the X dependency.
  it is part of a project called ‘interception tools’
  (https://gitlab.com/interception/linux/tools).
