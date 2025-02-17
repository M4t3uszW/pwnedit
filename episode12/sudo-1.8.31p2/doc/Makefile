#
# SPDX-License-Identifier: ISC
#
# Copyright (c) 2010-2015, 2017-2018 Todd C. Miller <Todd.Miller@sudo.ws>
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
# doc/Makefile.  Generated from Makefile.in by configure.
#

#### Start of system configuration section. ####

srcdir = .
docdir = $(datarootdir)/doc/$(PACKAGE_TARNAME)
top_builddir = ..
top_srcdir = ..

# Tools to use
SED = /usr/bin/sed
IGOR = igor
MANDOC = mandoc
MANCOMPRESS = 
MANCOMPRESSEXT = 
TR = /usr/bin/tr

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
mandir = $(prefix)/man

# Directory to copy man pages from
mansrcdir = .

# Directory in which to install the man page
mantype = mdoc
mansectsu = 8
mansectform = 5
mandirexe = $(mandir)/man1
mandirsu = $(mandir)/man$(mansectsu)
mandirform = $(mandir)/man$(mansectform)

# User and group ids the installed files should be "owned" by
install_uid = 0
install_gid = 0

# Set to non-empty for development mode
DEVEL = 

#### End of system configuration section. ####

SHELL = /bin/bash

DOCS = $(mansrcdir)/cvtsudoers.$(mantype) $(mansrcdir)/sudo.$(mantype) \
       $(mansrcdir)/sudo.conf.$(mantype) $(mansrcdir)/sudo_plugin.$(mantype) \
       $(mansrcdir)/sudoers.$(mantype) $(mansrcdir)/sudoers.ldap.$(mantype) \
       $(mansrcdir)/sudoers_timestamp.$(mantype) \
       $(mansrcdir)/sudoreplay.$(mantype) $(mansrcdir)/visudo.$(mantype)

DEVDOCS = $(srcdir)/cvtsudoers.man.in $(srcdir)/sudo.conf.man.in \
	  $(srcdir)/sudo.man.in $(srcdir)/sudo_plugin.man.in \
	  $(srcdir)/sudoers.ldap.man.in $(srcdir)/sudoers.man.in \
	  $(srcdir)/sudoers_timestamp.man.in $(srcdir)/sudoreplay.man.in \
	  $(srcdir)/visudo.man.in

OTHER_DOCS = $(top_srcdir)/ChangeLog $(top_srcdir)/README \
	     $(top_srcdir)/NEWS $(srcdir)/HISTORY $(srcdir)/CONTRIBUTORS \
	     $(srcdir)/LICENSE $(srcdir)/TROUBLESHOOTING $(srcdir)/UPGRADE

OTHER_DOCS_LDAP = $(top_srcdir)/README.LDAP $(srcdir)/schema.*

VERSION = 1.8.31p2
PACKAGE_TARNAME = sudo

all: $(DEVDOCS) $(DOCS)

igor: all
	@if [ "$(mantype)" != "mdoc" ]; then \
	    echo "make igor only supported for mdoc manuals" 1>&2; \
	    exit 1; \
	else \
	    rval=0; \
	    for m in $(DOCS); do \
		echo $(IGOR) -D $$m; \
		$(IGOR) -D $$m || rval=`expr $$rval + $$?`; \
	    done; \
	    exit $$rval; \
	fi

lint: all
	@if [ "$(mantype)" != "mdoc" ]; then \
	    echo "make lint only supported for mdoc manuals" 1>&2; \
	    exit 1; \
	else \
	    rval=0; \
	    for m in $(DOCS); do \
		echo $(MANDOC) -Tlint -Wstyle $$m; \
		$(MANDOC) -Tlint -Wstyle $$m || rval=`expr $$rval + $$?`; \
	    done; \
	    exit $$rval; \
	fi

depend:

Makefile: $(srcdir)/Makefile.in
	cd $(top_builddir) && ./config.status --file doc/Makefile

.SUFFIXES: .man

$(srcdir)/sudo.man.in: $(srcdir)/sudo.mdoc.in $(srcdir)/sudo.man.in.sed
	@if [ -n "$(DEVEL)" ]; then \
	    echo "Generating $@"; \
	    mansectsu=`echo @MANSECTSU@|$(TR) A-Z a-z`; \
	    mansectform=`echo @MANSECTFORM@|$(TR) A-Z a-z`; \
	    $(SED) -e 's/^\(\.nr [A-Z][A-Z]\) .[A-Z][A-Z]MAN./\1 1/' -e "s/$$mansectsu/8/g" -e "s/$$mansectform/5/g" $(srcdir)/sudo.mdoc.in | $(MANDOC) -Tman | $(SED) -e 's/^\(\.TH "SUDO" \)"8"\(.*\)/\1"'$$mansectsu'"\2/' -e "s/(5)/($$mansectform)/g" -e "s/(8)/($$mansectsu)/g" -f $(srcdir)/sudo.man.in.sed > $@; \
	fi

