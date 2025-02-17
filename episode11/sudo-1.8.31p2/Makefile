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

srcdir = .
devdir = $(srcdir)
top_builddir = .
top_srcdir = .

# Installation paths for package building
prefix = /usr/local
exec_prefix = $(prefix)
bindir = $(exec_prefix)/bin
sbindir = $(exec_prefix)/sbin
sysconfdir = /etc
libexecdir = $(exec_prefix)/libexec
includedir = $(prefix)/include
datarootdir = $(prefix)/share
localedir = $(datarootdir)/locale
localstatedir = $(prefix)/var
exampledir = $(docdir)/examples
docdir = $(datarootdir)/doc/$(PACKAGE_TARNAME)
mandir = $(prefix)/man
rundir = /run/sudo
vardir = /var/lib/sudo

# User and group ids the installed files should be "owned" by
install_uid = 0
install_gid = 0

# sudoers owner and mode for package building
sudoersdir = $(sysconfdir)
sudoers_uid = 0
sudoers_gid = 0
sudoers_mode = 0440
shlib_mode = 0644

SUBDIRS = lib/util  plugins/group_file plugins/sudoers \
	  plugins/system_group src include doc examples

SAMPLES = plugins/sample

VERSION = 1.8.31p2
PACKAGE_TARNAME = sudo

LIBTOOL_DEPS = ./ltmain.sh

SHELL = /bin/bash

SED = /usr/bin/sed

INSTALL = $(SHELL) $(top_srcdir)/install-sh -c
INSTALL_OWNER = -o $(install_uid) -g $(install_gid)

ECHO_N = -n
ECHO_C = 

# Message catalog support
NLS = enabled
POTFILES = po/sudo.pot plugins/sudoers/po/sudoers.pot
LOCALEDIR_SUFFIX = 
MSGFMT = msgfmt
MSGMERGE = msgmerge
XGETTEXT = xgettext
XGETTEXT_OPTS = -F -k_ -kN_ -kU_ --copyright-holder="Todd C. Miller" \
		"--msgid-bugs-address=https://bugzilla.sudo.ws" \
		--package-name=sudo --package-version=$(VERSION) \
		--flag warning:1:c-format --flag warningx:1:c-format \
		--flag fatal:1:c-format --flag fatalx:1:c-format \
		--flag easprintf:3:c-format --flag sudo_lbuf_append:2:c-format \
		--flag sudo_lbuf_append_quoted:3:c-format --foreign-user

# Default cppcheck options when run from the top-level Makefile
CPPCHECK_OPTS = -q --force --enable=warning,performance,portability --suppress=constStatement --error-exitcode=1 --inline-suppr -Dva_copy=va_copy -U__cplusplus -UQUAD_MAX -UQUAD_MIN -UUQUAD_MAX -U_POSIX_HOST_NAME_MAX -U_POSIX_PATH_MAX -U__NBBY -DNSIG=64

# Default splint options when run from the top-level Makefile
SPLINT_OPTS = -D__restrict= -checks

# Default PVS-studio options when run from the top-level Makefile
PVS_CFG = $(top_builddir)/PVS-Studio.cfg
PVS_IGNORE = 'V707,V011,V002,V536'
PVS_LOG_OPTS = -a 'GA:1,2' -e -t errorfile -d $(PVS_IGNORE)

all: config.status
	for d in $(SUBDIRS); do \
	    (cd $$d && exec $(MAKE) $@) && continue; \
	    exit $$?; \
	done

check pre-install: config.status
	for d in $(SUBDIRS); do \
	    (cd $$d && exec $(MAKE) $@) && continue; \
	    exit $$?; \
	done

cppcheck: config.status
	rval=0; \
	for d in $(SUBDIRS); do \
	    echo checking $$d; \
	    (cd $$d && exec $(MAKE) CPPCHECK_OPTS="$(CPPCHECK_OPTS)" $@) || rval=`expr $$rval + $$?`; \
	done; \
	exit $$rval

