---
title: New Game
---

[Home](../../Main%20Page.md) > [FF7](../../FF7.md) > [Technical](../Technical.md) > New Game

### Symptoms

When I select *New Game* from main menu, screen goes black and nothing
happens or the game crashes.

### Causes

There should be a FMV played here, and it's not because game can't find
codec to play it.

### Solution

This is probably your fault - you unchecked installing DirectShow and
DirectX drivers when installing the game. Game needs these drivers to
show FMVs, so you must reinstall the game - checking to install these
drivers. You can also try [this solution][] if installing DirectShow
don't help. Or [this solution][1] if you have some codec packs
installed.

[Back to Technical Problems page][]

  [this solution]: Movies.md "wikilink"
  [1]: NoMovies.md "wikilink"
  [Back to Technical Problems page]: ../Technical.md "wikilink"