fixman.sed: $(srcdir)/fixman.sh
	$(SHELL) $(srcdir)/fixman.sh $@

$(mansrcdir)/sudo.man: $(top_builddir)/config.status $(srcdir)/sudo.man.in fixman.sed
	(cd $(top_builddir) && $(SHELL) config.status --file=-) < $(srcdir)/sudo.man.in | $(SED) -f fixman.sed > $@

$(mansrcdir)/sudo.mdoc: $(top_builddir)/config.status $(srcdir)/sudo.mdoc.in
	cd $(top_builddir) && $(SHELL) config.status --file=doc/$@

$(srcdir)/visudo.man.in: $(srcdir)/visudo.mdoc.in
	@if [ -n "$(DEVEL)" ]; then \
	    echo "Generating $@"; \
	    mansectsu=`echo @MANSECTSU@|$(TR) A-Z a-z`; \
	    mansectform=`echo @MANSECTFORM@|$(TR) A-Z a-z`; \
	    $(SED) -e "s/$$mansectsu/8/g" -e "s/$$mansectform/5/g" $(srcdir)/visudo.mdoc.in | $(MANDOC) -Tman | $(SED) -e 's/^\(\.TH "VISUDO" \)"8"\(.*\)/\1"'$$mansectsu'"\2/' -e "s/(5)/($$mansectform)/g" -e "s/(8)/($$mansectsu)/g" > $@; \
	fi

$(mansrcdir)/visudo.man: $(top_builddir)/config.status $(srcdir)/visudo.man.in fixman.sed
	(cd $(top_builddir) && $(SHELL) config.status --file=-) < $(srcdir)/visudo.man.in | $(SED) -f fixman.sed > $@

$(mansrcdir)/visudo.mdoc: $(top_builddir)/config.status $(srcdir)/visudo.mdoc.in
	cd $(top_builddir) && $(SHELL) config.status --file=doc/$@

$(srcdir)/sudo.conf.man.in: $(srcdir)/sudo.conf.mdoc.in
	@if [ -n "$(DEVEL)" ]; then \
	    echo "Generating $@"; \
	    mansectsu=`echo @MANSECTSU@|$(TR) A-Z a-z`; \
	    mansectform=`echo @MANSECTFORM@|$(TR) A-Z a-z`; \
	    $(SED) -e 's/^\(\.nr [A-Z][A-Z]\) .[A-Z][A-Z]MAN./\1 1/' -e "s/$$mansectsu/8/g" -e "s/$$mansectform/5/g" $(srcdir)/sudo.conf.mdoc.in | $(MANDOC) -Tman | $(SED) -e 's/^\(\.TH "SUDO.CONF" \)"5"\(.*\)/\1"'$$mansectform'"\2/' -e "s/(5)/($$mansectform)/g" -e "s/(8)/($$mansectsu)/g" -f $(srcdir)/sudo.conf.man.in.sed > $@; \
	fi

$(mansrcdir)/sudo.conf.man: $(top_builddir)/config.status $(srcdir)/sudo.conf.man.in fixman.sed
	(cd $(top_builddir) && $(SHELL) config.status --file=-) < $(srcdir)/sudo.conf.man.in | $(SED) -f fixman.sed > $@

$(mansrcdir)/sudo.conf.mdoc: $(top_builddir)/config.status $(srcdir)/sudo.conf.mdoc.in
	cd $(top_builddir) && $(SHELL) config.status --file=doc/$@

$(srcdir)/sudoers.man.in: $(srcdir)/sudoers.mdoc.in $(srcdir)/sudoers.man.in.sed
	@if [ -n "$(DEVEL)" ]; then \
	    echo "Generating $@"; \
	    mansectsu=`echo @MANSECTSU@|$(TR) A-Z a-z`; \
	    mansectform=`echo @MANSECTFORM@|$(TR) A-Z a-z`; \
	    $(SED) -e 's/^\(\.nr [A-Z][A-Z]\) .[A-Z][A-Z]MAN./\1 1/' -e "s/$$mansectsu/8/g" -e "s/$$mansectform/5/g" $(srcdir)/sudoers.mdoc.in | $(MANDOC) -Tman | $(SED) -e 's/^\(\.TH "SUDOERS" \)"5"\(.*\)/\1"'$$mansectform'"\2/' -e "s/(5)/($$mansectform)/g" -e "s/(8)/($$mansectsu)/g" -f $(srcdir)/sudoers.man.in.sed> $@; \
	fi

