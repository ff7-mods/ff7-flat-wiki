---
title: Engine Basics
---

[Home](Main%20Page.md) > [FF7](FF7.md) > Engine Basics

## Parts of the Engine

The engine used to power Final Fantasy 7 is split into several modules.
This allowed the programming team to break apart into very distinct
groups. It also created a very diverse game playing environment. It also
allowed the artists to only have to work within their own module,
keeping the artwork as dynamic as possible.

The module system allowed for a single point of entry into, and exit out
of, each distinct part of the game. The PSX, which the game was
originally developed for, had very limited resources. With only 1
megabyte of video ram and 2 megabytes of system ram, data had to be
banked in and out efficiently. Modules were a clean way to dump whole
parts of the engine to make way for other parts.

The core system is made up of six modules. They are called the kernel,
field, menu, world map, battle, and mini game. They are arranged in the
following order.

  

<center>

![][1]

</center>

  

## Generic Program Flow

Not every module is accessible by every other module. There is a
distinct flow between them. For example, you can not access the menu
from battle, much to the chagrin of the poor user who had forgotten to
equip some last minute item. The field module, second only to the
kernel, drives the game. It includes a powerful scripting system that
can call any module within the game.

  [1]: ../../assets/Engine%20parts.jpg "Engine_parts.jpg"