splint: config.status
	rval=0; \
	for d in $(SUBDIRS); do \
	    echo splinting $$d; \
	    (cd $$d && exec $(MAKE) SPLINT_OPTS="$(SPLINT_OPTS)" $@) || rval=`expr $$rval + $$?`; \
	done; \
	exit $$rval

cov-build:
	make clean
	cov-build --dir cov-int make ${MFLAGS} all

cov-upload:
	tar zcf cov-int.tgz cov-int
	curl --form token=$$COVERITY_SUDO_TOKEN \
	    --form email=todd.miller@sudo.ws \
	    --form file=@cov-int.tgz \
	    --form version="$(VERSION)" \
	    https://scan.coverity.com/builds?project=sudo

cov-analyze: cov-upload

pvs-studio: config.status
	files=; \
	rval=0; \
	for d in $(SUBDIRS); do \
	    (cd $$d && exec $(MAKE) PVS_IGNORE="$(PVS_IGNORE)" pvs-log-files) || rval=`expr $$rval + $$?`; \
	    for f in $$d/*.plog; do \
		if test "$$f" != "$$d/*.plog"; then \
		    files="$$files $$f"; \
		fi; \
	    done; \
	done; \
	if test $$rval -ne 0; then \
	    exit $$rval; \
	fi; \
	plog-converter $(PVS_LOG_OPTS) $$files

install-dirs install-binaries install-includes install-plugin: config.status pre-install
	for d in $(SUBDIRS); do \
	    (cd $$d && exec $(MAKE) "INSTALL_OWNER=$(INSTALL_OWNER)" $@) && continue; \
	    exit $$?; \
	done

install-doc: config.status ChangeLog
	for d in $(SUBDIRS); do \
	    (cd $$d && exec $(MAKE) "INSTALL_OWNER=$(INSTALL_OWNER)" $@) && continue; \
	    exit $$?; \
	done

install: config.status ChangeLog pre-install install-nls
	for d in $(SUBDIRS); do \
	    (cd $$d && exec $(MAKE) "INSTALL_OWNER=$(INSTALL_OWNER)" $@) && continue; \
	    exit $$?; \
	done

uninstall: uninstall-nls
	for d in $(SUBDIRS); do \
	    (cd $$d && exec $(MAKE) $@) && continue; \
	    exit $$?; \
	done

uninstall-nls:
	for pot in $(POTFILES); do \
	    domain=`basename $$pot .pot`; \
	    rm -f $(DESTDIR)$(localedir)/*/LC_MESSAGES/$$domain.mo; \
	done

siglist.c signame.c:
	cd lib/util && exec $(MAKE) $@

depend: siglist.c signame.c
	$(top_srcdir)/mkdep.pl --builddir=`pwd` --srcdir=$(top_srcdir) \
	    lib/util/Makefile.in lib/zlib/Makefile.in \
	    plugins/group_file/Makefile.in plugins/sample/Makefile.in \
	    plugins/sudoers/Makefile.in plugins/system_group/Makefile.in \
	    src/Makefile.in && \
	$(top_builddir)/config.status --file $(top_builddir)/lib/util/Makefile \
	    --file $(top_builddir)/plugins/sample/Makefile \
	    --file $(top_builddir)/plugins/group_file/Makefile \
	    --file $(top_builddir)/plugins/sudoers/Makefile \
	    --file $(top_builddir)/plugins/system_group/Makefile \
	    --file $(top_builddir)/src/Makefile \
	    --file $(top_builddir)/lib/zlib/Makefile

ChangeLog:
	if test -d $(srcdir)/.hg && cd $(srcdir); then \
	    if hg log --style=changelog -r "sort(branch(.) or follow(), -date)" > $@.tmp; then \
		mv -f $@.tmp $@; \
	    else \
		rm -f $@.tmp; \
	    fi; \
	elif test -d $(srcdir)/.git && cd $(srcdir); then \
	    $(top_srcdir)/log2cl.pl -b master > $@; \
	else \
	    echo "ChangeLog data not available" > $@; \
	fi

config.status:
	@if [ ! -s config.status ]; then \
		echo "Please run configure first"; \
		exit 1; \
	fi

libtool: $(LIBTOOL_DEPS)
	$(SHELL) ./config.status --recheck

