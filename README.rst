======
evcape
======

``evcape`` makes modifier keys (shift, control) more useful
by simulating another key press (for instance escape or backspace)
when they are pressed and immediately released.

this tools is a small daemon that listens to keyboard events using the
linux input subsystem, and uses simple rules to detects patterns and
take corresponding actions.

it uses ``evdev``, ``udev`` and ``uinput`` and hence works with wayland and
on the console.

current status
==============

*WARNING*: this is alpha quality software, use at your own risk!

- keyboard input event detection works
- keyboard simulation works
- monitoring of hotplug events (external keyboards) works

who wrote this?
===============

wouter bolsterlee. wbolster.

https://github.com/wbolster on github. star my repos. fork them. and so on.

https://twitter.com/wbolster on twitter. follow me. or say hi.

similar projects
================

``evcape`` is inspired by ``xcape`` (https://github.com/alols/xcape),
but is not limited to xorg.
