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

Note that if you are using X11 autoconfiguration via evdev instead of manual
configuration, evdev will for some reason override the bindings for the
modifier keys. You currently will need to edit
`$PREFIX/share/X11/xkb/symbols/evdev` and delete all lines pertaining to
Henkan, Muhenkan, and Hiragana/Katakana.

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

This  is targetted  at the  generic 104-key  US layout,  preferably one  with a
single-line enter key, and backslash placed between it and backspace.

- The key standard Neo2 maps to the right-hand-side Mod3 (labelled backslash on
  a US keyboard) is instead mapped to Mod4.

- Right shift is remapped to Escape since I've never used it for shifting.

Happy Hacking JP Variant
------------------------

This is targetted at the JP line of Happy Hacking keyboards. I'm unclear on how
consistent Japanese layouts are, particularly with respect to modifiers; it may
or may not be appropriate for others.

For  reference,  the  physical  layout  of the  bottom  (thumb)  row  is  (with
gratuitous ASCII approximation):
```
  [Fn   ][HHLogo][<>    ][Alt   ][(/)   ][Space         ][(_)   ][Kana  ][Alt   ][Fn    ]
```

`<>`  is   the  Windows  key.  `(/)`   is  Muhenkan  ("no  conversion"   /  "no
transformation" (of kana  to kanji)). `(_)` is  Henkan ("conversion"). "HHLogo"
is "Hankaku/Zankaku" ("halfwidth/fullwidth").

This variant makes the following bindings:

- `(/)` Muhenkan = Mod3
- `(_)` Henkan = Mod4
- Kana = Compose
- `]` (corresponding to backslash on a US keyboard) = Enter
- `¥` = Backspace

The final two are simply there to make the key they are adjacent to effectively
larger. The  former would  be another Mod4  key in standard  Neo2, but  this is
unnecessary since  the thumb  can handle it  independently. The  latter doesn't
appear to correspond to anything on an  ISO 105-key keyboard and has no binding
at all in standard Neo2.

CapsLock is untouched (from the `de`  default of actually being capslock) since
it is  not directly accessible and  cannot be usefully chorded.  Right shift is
untouched  since it  is unusably  far away  from the  normal position  of one's
hands, an impressive achievement on such a small keyboard.

Hankaku/Zankaku  is currently  unbound  because I  couldn't  think of  anything
useful to do with it.