Makefile: $(srcdir)/Makefile.in
	./config.status --file Makefile

sync-po: rsync-po compile-po

rsync-po:
	rsync -Lrtvz  translationproject.org::tp/latest/sudo/ po/
	rsync -Lrtvz  translationproject.org::tp/latest/sudoers/ plugins/sudoers/po/

update-pot:
	@if $(XGETTEXT) --help >/dev/null 2>&1; then \
	    cd $(top_srcdir); \
	    for pot in $(POTFILES); do \
		echo "Updating $$pot"; \
		domain=`basename $$pot .pot`; \
		case "$$domain" in \
		    sudo) tmpfiles=; cfiles="src/*c lib/*/*c";; \
		    sudoers) \
			echo "gettext \"syntax error\"" > confstr.sh; \
			$(SED) -n 's/^.*--with-passprompt=\(.*\)$$/gettext \"\1\"/p' mkpkg | sort -u >> confstr.sh; \
			$(SED) -n -e 's/^badpass_message="/gettext "/p' \
			    -e 's/^passprompt="/gettext "/p' \
			    -e 's/^mailsub="/gettext "/p' configure.ac \
			    >> confstr.sh; \
			tmpfiles=confstr.sh; \
			cfiles="plugins/sudoers/*.c plugins/sudoers/auth/*.c";; \
		    *) echo unknown domain $$domain; continue;; \
		esac; \
		$(XGETTEXT) $(XGETTEXT_OPTS) -d$$domain $$cfiles $$tmpfiles -o $$pot.tmp; \
		test -n "$$tmpfiles" && rm -f $$tmpfiles; \
		if diff -I'^.POT-Creation-Date' -I'^.Project-Id-Version' -I'^#' $$pot.tmp $$pot >/dev/null; then \
		    rm -f $$pot.tmp; \
		else \
		    printf '/^#$$/+1,$$d\nw\nq\n' | ed - $$pot; \
		    $(SED) '1,/^#$$/d' $$pot.tmp >> $$pot; \
		    rm -f $$pot.tmp; \
		fi; \
	    done; \
	else \
	    echo "Unable to update .pot files: $(XGETTEXT) not found" 1>&2; \
	fi

