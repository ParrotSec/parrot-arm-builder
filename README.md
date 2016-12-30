# parrot-arm-builder
ParrotSec rootfs arm (armhf at the moment) builder.

You need a Debian (or derivates) or a Parrot (or derivates) installation to use the build system.

(Work in progress to get it working on Ubuntu and derivates)

- Use need first to install live-build:

sudo apt-get install live-build

And after, cd into armhf and launch a ./configure && make

You can, before launching the build system, modify as you wish, the configure script, the Makefile,
and the hooks and other stuffs, under the customization directory.

The result will be a tarball, into a gzip or a lzma or other formats (you can decide into the configure script),
containing a binary directory, where there is all the rootfs for armhf devices.

All the code is under GPLv3+ .