$(mansrcdir)/sudoers.man: $(top_builddir)/config.status $(srcdir)/sudoers.man.in fixman.sed
	(cd $(top_builddir) && $(SHELL) config.status --file=-) < $(srcdir)/sudoers.man.in | $(SED) -f fixman.sed > $@

$(mansrcdir)/sudoers.mdoc: $(top_builddir)/config.status $(srcdir)/sudoers.mdoc.in $(srcdir)/fixmdoc.sed
	(cd $(top_builddir) && $(SHELL) config.status --file=-) < $(srcdir)/sudoers.mdoc.in | $(SED) -f $(srcdir)/fixmdoc.sed > $@

$(srcdir)/sudoers.ldap.man.in: $(srcdir)/sudoers.ldap.mdoc.in
	@if [ -n "$(DEVEL)" ]; then \
	    echo "Generating $@"; \
	    mansectsu=`echo @MANSECTSU@|$(TR) A-Z a-z`; \
	    mansectform=`echo @MANSECTFORM@|$(TR) A-Z a-z`; \
	    $(SED) -e "s/$$mansectsu/8/g" -e "s/$$mansectform/5/g" $(srcdir)/sudoers.ldap.mdoc.in | $(MANDOC) -Tman | $(SED) -e 's/^\(\.TH "SUDOERS.LDAP" \)"5"\(.*\)/\1"'$$mansectform'"\2/' -e "s/(5)/($$mansectform)/g" -e "s/(8)/($$mansectsu)/g" > $@; \
	fi

$(mansrcdir)/sudoers.ldap.man: $(top_builddir)/config.status $(srcdir)/sudoers.ldap.man.in fixman.sed
	(cd $(top_builddir) && $(SHELL) config.status --file=-) < $(srcdir)/sudoers.ldap.man.in | $(SED) -f fixman.sed > $@

$(mansrcdir)/sudoers.ldap.mdoc: $(top_builddir)/config.status $(srcdir)/sudoers.ldap.mdoc.in
	cd $(top_builddir) && $(SHELL) config.status --file=doc/$@

$(srcdir)/sudoers_timestamp.man.in: $(srcdir)/sudoers_timestamp.mdoc.in
	@if [ -n "$(DEVEL)" ]; then \
	    echo "Generating $@"; \
	    mansectsu=`echo @MANSECTSU@|$(TR) A-Z a-z`; \
	    mansectform=`echo @MANSECTFORM@|$(TR) A-Z a-z`; \
	    $(SED) -e "s/$$mansectsu/8/g" -e "s/$$mansectform/5/g" $(srcdir)/sudoers_timestamp.mdoc.in | $(MANDOC) -Tman | $(SED) -e 's/^\(\.TH "SUDOERS_TIMESTAMP" \)"5"\(.*\)/\1"'$$mansectform'"\2/' -e "s/(5)/($$mansectform)/g" -e "s/(8)/($$mansectsu)/g" > $@; \
	fi

$(mansrcdir)/sudoers_timestamp.man: $(top_builddir)/config.status $(srcdir)/sudoers_timestamp.man.in fixman.sed
	(cd $(top_builddir) && $(SHELL) config.status --file=-) < $(srcdir)/sudoers_timestamp.man.in | $(SED) -f fixman.sed > $@

$(mansrcdir)/sudoers_timestamp.mdoc: $(top_builddir)/config.status $(srcdir)/sudoers_timestamp.mdoc.in
	cd $(top_builddir) && $(SHELL) config.status --file=doc/$@

$(srcdir)/cvtsudoers.man.in: $(srcdir)/cvtsudoers.mdoc.in
	@if [ -n "$(DEVEL)" ]; then \
	    echo "Generating $@"; \
	    mansectsu=`echo @MANSECTSU@|$(TR) A-Z a-z`; \
	    mansectform=`echo @MANSECTFORM@|$(TR) A-Z a-z`; \
	    $(SED) -e "s/$$mansectsu/8/g" -e "s/$$mansectform/5/g" $(srcdir)/cvtsudoers.mdoc.in | $(MANDOC) -Tman | $(SED) -e "s/(5)/($$mansectform)/g" -e "s/(8)/($$mansectsu)/g" > $@; \
	fi