update-po: update-pot
	@if $(MSGFMT) --help >/dev/null 2>&1; then \
	    cd $(top_srcdir); \
	    for pot in $(POTFILES); do \
		podir=`dirname $$pot`; \
		for po in $$podir/*.po; do \
		    echo $(ECHO_N) "Updating $$po$(ECHO_C)"; \
		    $(MSGMERGE) --update $$po $$pot; \
		    $(MSGFMT) --output /dev/null --check-format $$po || exit 1; \
		done; \
	    done; \
	else \
	    echo "Unable to update .po files: $(MSGFMT) not found" 1>&2; \
	fi

compile-po:
	@if $(MSGFMT) --help >/dev/null 2>&1; then \
	    cd $(top_srcdir); \
	    rm -f Makefile.$$$$; \
	    POFILES=""; \
	    for pot in $(POTFILES); do \
		podir=`dirname $$pot`; \
		for po in $$podir/*.po; do \
		    POFILES="$$POFILES $$po"; \
		done; \
	    done; \
	    echo "all: `echo $$POFILES | $(SED) 's/\.po/.mo/g'`" >> Makefile.$$$$; \
	    echo "" >> Makefile.$$$$; \
	    for po in $$POFILES; do \
		mo=`echo $$po | $(SED) 's/po$$/mo/'`; \
		echo "$$mo: $$po" >> Makefile.$$$$; \
		echo "	$(MSGFMT) --statistics -c -o $$mo $$po" >> Makefile.$$$$; \
	    done; \
	    $(MAKE) -f Makefile.$$$$; \
	    rm -f Makefile.$$$$; \
	else \
	    echo "Unable to compile message catalogs: $(MSGFMT) not found" 1>&2; \
	fi

install-nls:
	@if test "$(NLS)" = "enabled"; then \
	    for pot in $(POTFILES); do \
		podir=`dirname $(top_srcdir)/$$pot`; \
		domain=`basename $$pot .pot`; \
		SUDO_LINGUAS=$${LINGUAS-"`echo $$podir/*.mo | $(SED) 's:'$$podir'/\([^ ]*\).mo:\1:g'`"}; \
		echo $(ECHO_N) "Installing $$domain message catalogs:$(ECHO_C)"; \
		for lang in $$SUDO_LINGUAS; do \
		    test -s $$podir/$$lang.mo || continue; \
		    echo $(ECHO_N) " $$lang$(ECHO_C)"; \
		    $(SHELL) $(top_srcdir)/mkinstalldirs $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES; \
		    if test -n "$(LOCALEDIR_SUFFIX)"; then \
			if test ! -d $(DESTDIR)$(localedir)/$$lang$(LOCALEDIR_SUFFIX); then \
			    ln -s $$lang $(DESTDIR)$(localedir)/$$lang$(LOCALEDIR_SUFFIX); \
			fi; \
		    fi; \
		    $(INSTALL) $(INSTALL_OWNER) -m 0644 $$podir/$$lang.mo $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES/$$domain.mo; \
		done; \
		echo ""; \
	    done; \
	fi

check-dist: update-pot compile-po
	@if test -d $(srcdir)/.hg && cd $(srcdir); then \
	    if test `hg stat -am | wc -l` -ne 0; then \
		echo "Uncommitted changes" 1>&2; \
		hg stat -am 1>&2; \
		exit 1; \
	    fi; \
	fi

dist: check-dist force-dist

force-dist: ChangeLog $(srcdir)/MANIFEST
	cd $(top_srcdir) && \
	pax -w -x ustar -s '/^/$(PACKAGE_TARNAME)-$(VERSION)\//' \
	    -f ../$(PACKAGE_TARNAME)-$(VERSION).tar \
	    `$(SED) 's/[ 	].*//' $(srcdir)/MANIFEST` && \
	gzip -9f ../$(PACKAGE_TARNAME)-$(VERSION).tar && \
	ls -l ../$(PACKAGE_TARNAME)-$(VERSION).tar.gz

package: $(srcdir)/sudo.pp
	DESTDIR=`cd $(top_builddir) && pwd`/destdir; rm -rf $$DESTDIR; \
	$(MAKE) install INSTALL_OWNER= DESTDIR=$$DESTDIR && \
	$(SHELL) $(srcdir)/pp $(PPFLAGS) \
	    --destdir=$$DESTDIR \
	    $(srcdir)/sudo.pp \
	    prefix=$(prefix) \
	    bindir=$(bindir) \
	    sbindir=$(sbindir) \
	    libexecdir=$(libexecdir) \
	    includedir=$(includedir) \
	    vardir=$(vardir) \
	    rundir=$(rundir) \
	    mandir=$(mandir) \
	    localedir=$(localedir) \
	    docdir=$(docdir) \
	    exampledir=$(exampledir) \
	    sysconfdir=$(sysconfdir) \
	    sudoersdir=$(sudoersdir) \
	    sudoers_uid=$(sudoers_uid) \
	    sudoers_gid=$(sudoers_gid) \
	    sudoers_mode=$(sudoers_mode) \
	    shlib_mode=$(shlib_mode) \
	    version=$(VERSION) $(PPVARS)

clean: config.status
	for d in $(SUBDIRS) $(SAMPLES); do \
	    (cd $$d && exec $(MAKE) $@); \
	done
	-rm -rf cov-int cov-int.tgz

mostlyclean: clean

distclean: config.status
	for d in $(SUBDIRS) $(SAMPLES); do \
	    (cd $$d && exec $(MAKE) $@); \
	done
	-rm -rf autom4te.cache config.cache config.h config.log config.status \
	    init.d/*.sh init.d/sudo.conf libtool Makefile pathnames.h stamp-*

cleandir: distclean

clobber: distclean

realclean: distclean

me:

a:

sandwich:
	@if test -n "$$SUDO_USER"; then \
	    echo "Okay."; \
	else \
	    echo "What?  Make it yourself!"; \
	fi

.PHONY: ChangeLog me a sandwhich
