#
# SPDX-License-Identifier: ISC
#
# Copyright (c) 2014, 2017-2018 Todd C. Miller <Todd.Miller@sudo.ws>
#
# Permission to use, copy, modify, and distribute this software for any
# purpose with or without fee is hereby granted, provided that the above
# copyright notice and this permission notice appear in all copies.
#
# THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
# WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
# MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
# ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
# WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
# ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
# OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
#
# examples/Makefile.  Generated from Makefile.in by configure.
#

#### Start of system configuration section. ####

srcdir = .
docdir = $(datarootdir)/doc/$(PACKAGE_TARNAME)
exampledir = $(docdir)/examples
top_builddir = ..
top_srcdir = ..

# Our install program supports extra flags...
INSTALL = $(SHELL) $(top_srcdir)/install-sh -c
INSTALL_OWNER = -o $(install_uid) -g $(install_gid)

# Where to install things...
prefix = /usr/local
exec_prefix = $(prefix)
bindir = $(exec_prefix)/bin
sbindir = $(exec_prefix)/sbin
sysconfdir = /etc
libexecdir = $(exec_prefix)/libexec
datarootdir = $(prefix)/share
localstatedir = $(prefix)/var

# User and group ids the installed files should be "owned" by
install_uid = 0
install_gid = 0

#### End of system configuration section. ####

SHELL = /bin/bash

EXAMPLES = $(srcdir)/pam.conf $(srcdir)/sudo.conf $(srcdir)/sudoers \
	   $(srcdir)/syslog.conf
 
VERSION = 1.8.31p2
PACKAGE_TARNAME = sudo

all: $(EXAMPLES)

depend:

Makefile: $(srcdir)/Makefile.in
	cd $(top_builddir) && ./config.status --file examples/Makefile

pre-install:

install: install-doc

install-dirs:
	$(SHELL) $(top_srcdir)/mkinstalldirs $(DESTDIR)$(exampledir)

install-binaries:

install-includes:

install-doc: install-dirs
	for f in $(EXAMPLES); do $(INSTALL) $(INSTALL_OWNER) -m 0644 $$f $(DESTDIR)$(exampledir); done

install-plugin:

uninstall:
	-rm -rf	$(DESTDIR)$(exampledir)

splint:

cppcheck:

pvs-log-files:

pvs-studio:

check:

clean:

mostlyclean: clean

distclean: clean
	-rm -rf Makefile

clobber: distclean

realclean: distclean

cleandir: distclean
