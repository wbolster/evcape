======
evcape
======

Make tapping <kbd>Ctrl</kdb> or <kdb>Caps Lock</kdb> send <kbd>Esc</kdb>. Ideal for vim bindings.

``evcape`` is designed to simulate additional key press (for instance escape or backspace)
when modifier keys (Shift, Control) are pressed and immediately released.

This tools is a small daemon that listens to keyboard events using the
linux input subsystem, and uses simple rules to detects patterns and
take corresponding actions.

It uses ``evdev``, ``udev`` and ``uinput`` and hence works with wayland and
on the console, unlike ``evcape``'s inspiration, ``xcape``.

Usage
==============

.. code:: sh

  # if using capslock as in DEFAULT_RULES
  setxkbmap -option "caps:ctrl_modifier" 
  # run without modified device permissions (need root)
  sudo ./evcape.py

Dependencies
==============

``evcape`` uses python's evdev and udev libaries.
On debian, ``apt install python3-evdev python3-pyudev``

Current status
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

use your system packages, or use a `virtualenv` for isolation::

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

Who wrote this?
===============

wouter bolsterlee. wbolster.

https://github.com/wbolster on github. star my repos. fork them. and so on.

https://twitter.com/wbolster on twitter. follow me. or say hi.

Similar projects
================

``evcape`` is inspired by ``xcape`` (https://github.com/alols/xcape),
but is not limited to xorg.


``caps2esc`` (https://gitlab.com/interception/linux/plugins/caps2esc) is a c implementation of ``xcape`` without the X dependency. It is part of ``interception tools`` (https://gitlab.com/interception/linux/tools)
