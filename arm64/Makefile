#!/bin/sh

# (C) 2012-2015 Fathi Boudra <fathi.boudra@linaro.org>

# (C) 2015-2017 Francesco Bonanno <mibofra@frozenbox.org> , little changes for parrot arm rootfs tarballs.

# Calls all necessary live-build programs in the correct order to complete
# the bootstrap, chroot, binary, and source stage.

# You need live-build package installed and superuser privileges.

BUILD_NUMBER=1
BASEIMG=parrotsec-standard-3.5-arm64
IMAGEPREFIX=$(BASEIMG)-$(BUILD_NUMBER)
LOGFILE=$(IMAGEPREFIX).build-log.txt
CONFIGFILE=$(IMAGEPREFIX).config.tar.bz2
LISTFILE=$(IMAGEPREFIX).contents
CHROOTFILE=$(IMAGEPREFIX).files
PKGSFILE=$(IMAGEPREFIX).packages
TARGZFILE=$(IMAGEPREFIX).tar.gz
MD5SUMSFILE=$(IMAGEPREFIX).md5sums.txt
SHA1SUMSFILE=$(IMAGEPREFIX).sha1sums.txt

all:
	set -e; sudo lb build 2>&1 | tee $(LOGFILE)
	if [ -f live-image-arm64.tar.tar.gz ]; then \
		tar -jcf $(CONFIGFILE) auto/ config/ configure; \
		sudo mv live-image-arm64.contents $(LISTFILE); \
		sudo mv chroot.files $(CHROOTFILE); \
		sudo mv chroot.packages.install $(PKGSFILE); \
		sudo mv live-image-arm64.tar.tar.gz $(TARGZFILE); \
		md5sum $(LOGFILE) $(CONFIGFILE) $(LISTFILE) $(CHROOTFILE) $(PKGSFILE) $(TARGZFILE) > $(MD5SUMSFILE); \
		sha1sum $(LOGFILE) $(CONFIGFILE) $(LISTFILE) $(CHROOTFILE) $(PKGSFILE) $(TARGZFILE) > $(SHA1SUMSFILE); \
	fi

finalize:
	if [ -f live-image-arm64.tar.tar.gz ]; then \
		tar -jcf $(CONFIGFILE) auto/ config/ configure; \
		sudo mv live-image-arm64.contents $(LISTFILE); \
                sudo mv chroot.files $(CHROOTFILE); \
		sudo mv chroot.packages.install $(PKGSFILE); \
		sudo mv live-image-arm64.tar.tar.gz $(TARGZFILE); \
		md5sum $(LOGFILE) $(CONFIGFILE) $(LISTFILE) $(CHROOTFILE) $(PKGSFILE) $(TARGZFILE) > $(MD5SUMSFILE); \
		sha1sum $(LOGFILE) $(CONFIGFILE) $(LISTFILE) $(CHROOTFILE) $(PKGSFILE) $(TARGZFILE) > $(SHA1SUMSFILE); \
	fi

clean:
	sudo lb clean --purge
	rm -f $(BASEIMG)-*
	rm -rf config
	rm -rf .build
