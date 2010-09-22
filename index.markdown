---
title: Home
layout: default
---

An Ocaml binding for Yices 1, version 0.4. Based on CamlIDL, this library
allows the access to both Yices APIs (full and light), unsatisfiable
cores, bit vectors, and more experimental features (interrupting,
switching between APIs).

* [API (Ocamldoc)](api/)
* [Repo](http://github.com/polazarus/ocamlyices)
* [Wiki](http://github.com/polazarus/ocamlyices/wiki)

Requirements
============

*	Yices >= 1.0.26 < 2, http://yices.csl.sri.com,
	preferably without GMP statically linked.
	libyices.a or libyices.a must be installed on the system.

	You can use `./install-yices.sh yices.tar.gz` to install yices in `/usr/local`
	and register the DLL. If a warning appears about the absence of `libyices.so`,
	you may have to use configure with `--enable-custom`. You can change
	destination directories with
	`./install-yices yices.tar.gz /usr/local /usr/local/lib64`

*	GMP and GMP header (`gmp.h`)

*	Ocaml

*	Camlidl

*	For developers, to use the latest version from the repository: autoconf


WARNING
=======

Hardly tested! and only under Linux, but reported to work under MacOS X...


Setup
=====

Warning! Please make sure to uninstall any previous version beforehand.

	$ autoconf # Only if there is no configure
	$ ./configure
	$ make

Build the Ocamlyices library (for ocamlopt and ocamlc).
Part of the linking is done by an incremental, aka partial, linking, the rest is
done by ocamlc or ocamlopt when you use the Ocamlyices library.

	$ sudo make install

Install the library in ``DESTDIR/ocamlyices`` and possibly a DLL in
``DESTDIR/stublibs``. If you have Findlib installed on your system, it uses
Findlib default destination directory. Otherwise, it calls `ocamlc -where` and
uses the standard Ocaml directory.


Configure options: `./configure [OPTIONS]`
------------------------------------------  

	--enable-custom
	--disable-custom [DEFAULT]

Build the Ocamlyices for custom bytecode compilation (see ocamlc manual for
more information), rather than using a shared library. As a result, every
program using such a version of ocamlyices will be compilated with the
option `-custom`.

	--enable-force-static
	--disable-force-static [DEFAULT]

Embed the static version of the Yices library into the ocamlyices library.
Force `--enable-partial-linking`.

	--enable-partial-linking [DEFAULT]
	--disbable-partial-linking

Partial linking is mostly needed to the second option (force static). Also,
with this option the ocamlyices.cma/.cmxa does not depend on camlidl.


Usage
=====

With Ocamlfind:

    ocamlfind ocamlc/ocamlopt -package ocamlyices ...

Or without:

    ocamlc -I +ocamlyices nums.cma ocamlyices.cma ...
    ocamlopt -I +ocamlyices nums.cmxa ocamlyices.cmxa ...

_nums_ is required in order to handle GMP big integers as big_int.

Doc
---

A very limited ocamldoc is available in `doc/` provided you run this command:

    $ make doc

For the rest, see the official documentation at
http://yices.csl.sri.com/capi.shtml

Also, three examples are also avalaible in `examples/`.

Uninstall
=========

    $ sudo make uninstall

Uninstall the library

License
=======

Copyright (c) 2010, Mickaël Delahaye

Permission to use, copy, modify, and/or distribute this software for any purpose
with or without fee is hereby granted, provided that the above copyright notice
and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED “AS IS” AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH
REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND
FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT,
INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS
OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER
TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF
THIS SOFTWARE.
