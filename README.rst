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

- keyboard input event detection works
- keyboard simulation works
- monitoring of hotplug events (external keyboards) works
- rules are built-in and can only be changed by editing the source code

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
