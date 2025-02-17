#
# SPDX-License-Identifier: ISC
#
# Copyright (c) 2011-2018 Todd C. Miller <Todd.Miller@sudo.ws>
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
# plugins/sample/Makefile.  Generated from Makefile.in by configure.
#

#### Start of system configuration section. ####

srcdir = .
devdir = $(srcdir)
top_builddir = ../..
top_srcdir = ../..
incdir = $(top_srcdir)/include
cross_compiling = no

# Compiler & tools to use
CC = gcc
LIBTOOL = $(SHELL) $(top_builddir)/libtool
SED = /usr/bin/sed
AWK = mawk

# Our install program supports extra flags...
INSTALL = $(SHELL) $(top_srcdir)/install-sh -c
INSTALL_OWNER = -o $(install_uid) -g $(install_gid)
INSTALL_BACKUP = 

# Libraries
LIBS = $(top_builddir)/lib/util/libsudo_util.la

# C preprocessor flags
CPPFLAGS = -I$(incdir) -I$(top_builddir) -I$(top_srcdir) -DZLIB_CONST -D_FORTIFY_SOURCE=2

# Usually -O and/or -g
CFLAGS = -g -O2 -fvisibility=hidden

# Flags to pass to the link stage
LDFLAGS =  -Wl,-z,relro
LT_LDFLAGS =  

# Flags to pass to libtool
LTFLAGS = --tag=disable-static

# Address sanitizer flags
ASAN_CFLAGS = 
ASAN_LDFLAGS = 

# PIE flags
PIE_CFLAGS = -fPIE
PIE_LDFLAGS = -Wc,-fPIE -pie

# Stack smashing protection flags
SSP_CFLAGS = -fstack-protector-strong
SSP_LDFLAGS = -Wc,-fstack-protector-strong

# cppcheck options, usually set in the top-level Makefile
CPPCHECK_OPTS = -q --force --enable=warning,performance,portability --suppress=constStatement --error-exitcode=1 --inline-suppr -Dva_copy=va_copy -U__cplusplus -UQUAD_MAX -UQUAD_MIN -UUQUAD_MAX -U_POSIX_HOST_NAME_MAX -U_POSIX_PATH_MAX -U__NBBY -DNSIG=64

# splint options, usually set in the top-level Makefile
SPLINT_OPTS = -D__restrict= -checks

# PVS-studio options
PVS_CFG = $(top_srcdir)/PVS-Studio.cfg
PVS_IGNORE = 'V707,V011,V002,V536'
PVS_LOG_OPTS = -a 'GA:1,2' -e -t errorfile -d $(PVS_IGNORE)

# Where to install things...
prefix = /usr/local
exec_prefix = $(prefix)
bindir = $(exec_prefix)/bin
sbindir = $(exec_prefix)/sbin
sysconfdir = /etc
libexecdir = $(exec_prefix)/libexec
datarootdir = $(prefix)/share
localstatedir = $(prefix)/var
plugindir = /usr/local/libexec/sudo

# File mode and map file to use for shared libraries/objects
shlib_enable = yes
shlib_mode = 0644
shlib_exp = $(srcdir)/sample_plugin.exp
shlib_map = sample_plugin.map
shlib_opt = sample_plugin.opt

# User and group ids the installed files should be "owned" by
install_uid = 0
install_gid = 0

#### End of system configuration section. ####

SHELL = /bin/bash

OBJS =	sample_plugin.lo

LIBOBJDIR = $(top_builddir)/@ac_config_libobj_dir@/

VERSION = 1.8.31p2

all: sample_plugin.la

depend:
	$(top_srcdir)/mkdep.pl --srcdir=$(top_srcdir) \
	    --builddir=`pwd`/$(top_builddir) plugins/sample/Makefile.in
	cd $(top_builddir) && ./config.status --file plugins/sample/Makefile

Makefile: $(srcdir)/Makefile.in
	cd $(top_builddir) && ./config.status --file plugins/sample/Makefile

.SUFFIXES: .c .h .i .lo .plog

.c.lo:
	$(LIBTOOL) $(LTFLAGS) --mode=compile $(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $<

.c.i:
	$(CC) -E -o $@ $(CPPFLAGS) $<

.i.plog:
	ifile=$<; rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $${ifile%i}c --i-file $< --output-file $@

$(shlib_map): $(shlib_exp)
	@$(AWK) 'BEGIN { print "{\n\tglobal:" } { print "\t\t"$$0";" } END { print "\tlocal:\n\t\t*;\n};" }' $(shlib_exp) > $@

$(shlib_opt): $(shlib_exp)
	@$(SED) 's/^/+e /' $(shlib_exp) > $@

sample_plugin.la: $(OBJS) 
	$(LIBTOOL) $(LTFLAGS) --mode=link $(CC) $(LDFLAGS) $(ASAN_LDFLAGS) $(SSP_LDFLAGS) $(LT_LDFLAGS) -o $@ $(OBJS) $(LIBS) -module -avoid-version -rpath $(plugindir) -shrext .so

pre-install:

install: install-plugin

install-dirs:
	$(SHELL) $(top_srcdir)/mkinstalldirs $(DESTDIR)$(plugindir)

install-binaries:

install-includes:

install-doc:

install-plugin: install-dirs sample_plugin.la
	if [ X"$(shlib_enable)" = X"yes" ]; then \
	    INSTALL_BACKUP='$(INSTALL_BACKUP)' $(LIBTOOL) $(LTFLAGS) --mode=install $(INSTALL) $(INSTALL_OWNER) -m $(shlib_mode) sample_plugin.la $(DESTDIR)$(plugindir); \
	fi

uninstall:
	-$(LIBTOOL) $(LTFLAGS) --mode=uninstall rm -f $(DESTDIR)$(plugindir)/sample_plugin.la
	-test -z "$(INSTALL_BACKUP)" || \
	    rm -f $(DESTDIR)$(plugindir)/sample_plugin.so$(INSTALL_BACKUP)

splint:
	splint $(SPLINT_OPTS) -I$(incdir) -I$(top_builddir) -I$(top_srcdir) $(srcdir)/*.c

cppcheck:
	cppcheck $(CPPCHECK_OPTS) -I$(incdir) -I$(top_builddir) -I$(top_srcdir) $(srcdir)/*.c

pvs-log-files: $(POBJS)

pvs-studio: $(POBJS)
	plog-converter $(PVS_LOG_OPTS) $(POBJS)

check:

clean:
	-$(LIBTOOL) $(LTFLAGS) --mode=clean rm -f *.lo *.o *.la *.a *.i *.plog \
	    stamp-* core *.core core.*

mostlyclean: clean

distclean: clean
	-rm -rf Makefile .libs $(shlib_map) $(shlib_opt)

clobber: distclean

realclean: distclean
	rm -f TAGS tags

cleandir: realclean

# Autogenerated dependencies, do not modify
sample_plugin.lo: $(srcdir)/sample_plugin.c $(incdir)/compat/stdbool.h \
                  $(incdir)/sudo_compat.h $(incdir)/sudo_plugin.h \
                  $(incdir)/sudo_util.h $(top_builddir)/config.h \
                  $(top_builddir)/pathnames.h
	$(LIBTOOL) $(LTFLAGS) --mode=compile $(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/sample_plugin.c
sample_plugin.i: $(srcdir)/sample_plugin.c $(incdir)/compat/stdbool.h \
                  $(incdir)/sudo_compat.h $(incdir)/sudo_plugin.h \
                  $(incdir)/sudo_util.h $(top_builddir)/config.h \
                  $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
sample_plugin.plog: sample_plugin.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/sample_plugin.c --i-file $< --output-file $@
