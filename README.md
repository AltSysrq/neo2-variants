Neo2 Keyboard Layout Variants
=============================

This repository  hosts an  XKB file  containing variants  of the  Neo2 keyboard
layout,  which can  be  found  at http://neo-layout.org/  and  ships with  X11.
Familariaty with this layout is assumed for the rest of this document.

The variants serve three main purposes:

- I use right-alt  a lot (especially in  Emacs), so remapping it  to Mod4 isn't
  really acceptable.

- I don't own  any keyboard with an  ISO layout, which is assumed  by Neo. This
  means the  only _other_ Mod4  key (after rebinding  right-alt back to  an alt
  key) doesn't actually exist on a US  keyboard. While both exist on a Japanese
  keyboard, it is more  useful to use the input mode-switch  keys at the thumbs
  for these modifiers.

- Change the number bar to be like Dvorak Classic instead of Qwerty.

A decent amount of this is probably particular to the way I learned to type; in
particular, the changes to right shift are probably unwelcome by many.

I  haven't  even attempted  to  port  these  modifications  to the  Windows  or
Macintosh implementations  of the layout,  and have  no attention to  doing so.
Anyone interested is  encouraged to upgrade their operating system  to one that
uses XKB.

Installation
------------

Simply copy `neo2v` to  `$PREFIX/share/X11/xkb/symbols` (`$PREFIX` is generally
`/usr` or `/usr/local`).

You can switch to the layouts with `setxkbmap`:
```sh
setxkbmap neo2v neo2v_us
setxkbmap neo2v neo2v_hhjp
```

Differences from standard Neo2 (common)
---------------------------------------

The right alt key is always actually right alt in all the variants.

The keys between  and including the ones  labelled `1` and `=`  are rotated one
space to the right. This moves _all_  the symbols on each key. Then, the digits
are reordered to match Dvorak Classic;  this does _not_ affect other symbols on
the keys. This results in a top bar  as shown below. Dead keys are indicated by
composing them with `a` or `c`.

```
Shifted         ǎ—°§ℓ»«$€„“”ç
Unshifted       â-7531902468à
```

US Variant
----------

- The key standard Neo2 maps to the right-hand-side Mod3 (labelled backslash on
  a US keyboard) is instead mapped to Mod4.

- Right shift is remapped to Escape since I've never used it for shifting.
