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
`$PREFIX/share/X11/xkb/symbols/inet` and delete all lines pertaining to
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

Both variants also bind exclamation point to F24 so that the Yubikey can type
it.

Both variants alter Shift+`.` to still produce `.` instead of `•`.

Both variants change all keypad keys accessible through level-5 shift to the
non-keypad variants, since a number of terminal programs (eg, less and vim)
somehow don't understand the corresponding escape sequences.

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
- `\_` = Underscore
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

Yubikey Configuration
---------------------

If you want to use the Yubikey Neo with either of the layouts, you can
configure that with the following command:

```
  ykpersonalize -S15113309120a1816381c080d0e0f041a9591b389928a9896b89c888d8e8f849a242225212620271f2d23732b28
```

Note that `ykpersonalize`'s command-line argument parsing is broken, and using
the perhaps more natural `-S 15...` will result in it resetting the device map
to QWERTY. Also note that, though not documented, you can't change the scanmap
while the device is programmed, so you may need to do
```
  ykpersonalize -z -1
  ykpersonalize -z -2
```

first. (Note that this will clear all the configuration! In particular, it
destroys the factory-preset first configuration irrecoverably. Maybe there is
some way to change the scanmap without nuking it, but I have not found it.)

Derivation (`+` = "hold shift", indicated to Yubikey by setting bit 7):

```
  c  b  d  e  f  g  h  i  j  k  l  n  r  t  u  v
  R  N  ;  F  O  I  U  S  /  Y  E  J  K  L  A  W
 15 11 33 09 12 0a 18 16 38 1c 08 0d 0e 0f 04 1a

  C  B  D  E  F  G  H  I  J  K  L  N  R  T  U  V
 +R +N +; +F +O +I +U +S +/ +Y +E +J +K +L +A +W
 95 91 b3 89 92 8a 98 96 b8 9c 88 8d 8e 8f 84 9a

  0  1  2  3  4  5  6  7  8  9  ! \t \r
  7  5  8  4  9  3  0  2  -  6 F24 HT RET
 24 22 25 21 26 20 27 1f 2d 23 73 2b 28
```

See for reference http://www.freebsddiary.org/APC/usb_hid_usages.php
