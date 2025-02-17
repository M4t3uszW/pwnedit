#
# SPDX-License-Identifier: ISC
#
# Copyright (c) 2010-2018 Todd C. Miller <Todd.Miller@sudo.ws>
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
# plugins/group_file/Makefile.  Generated from Makefile.in by configure.
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
LT_LIBS = $(top_builddir)/lib/util/libsudo_util.la
LIBS = $(LT_LIBS)

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
shlib_exp = $(srcdir)/group_file.exp
shlib_map = group_file.map
shlib_opt = group_file.opt

# User and group ids the installed files should be "owned" by
install_uid = 0
install_gid = 0

#### End of system configuration section. ####

SHELL = /bin/bash

OBJS =	group_file.lo getgrent.lo

IOBJS = $(OBJS:.lo=.i)

POBJS = $(IOBJS:.i=.plog)

LIBOBJDIR = $(top_builddir)/@ac_config_libobj_dir@/

VERSION = 1.8.31p2

all: group_file.la

depend:
	$(top_srcdir)/mkdep.pl --srcdir=$(top_srcdir) \
	    --builddir=`pwd`/$(top_builddir) plugins/group_file/Makefile.in
	cd $(top_builddir) && ./config.status --file plugins/group_file/Makefile

Makefile: $(srcdir)/Makefile.in
	cd $(top_builddir) && ./config.status --file plugins/group_file/Makefile

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

group_file.la: $(OBJS) $(LT_LIBS) 
	$(LIBTOOL) $(LTFLAGS) --mode=link $(CC) $(LDFLAGS) $(ASAN_LDFLAGS) $(SSP_LDFLAGS) $(LT_LDFLAGS) -o $@ $(OBJS) $(LIBS) -module -avoid-version -rpath $(plugindir) -shrext .so

pre-install:

install: install-plugin

install-dirs:
	$(SHELL) $(top_srcdir)/mkinstalldirs $(DESTDIR)$(plugindir)

install-binaries:

install-includes:

install-doc:

install-plugin: install-dirs group_file.la
	if [ X"$(shlib_enable)" = X"yes" ]; then \
	    INSTALL_BACKUP='$(INSTALL_BACKUP)' $(LIBTOOL) $(LTFLAGS) --mode=install $(INSTALL) $(INSTALL_OWNER) -m $(shlib_mode) group_file.la $(DESTDIR)$(plugindir); \
	fi

uninstall:
	-$(LIBTOOL) $(LTFLAGS) --mode=uninstall rm -f $(DESTDIR)$(plugindir)/group_file.la
	-test -z "$(INSTALL_BACKUP)" || \
	    rm -f $(DESTDIR)$(plugindir)/group_file.so$(INSTALL_BACKUP)

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
getgrent.lo: $(srcdir)/getgrent.c $(incdir)/compat/stdbool.h \
             $(incdir)/sudo_compat.h $(incdir)/sudo_util.h \
             $(top_builddir)/config.h
	$(LIBTOOL) $(LTFLAGS) --mode=compile $(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/getgrent.c
getgrent.i: $(srcdir)/getgrent.c $(incdir)/compat/stdbool.h \
             $(incdir)/sudo_compat.h $(incdir)/sudo_util.h \
             $(top_builddir)/config.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
getgrent.plog: getgrent.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/getgrent.c --i-file $< --output-file $@
group_file.lo: $(srcdir)/group_file.c $(incdir)/compat/stdbool.h \
               $(incdir)/sudo_compat.h $(incdir)/sudo_plugin.h \
               $(top_builddir)/config.h
	$(LIBTOOL) $(LTFLAGS) --mode=compile $(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/group_file.c
group_file.i: $(srcdir)/group_file.c $(incdir)/compat/stdbool.h \
               $(incdir)/sudo_compat.h $(incdir)/sudo_plugin.h \
               $(top_builddir)/config.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
group_file.plog: group_file.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/group_file.c --i-file $< --output-file $@