$(mansrcdir)/cvtsudoers.man: $(top_builddir)/config.status $(srcdir)/cvtsudoers.man.in fixman.sed
	(cd $(top_builddir) && $(SHELL) config.status --file=-) < $(srcdir)/cvtsudoers.man.in | $(SED) -f fixman.sed > $@

$(mansrcdir)/cvtsudoers.mdoc: $(top_builddir)/config.status $(srcdir)/cvtsudoers.mdoc.in
	cd $(top_builddir) && $(SHELL) config.status --file=doc/$@

$(srcdir)/sudoreplay.man.in: $(srcdir)/sudoreplay.mdoc.in
	@if [ -n "$(DEVEL)" ]; then \
	    echo "Generating $@"; \
	    mansectsu=`echo @MANSECTSU@|$(TR) A-Z a-z`; \
	    mansectform=`echo @MANSECTFORM@|$(TR) A-Z a-z`; \
	    $(SED) -e "s/$$mansectsu/8/g" -e "s/$$mansectform/5/g" $(srcdir)/sudoreplay.mdoc.in | $(MANDOC) -Tman | $(SED) -e 's/^\(\.TH "SUDOREPLAY" \)"8"\(.*\)/\1"'$$mansectsu'"\2/' -e "s/(5)/($$mansectform)/g" -e "s/(8)/($$mansectsu)/g" > $@; \
	fi

$(mansrcdir)/sudoreplay.man: $(top_builddir)/config.status $(srcdir)/sudoreplay.man.in fixman.sed
	(cd $(top_builddir) && $(SHELL) config.status --file=-) < $(srcdir)/sudoreplay.man.in | $(SED) -f fixman.sed > $@

$(mansrcdir)/sudoreplay.mdoc: $(top_builddir)/config.status $(srcdir)/sudoreplay.mdoc.in
	cd $(top_builddir) && $(SHELL) config.status --file=doc/$@

$(srcdir)/sudo_plugin.man.in: $(srcdir)/sudo_plugin.mdoc.in
	@if [ -n "$(DEVEL)" ]; then \
	    echo "Generating $@"; \
	    mansectsu=`echo @MANSECTSU@|$(TR) A-Z a-z`; \
	    mansectform=`echo @MANSECTFORM@|$(TR) A-Z a-z`; \
	    $(SED) -e "s/$$mansectsu/8/g" -e "s/$$mansectform/5/g" $(srcdir)/sudo_plugin.mdoc.in | $(MANDOC) -Tman | $(SED) -e 's/^\(\.TH "SUDO_PLUGIN" \)"8"\(.*\)/\1"'$$mansectsu'"\2/' -e "s/(5)/($$mansectform)/g" -e "s/(8)/($$mansectsu)/g" > $@; \
	fi

$(mansrcdir)/sudo_plugin.man: $(top_builddir)/config.status $(srcdir)/sudo_plugin.man.in fixman.sed
	(cd $(top_builddir) && $(SHELL) config.status --file=-) < $(srcdir)/sudo_plugin.man.in | $(SED) -f fixman.sed > $@

$(mansrcdir)/sudo_plugin.mdoc: $(top_builddir)/config.status $(srcdir)/sudo_plugin.mdoc.in
	cd $(top_builddir) && $(SHELL) config.status --file=doc/$@

pre-install:

install: install-doc

install-dirs:
	$(SHELL) $(top_srcdir)/mkinstalldirs $(DESTDIR)$(docdir) \
	    $(DESTDIR)$(mandirexe) $(DESTDIR)$(mandirform) $(DESTDIR)$(mandirsu)

install-binaries:

install-includes:

install-doc: install-dirs
	for f in $(OTHER_DOCS); do $(INSTALL) $(INSTALL_OWNER) -m 0644 $$f $(DESTDIR)$(docdir); done
	#for f in $(OTHER_DOCS_LDAP); do $(INSTALL) $(INSTALL_OWNER) -m 0644 $$f $(DESTDIR)$(docdir); done
	$(INSTALL) $(INSTALL_OWNER) -m 0644 $(mansrcdir)/cvtsudoers.$(mantype) $(DESTDIR)$(mandirexe)/cvtsudoers.1
	$(INSTALL) $(INSTALL_OWNER) -m 0644 $(mansrcdir)/sudo.$(mantype) $(DESTDIR)$(mandirsu)/sudo.$(mansectsu)
	$(INSTALL) $(INSTALL_OWNER) -m 0644 $(mansrcdir)/sudo_plugin.$(mantype) $(DESTDIR)$(mandirsu)/sudo_plugin.$(mansectsu)
	$(INSTALL) $(INSTALL_OWNER) -m 0644 $(mansrcdir)/sudoreplay.$(mantype) $(DESTDIR)$(mandirsu)/sudoreplay.$(mansectsu)
	$(INSTALL) $(INSTALL_OWNER) -m 0644 $(mansrcdir)/visudo.$(mantype) $(DESTDIR)$(mandirsu)/visudo.$(mansectsu)
	$(INSTALL) $(INSTALL_OWNER) -m 0644 $(mansrcdir)/sudo.conf.$(mantype) $(DESTDIR)$(mandirform)/sudo.conf.$(mansectform)
	$(INSTALL) $(INSTALL_OWNER) -m 0644 $(mansrcdir)/sudoers.$(mantype) $(DESTDIR)$(mandirform)/sudoers.$(mansectform)
	$(INSTALL) $(INSTALL_OWNER) -m 0644 $(mansrcdir)/sudoers_timestamp.$(mantype) $(DESTDIR)$(mandirform)/sudoers_timestamp.$(mansectform)
	#$(INSTALL) $(INSTALL_OWNER) -m 0644 $(mansrcdir)/sudoers.ldap.$(mantype) $(DESTDIR)$(mandirform)/sudoers.ldap.$(mansectform)
	@if test -n "$(MANCOMPRESS)"; then \
	    for f in $(mandirexe)/cvtsudoers.1 $(mandirsu)/sudo.$(mansectsu) $(mandirsu)/sudo_plugin.$(mansectsu) $(mandirsu)/sudoreplay.$(mansectsu) $(mandirsu)/visudo.$(mansectsu) $(mandirform)/sudo.conf.$(mansectform) $(mandirform)/sudoers.$(mansectform) $(mandirform)/sudoers_timestamp.$(mansectform) $(mandirform)/sudoers.ldap.$(mansectform); do \
		if test -f $(DESTDIR)$$f; then \
		    echo $(MANCOMPRESS) -f $(DESTDIR)$$f; \
		    $(MANCOMPRESS) -f $(DESTDIR)$$f; \
		fi; \
	    done; \
	    rm -f $(DESTDIR)$(mandirsu)/sudoedit.$(mansectsu)$(MANCOMPRESSEXT); \
	    echo ln -s sudo.$(mansectsu)$(MANCOMPRESSEXT) $(DESTDIR)$(mandirsu)/sudoedit.$(mansectsu)$(MANCOMPRESSEXT); \
	    ln -s sudo.$(mansectsu)$(MANCOMPRESSEXT) $(DESTDIR)$(mandirsu)/sudoedit.$(mansectsu)$(MANCOMPRESSEXT); \
	else \
	    rm -f $(DESTDIR)$(mandirsu)/sudoedit.$(mansectsu); \
	    echo ln -s sudo.$(mansectsu) $(DESTDIR)$(mandirsu)/sudoedit.$(mansectsu); \
	    ln -s sudo.$(mansectsu) $(DESTDIR)$(mandirsu)/sudoedit.$(mansectsu); \
	fi

install-plugin:

uninstall:
	-rm -rf	$(DESTDIR)$(docdir)
	-rm -f	$(DESTDIR)$(mandirexe)/cvtsudoers.1 \
		$(DESTDIR)$(mandirsu)/sudo.$(mansectsu) \
		$(DESTDIR)$(mandirsu)/sudoedit.$(mansectsu) \
		$(DESTDIR)$(mandirsu)/sudo_plugin.$(mansectsu) \
		$(DESTDIR)$(mandirsu)/sudoreplay.$(mansectsu) \
		$(DESTDIR)$(mandirsu)/visudo.$(mansectsu) \
		$(DESTDIR)$(mandirform)/sudo.conf.$(mansectform) \
		$(DESTDIR)$(mandirform)/sudoers.$(mansectform) \
		$(DESTDIR)$(mandirform)/sudoers_timestamp.$(mansectform)
		$(DESTDIR)$(mandirform)/sudoers.ldap.$(mansectform)

splint:

cppcheck:

pvs-log-files:

pvs-studio:

check:

clean:
	-rm -f fixman.sed

mostlyclean: clean

distclean: clean
	-rm -rf Makefile config.log *.man *.mdoc

clobber: distclean

realclean: distclean

cleandir: distclean
