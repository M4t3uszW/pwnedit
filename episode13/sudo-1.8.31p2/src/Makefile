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
# src/Makefile.  Generated from Makefile.in by configure.
#

#### Start of system configuration section. ####

srcdir = .
devdir = $(srcdir)
top_builddir = ..
top_srcdir = ..
incdir = $(top_srcdir)/include
rundir = /run/sudo
cross_compiling = no

# Compiler & tools to use
CC = gcc
LIBTOOL = $(SHELL) $(top_builddir)/libtool
SED = /usr/bin/sed

# Our install program supports extra flags...
INSTALL = $(SHELL) $(top_srcdir)/install-sh -c
INSTALL_OWNER = -o $(install_uid) -g $(install_gid)
INSTALL_BACKUP = 

# Libraries
LT_LIBS = $(top_builddir)/lib/util/libsudo_util.la
LIBS =   -lutil   $(LT_LIBS)

# C preprocessor defines
CPPDEFS = -D_PATH_SUDO_CONF=\"$(sysconfdir)/sudo.conf\" \
	  -DLOCALEDIR=\"$(localedir)\"

# C preprocessor flags
CPPFLAGS = -I$(incdir) -I$(top_builddir) -I. -I$(srcdir) -I$(top_srcdir) \
	   $(CPPDEFS) -DZLIB_CONST -D_FORTIFY_SOURCE=2

# Usually -O and/or -g
CFLAGS = -g -O2 -fvisibility=hidden

# Flags to pass to the link stage
LDFLAGS =  -Wl,-z,relro
SUDO_LDFLAGS = $(LDFLAGS) 
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
localedir = $(datarootdir)/locale
localstatedir = $(prefix)/var
noexecfile = sudo_noexec.so
noexecdir = $(exec_prefix)/libexec/sudo
tmpfiles_d = 

# User and group ids the installed files should be "owned" by
install_uid = 0
install_gid = 0

# File mode to use for shared libraries
shlib_mode = 0644

# Optional init script and rc.d link
INIT_DIR=
INIT_SCRIPT=
RC_LINK=

TEST_PROGS = check_ttyname check_noexec
TEST_LIBS =  $(LT_LIBS)
TEST_LDFLAGS =  -Wl,-z,relro

#### End of system configuration section. ####

SHELL = /bin/bash

PROGS = sudo sudo_noexec.la

OBJS = conversation.o env_hooks.o exec.o exec_common.o exec_monitor.o \
       exec_nopty.o exec_pty.o get_pty.o hooks.o limits.o load_plugins.o \
       net_ifs.o parse_args.o preserve_fds.o signal.o sudo.o sudo_edit.o \
       tcsetpgrp_nobg.o tgetpass.o ttyname.o utmp.o 

IOBJS = $(OBJS:.o=.i) sesh.i

POBJS = $(IOBJS:.i=.plog)

SESH_OBJS = sesh.o exec_common.o

CHECK_NOEXEC_OBJS = check_noexec.o exec_common.o

CHECK_TTYNAME_OBJS = check_ttyname.o ttyname.o

LIBOBJDIR = $(top_builddir)/@ac_config_libobj_dir@/

VERSION = 1.8.31p2

all: $(PROGS)

depend:
	$(top_srcdir)/mkdep.pl --srcdir=$(top_srcdir) \
	    --builddir=`pwd`/$(top_builddir) src/Makefile.in
	cd $(top_builddir) && ./config.status --file src/Makefile

Makefile: $(srcdir)/Makefile.in
	cd $(top_builddir) && ./config.status --file src/Makefile

./sudo_usage.h: $(srcdir)/sudo_usage.h.in
	cd $(top_builddir) && ./config.status --file src/sudo_usage.h

.SUFFIXES: .c .h .i .lo .o .plog

.c.o:
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $<

.c.lo:
	$(LIBTOOL) $(LTFLAGS) --mode=compile $(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $<

.c.i:
	$(CC) -E -o $@ $(CPPFLAGS) $<

.i.plog:
	ifile=$<; rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $${ifile%i}c --i-file $< --output-file $@

sudo: $(OBJS) $(LT_LIBS) 
	$(LIBTOOL) $(LTFLAGS) --mode=link $(CC) -o $@ $(OBJS) $(SUDO_LDFLAGS) $(ASAN_LDFLAGS) $(PIE_LDFLAGS) $(SSP_LDFLAGS) $(LIBS) 

# We can't use -module here since you cannot preload a module on Darwin
libsudo_noexec.la: sudo_noexec.lo
	$(LIBTOOL) $(LTFLAGS) --mode=link $(CC) $(LDFLAGS) $(LT_LDFLAGS) $(SSP_LDFLAGS) -ldl -o $@ sudo_noexec.lo -avoid-version -rpath $(noexecdir) -shrext .so

# Some hackery is required to install this as sudo_noexec, not libsudo_noexec
sudo_noexec.la: libsudo_noexec.la
	sed 's/libsudo_noexec/sudo_noexec/g' libsudo_noexec.la > sudo_noexec.la
	if test -f .libs/libsudo_noexec.lai; then sed 's/libsudo_noexec/sudo_noexec/g' .libs/libsudo_noexec.lai > .libs/sudo_noexec.lai; fi
	cp -p .libs/libsudo_noexec.so .libs/sudo_noexec.so

sesh: $(SESH_OBJS) $(LT_LIBS)
	$(LIBTOOL) $(LTFLAGS) --mode=link $(CC) -o $@ $(SESH_OBJS) $(LDFLAGS) $(ASAN_LDFLAGS) $(PIE_LDFLAGS) $(SSP_LDFLAGS) $(LIBS)

check_noexec: $(CHECK_NOEXEC_OBJS) $(top_builddir)/lib/util/libsudo_util.la sudo_noexec.la
	$(LIBTOOL) $(LTFLAGS) --mode=link $(CC) -o $@ $(CHECK_NOEXEC_OBJS) $(TEST_LDFLAGS) $(ASAN_LDFLAGS) $(PIE_LDFLAGS) $(SSP_LDFLAGS) $(TEST_LIBS)

check_ttyname: $(CHECK_TTYNAME_OBJS) $(top_builddir)/lib/util/libsudo_util.la
	$(LIBTOOL) $(LTFLAGS) --mode=link $(CC) -o $@ $(CHECK_TTYNAME_OBJS) $(TEST_LDFLAGS) $(ASAN_LDFLAGS) $(PIE_LDFLAGS) $(SSP_LDFLAGS) $(TEST_LIBS)

pre-install:

install: install-binaries install-rc install-noexec

install-dirs:
	# We only create the rc.d dir when installing to the actual system dir
	$(SHELL) $(top_srcdir)/mkinstalldirs $(DESTDIR)$(bindir) \
	    $(DESTDIR)$(libexecdir)/sudo $(DESTDIR)$(noexecdir)
	if test -n "$(INIT_SCRIPT)"; then \
	    $(SHELL) $(top_srcdir)/mkinstalldirs $(DESTDIR)$(INIT_DIR); \
	    if test -z "$(DESTDIR)"; then \
		$(SHELL) $(top_srcdir)/mkinstalldirs \
		    `echo $(RC_LINK) | $(SED) 's,/[^/]*$$,,'`; \
	    fi; \
	elif test -n "$(tmpfiles_d)"; then \
	    $(SHELL) $(top_srcdir)/mkinstalldirs $(DESTDIR)$(tmpfiles_d); \
	fi

install-rc: install-dirs
	# We only create the rc.d link when installing to the actual system dir
	if [ -n "$(INIT_SCRIPT)" ]; then \
	    $(INSTALL) $(INSTALL_OWNER) -m 0755 $(top_builddir)/init.d/$(INIT_SCRIPT) $(DESTDIR)$(INIT_DIR)/sudo; \
	    if test -z "$(DESTDIR)"; then \
		rm -f $(RC_LINK); \
		ln -s $(INIT_DIR)/sudo $(RC_LINK); \
	    fi; \
	elif test -n "$(tmpfiles_d)"; then \
	    $(INSTALL) $(INSTALL_OWNER) -m 0644 $(top_builddir)/init.d/sudo.conf $(DESTDIR)$(tmpfiles_d)/sudo.conf; \
	fi

install-binaries: install-dirs $(PROGS)
	INSTALL_BACKUP='$(INSTALL_BACKUP)' $(LIBTOOL) $(LTFLAGS) --mode=install $(INSTALL) $(INSTALL_OWNER) -m 04755 sudo $(DESTDIR)$(bindir)/sudo
	rm -f $(DESTDIR)$(bindir)/sudoedit
	ln -s sudo $(DESTDIR)$(bindir)/sudoedit
	if [ -f sesh ]; then \
	    INSTALL_BACKUP='$(INSTALL_BACKUP)' $(LIBTOOL) $(LTFLAGS) --mode=install $(INSTALL) $(INSTALL_OWNER) -m 0755 sesh $(DESTDIR)$(libexecdir)/sudo/sesh; \
	fi

install-doc:

install-includes:

install-noexec: install-dirs sudo_noexec.la
	INSTALL_BACKUP='$(INSTALL_BACKUP)' $(LIBTOOL) $(LTFLAGS) --mode=install $(INSTALL) $(INSTALL_OWNER) -m $(shlib_mode) sudo_noexec.la $(DESTDIR)$(noexecdir)

install-plugin:

uninstall:
	-$(LIBTOOL) $(LTFLAGS) --mode=uninstall rm -f $(DESTDIR)$(noexecdir)/sudo_noexec.la
	-rm -f	$(DESTDIR)$(bindir)/sudo \
		$(DESTDIR)$(bindir)/sudoedit \
		$(DESTDIR)$(libexecdir)/sudo/sesh \
		$(DESTDIR)/usr/lib/tmpfiles.d/sudo.conf
	-test -z "$(INSTALL_BACKUP)" || \
	    rm -f $(DESTDIR)$(bindir)/sudo$(INSTALL_BACKUP) \
		  $(DESTDIR)$(libexecdir)/sudo/sesh$(INSTALL_BACKUP) \
		  $(DESTDIR)$(noexecdir)/sudo_noexec.so$(INSTALL_BACKUP)
	-test -z "$(INIT_SCRIPT)" || \
	    rm -f $(DESTDIR)$(RC_LINK) $(DESTDIR)$(INIT_DIR)/sudo

splint:
	splint $(SPLINT_OPTS) -I$(incdir) -I$(top_builddir) -I. -I$(srcdir) -I$(top_srcdir) $(srcdir)/*.c

cppcheck:
	cppcheck $(CPPCHECK_OPTS) -I$(incdir) -I$(top_builddir) -I. -I$(srcdir) -I$(top_srcdir) $(srcdir)/*.c

pvs-log-files: $(POBJS)

pvs-studio: $(POBJS)
	plog-converter $(PVS_LOG_OPTS) $(POBJS)

check: $(TEST_PROGS)
	@if test X"$(cross_compiling)" != X"yes"; then \
	    MALLOC_OPTIONS=S; export MALLOC_OPTIONS; \
	    MALLOC_CONF="abort:true,junk:true"; export MALLOC_CONF; \
	    ./check_ttyname; \
	    if test X"check_noexec" != X""; then \
		./check_noexec .libs/$(noexecfile); \
	    fi; \
	fi

clean:
	-$(LIBTOOL) $(LTFLAGS) --mode=clean rm -f $(PROGS) $(TEST_PROGS) \
	    *.lo *.o *.la *.a *.i *.plog stamp-* core *.core core.* nohup.out

mostlyclean: clean

distclean: clean
	-rm -rf Makefile .libs sudo_usage.h

clobber: distclean

realclean: distclean
	rm -f TAGS tags

cleandir: realclean

# *Not* auto-generated to avoid building with ASAN
sudo_noexec.lo: $(srcdir)/sudo_noexec.c $(incdir)/sudo_compat.h \
                $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(LIBTOOL) $(LTFLAGS) --mode=compile $(CC) -c $(CPPFLAGS) $(CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/sudo_noexec.c

# Autogenerated dependencies, do not modify
check_noexec.o: $(srcdir)/regress/noexec/check_noexec.c \
                $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
                $(incdir)/sudo_fatal.h $(incdir)/sudo_util.h \
                $(srcdir)/sudo_exec.h $(top_builddir)/config.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/regress/noexec/check_noexec.c
check_noexec.i: $(srcdir)/regress/noexec/check_noexec.c \
                $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
                $(incdir)/sudo_fatal.h $(incdir)/sudo_util.h \
                $(srcdir)/sudo_exec.h $(top_builddir)/config.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
check_noexec.plog: check_noexec.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/regress/noexec/check_noexec.c --i-file $< --output-file $@
check_ttyname.o: $(srcdir)/regress/ttyname/check_ttyname.c \
                 $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
                 $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
                 $(incdir)/sudo_queue.h $(incdir)/sudo_util.h \
                 $(top_builddir)/config.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/regress/ttyname/check_ttyname.c
check_ttyname.i: $(srcdir)/regress/ttyname/check_ttyname.c \
                 $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
                 $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
                 $(incdir)/sudo_queue.h $(incdir)/sudo_util.h \
                 $(top_builddir)/config.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
check_ttyname.plog: check_ttyname.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/regress/ttyname/check_ttyname.c --i-file $< --output-file $@
conversation.o: $(srcdir)/conversation.c $(incdir)/compat/stdbool.h \
                $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
                $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
                $(incdir)/sudo_gettext.h $(incdir)/sudo_plugin.h \
                $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo.h \
                $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
                $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/conversation.c
conversation.i: $(srcdir)/conversation.c $(incdir)/compat/stdbool.h \
                $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
                $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
                $(incdir)/sudo_gettext.h $(incdir)/sudo_plugin.h \
                $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo.h \
                $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
                $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
conversation.plog: conversation.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/conversation.c --i-file $< --output-file $@
env_hooks.o: $(srcdir)/env_hooks.c $(incdir)/compat/stdbool.h \
             $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
             $(incdir)/sudo_debug.h $(incdir)/sudo_dso.h \
             $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
             $(incdir)/sudo_plugin.h $(incdir)/sudo_queue.h \
             $(incdir)/sudo_util.h $(srcdir)/sudo.h $(top_builddir)/config.h \
             $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/env_hooks.c
env_hooks.i: $(srcdir)/env_hooks.c $(incdir)/compat/stdbool.h \
             $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
             $(incdir)/sudo_debug.h $(incdir)/sudo_dso.h \
             $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
             $(incdir)/sudo_plugin.h $(incdir)/sudo_queue.h \
             $(incdir)/sudo_util.h $(srcdir)/sudo.h $(top_builddir)/config.h \
             $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
env_hooks.plog: env_hooks.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/env_hooks.c --i-file $< --output-file $@
exec.o: $(srcdir)/exec.c $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
        $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h $(incdir)/sudo_event.h \
        $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
        $(incdir)/sudo_plugin.h $(incdir)/sudo_queue.h $(incdir)/sudo_util.h \
        $(srcdir)/sudo.h $(srcdir)/sudo_exec.h $(srcdir)/sudo_plugin_int.h \
        $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/exec.c
exec.i: $(srcdir)/exec.c $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
        $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h $(incdir)/sudo_event.h \
        $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
        $(incdir)/sudo_plugin.h $(incdir)/sudo_queue.h $(incdir)/sudo_util.h \
        $(srcdir)/sudo.h $(srcdir)/sudo_exec.h $(srcdir)/sudo_plugin_int.h \
        $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
exec.plog: exec.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/exec.c --i-file $< --output-file $@
exec_common.o: $(srcdir)/exec_common.c $(incdir)/compat/stdbool.h \
               $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
               $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
               $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
               $(incdir)/sudo_util.h $(srcdir)/sudo.h $(srcdir)/sudo_exec.h \
               $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/exec_common.c
exec_common.i: $(srcdir)/exec_common.c $(incdir)/compat/stdbool.h \
               $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
               $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
               $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
               $(incdir)/sudo_util.h $(srcdir)/sudo.h $(srcdir)/sudo_exec.h \
               $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
exec_common.plog: exec_common.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/exec_common.c --i-file $< --output-file $@
exec_monitor.o: $(srcdir)/exec_monitor.c $(incdir)/compat/stdbool.h \
                $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
                $(incdir)/sudo_debug.h $(incdir)/sudo_event.h \
                $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
                $(incdir)/sudo_plugin.h $(incdir)/sudo_queue.h \
                $(incdir)/sudo_util.h $(srcdir)/sudo.h $(srcdir)/sudo_exec.h \
                $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
                $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/exec_monitor.c
exec_monitor.i: $(srcdir)/exec_monitor.c $(incdir)/compat/stdbool.h \
                $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
                $(incdir)/sudo_debug.h $(incdir)/sudo_event.h \
                $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
                $(incdir)/sudo_plugin.h $(incdir)/sudo_queue.h \
                $(incdir)/sudo_util.h $(srcdir)/sudo.h $(srcdir)/sudo_exec.h \
                $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
                $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
exec_monitor.plog: exec_monitor.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/exec_monitor.c --i-file $< --output-file $@
exec_nopty.o: $(srcdir)/exec_nopty.c $(incdir)/compat/stdbool.h \
              $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
              $(incdir)/sudo_debug.h $(incdir)/sudo_event.h \
              $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
              $(incdir)/sudo_plugin.h $(incdir)/sudo_queue.h \
              $(incdir)/sudo_util.h $(srcdir)/sudo.h $(srcdir)/sudo_exec.h \
              $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
              $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/exec_nopty.c
exec_nopty.i: $(srcdir)/exec_nopty.c $(incdir)/compat/stdbool.h \
              $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
              $(incdir)/sudo_debug.h $(incdir)/sudo_event.h \
              $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
              $(incdir)/sudo_plugin.h $(incdir)/sudo_queue.h \
              $(incdir)/sudo_util.h $(srcdir)/sudo.h $(srcdir)/sudo_exec.h \
              $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
              $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
exec_nopty.plog: exec_nopty.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/exec_nopty.c --i-file $< --output-file $@
exec_pty.o: $(srcdir)/exec_pty.c $(incdir)/compat/stdbool.h \
            $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
            $(incdir)/sudo_debug.h $(incdir)/sudo_event.h \
            $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
            $(incdir)/sudo_plugin.h $(incdir)/sudo_queue.h \
            $(incdir)/sudo_util.h $(srcdir)/sudo.h $(srcdir)/sudo_exec.h \
            $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
            $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/exec_pty.c
exec_pty.i: $(srcdir)/exec_pty.c $(incdir)/compat/stdbool.h \
            $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
            $(incdir)/sudo_debug.h $(incdir)/sudo_event.h \
            $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
            $(incdir)/sudo_plugin.h $(incdir)/sudo_queue.h \
            $(incdir)/sudo_util.h $(srcdir)/sudo.h $(srcdir)/sudo_exec.h \
            $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
            $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
exec_pty.plog: exec_pty.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/exec_pty.c --i-file $< --output-file $@
get_pty.o: $(srcdir)/get_pty.c $(incdir)/compat/stdbool.h \
           $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
           $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
           $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
           $(incdir)/sudo_util.h $(srcdir)/sudo.h $(top_builddir)/config.h \
           $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/get_pty.c
get_pty.i: $(srcdir)/get_pty.c $(incdir)/compat/stdbool.h \
           $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
           $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
           $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
           $(incdir)/sudo_util.h $(srcdir)/sudo.h $(top_builddir)/config.h \
           $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
get_pty.plog: get_pty.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/get_pty.c --i-file $< --output-file $@
hooks.o: $(srcdir)/hooks.c $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
         $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
         $(incdir)/sudo_gettext.h $(incdir)/sudo_plugin.h \
         $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo.h \
         $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
         $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/hooks.c
hooks.i: $(srcdir)/hooks.c $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
         $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
         $(incdir)/sudo_gettext.h $(incdir)/sudo_plugin.h \
         $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo.h \
         $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
         $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
hooks.plog: hooks.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/hooks.c --i-file $< --output-file $@
limits.o: $(srcdir)/limits.c $(incdir)/compat/stdbool.h \
          $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h \
          $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
          $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo.h \
          $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/limits.c
limits.i: $(srcdir)/limits.c $(incdir)/compat/stdbool.h \
          $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h \
          $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
          $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo.h \
          $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
limits.plog: limits.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/limits.c --i-file $< --output-file $@
load_plugins.o: $(srcdir)/load_plugins.c $(incdir)/compat/stdbool.h \
                $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
                $(incdir)/sudo_debug.h $(incdir)/sudo_dso.h \
                $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
                $(incdir)/sudo_plugin.h $(incdir)/sudo_queue.h \
                $(incdir)/sudo_util.h $(srcdir)/sudo.h \
                $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
                $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/load_plugins.c
load_plugins.i: $(srcdir)/load_plugins.c $(incdir)/compat/stdbool.h \
                $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
                $(incdir)/sudo_debug.h $(incdir)/sudo_dso.h \
                $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
                $(incdir)/sudo_plugin.h $(incdir)/sudo_queue.h \
                $(incdir)/sudo_util.h $(srcdir)/sudo.h \
                $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
                $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
load_plugins.plog: load_plugins.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/load_plugins.c --i-file $< --output-file $@
net_ifs.o: $(srcdir)/net_ifs.c $(incdir)/compat/stdbool.h \
           $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
           $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
           $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
           $(top_builddir)/config.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/net_ifs.c
net_ifs.i: $(srcdir)/net_ifs.c $(incdir)/compat/stdbool.h \
           $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
           $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
           $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
           $(top_builddir)/config.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
net_ifs.plog: net_ifs.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/net_ifs.c --i-file $< --output-file $@
openbsd.o: $(srcdir)/openbsd.c $(incdir)/compat/stdbool.h \
           $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
           $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
           $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
           $(incdir)/sudo_util.h $(srcdir)/sudo.h $(top_builddir)/config.h \
           $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/openbsd.c
openbsd.i: $(srcdir)/openbsd.c $(incdir)/compat/stdbool.h \
           $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
           $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
           $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
           $(incdir)/sudo_util.h $(srcdir)/sudo.h $(top_builddir)/config.h \
           $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
openbsd.plog: openbsd.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/openbsd.c --i-file $< --output-file $@
parse_args.o: $(srcdir)/parse_args.c $(incdir)/compat/getopt.h \
              $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
              $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h \
              $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
              $(incdir)/sudo_lbuf.h $(incdir)/sudo_queue.h \
              $(incdir)/sudo_util.h $(srcdir)/sudo.h $(top_builddir)/config.h \
              $(top_builddir)/pathnames.h ./sudo_usage.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/parse_args.c
parse_args.i: $(srcdir)/parse_args.c $(incdir)/compat/getopt.h \
              $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
              $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h \
              $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
              $(incdir)/sudo_lbuf.h $(incdir)/sudo_queue.h \
              $(incdir)/sudo_util.h $(srcdir)/sudo.h $(top_builddir)/config.h \
              $(top_builddir)/pathnames.h ./sudo_usage.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
parse_args.plog: parse_args.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/parse_args.c --i-file $< --output-file $@
preload.o: $(srcdir)/preload.c $(incdir)/sudo_compat.h $(incdir)/sudo_dso.h \
           $(incdir)/sudo_plugin.h $(top_builddir)/config.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/preload.c
preload.i: $(srcdir)/preload.c $(incdir)/sudo_compat.h $(incdir)/sudo_dso.h \
           $(incdir)/sudo_plugin.h $(top_builddir)/config.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
preload.plog: preload.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/preload.c --i-file $< --output-file $@
preserve_fds.o: $(srcdir)/preserve_fds.c $(incdir)/compat/stdbool.h \
                $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
                $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
                $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
                $(incdir)/sudo_util.h $(srcdir)/sudo.h \
                $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/preserve_fds.c
preserve_fds.i: $(srcdir)/preserve_fds.c $(incdir)/compat/stdbool.h \
                $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
                $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
                $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
                $(incdir)/sudo_util.h $(srcdir)/sudo.h \
                $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
preserve_fds.plog: preserve_fds.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/preserve_fds.c --i-file $< --output-file $@
selinux.o: $(srcdir)/selinux.c $(incdir)/compat/stdbool.h \
           $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
           $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
           $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
           $(incdir)/sudo_util.h $(srcdir)/sudo.h $(srcdir)/sudo_exec.h \
           $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/selinux.c
selinux.i: $(srcdir)/selinux.c $(incdir)/compat/stdbool.h \
           $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
           $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
           $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
           $(incdir)/sudo_util.h $(srcdir)/sudo.h $(srcdir)/sudo_exec.h \
           $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
selinux.plog: selinux.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/selinux.c --i-file $< --output-file $@
sesh.o: $(srcdir)/sesh.c $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
        $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
        $(incdir)/sudo_gettext.h $(incdir)/sudo_plugin.h \
        $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo_exec.h \
        $(top_builddir)/config.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/sesh.c
sesh.i: $(srcdir)/sesh.c $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
        $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
        $(incdir)/sudo_gettext.h $(incdir)/sudo_plugin.h \
        $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo_exec.h \
        $(top_builddir)/config.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
sesh.plog: sesh.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/sesh.c --i-file $< --output-file $@
signal.o: $(srcdir)/signal.c $(incdir)/compat/stdbool.h \
          $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h \
          $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
          $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo.h \
          $(srcdir)/sudo_exec.h $(top_builddir)/config.h \
          $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/signal.c
signal.i: $(srcdir)/signal.c $(incdir)/compat/stdbool.h \
          $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h \
          $(incdir)/sudo_fatal.h $(incdir)/sudo_gettext.h \
          $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo.h \
          $(srcdir)/sudo_exec.h $(top_builddir)/config.h \
          $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
signal.plog: signal.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/signal.c --i-file $< --output-file $@
solaris.o: $(srcdir)/solaris.c $(incdir)/compat/stdbool.h \
           $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
           $(incdir)/sudo_debug.h $(incdir)/sudo_dso.h $(incdir)/sudo_fatal.h \
           $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
           $(incdir)/sudo_util.h $(srcdir)/sudo.h $(top_builddir)/config.h \
           $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/solaris.c
solaris.i: $(srcdir)/solaris.c $(incdir)/compat/stdbool.h \
           $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
           $(incdir)/sudo_debug.h $(incdir)/sudo_dso.h $(incdir)/sudo_fatal.h \
           $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
           $(incdir)/sudo_util.h $(srcdir)/sudo.h $(top_builddir)/config.h \
           $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
solaris.plog: solaris.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/solaris.c --i-file $< --output-file $@
sudo.o: $(srcdir)/sudo.c $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
        $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
        $(incdir)/sudo_gettext.h $(incdir)/sudo_plugin.h \
        $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo.h \
        $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
        $(top_builddir)/pathnames.h ./sudo_usage.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/sudo.c
sudo.i: $(srcdir)/sudo.c $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
        $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
        $(incdir)/sudo_gettext.h $(incdir)/sudo_plugin.h \
        $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo.h \
        $(srcdir)/sudo_plugin_int.h $(top_builddir)/config.h \
        $(top_builddir)/pathnames.h ./sudo_usage.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
sudo.plog: sudo.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/sudo.c --i-file $< --output-file $@
sudo_edit.o: $(srcdir)/sudo_edit.c $(incdir)/compat/stdbool.h \
             $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
             $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
             $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
             $(incdir)/sudo_util.h $(srcdir)/sudo.h $(srcdir)/sudo_exec.h \
             $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/sudo_edit.c
sudo_edit.i: $(srcdir)/sudo_edit.c $(incdir)/compat/stdbool.h \
             $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
             $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
             $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
             $(incdir)/sudo_util.h $(srcdir)/sudo.h $(srcdir)/sudo_exec.h \
             $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
sudo_edit.plog: sudo_edit.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/sudo_edit.c --i-file $< --output-file $@
tcsetpgrp_nobg.o: $(srcdir)/tcsetpgrp_nobg.c $(incdir)/compat/stdbool.h \
                  $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
                  $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
                  $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
                  $(incdir)/sudo_util.h $(srcdir)/sudo.h \
                  $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/tcsetpgrp_nobg.c
tcsetpgrp_nobg.i: $(srcdir)/tcsetpgrp_nobg.c $(incdir)/compat/stdbool.h \
                  $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
                  $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
                  $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
                  $(incdir)/sudo_util.h $(srcdir)/sudo.h \
                  $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
tcsetpgrp_nobg.plog: tcsetpgrp_nobg.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/tcsetpgrp_nobg.c --i-file $< --output-file $@
tgetpass.o: $(srcdir)/tgetpass.c $(incdir)/compat/stdbool.h \
            $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
            $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
            $(incdir)/sudo_gettext.h $(incdir)/sudo_plugin.h \
            $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo.h \
            $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/tgetpass.c
tgetpass.i: $(srcdir)/tgetpass.c $(incdir)/compat/stdbool.h \
            $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
            $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
            $(incdir)/sudo_gettext.h $(incdir)/sudo_plugin.h \
            $(incdir)/sudo_queue.h $(incdir)/sudo_util.h $(srcdir)/sudo.h \
            $(top_builddir)/config.h $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
tgetpass.plog: tgetpass.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/tgetpass.c --i-file $< --output-file $@
ttyname.o: $(srcdir)/ttyname.c $(incdir)/compat/stdbool.h \
           $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
           $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
           $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
           $(incdir)/sudo_util.h $(srcdir)/sudo.h $(top_builddir)/config.h \
           $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/ttyname.c
ttyname.i: $(srcdir)/ttyname.c $(incdir)/compat/stdbool.h \
           $(incdir)/sudo_compat.h $(incdir)/sudo_conf.h \
           $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
           $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h \
           $(incdir)/sudo_util.h $(srcdir)/sudo.h $(top_builddir)/config.h \
           $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
ttyname.plog: ttyname.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/ttyname.c --i-file $< --output-file $@
utmp.o: $(srcdir)/utmp.c $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
        $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
        $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h $(incdir)/sudo_util.h \
        $(srcdir)/sudo.h $(srcdir)/sudo_exec.h $(top_builddir)/config.h \
        $(top_builddir)/pathnames.h
	$(CC) -c $(CPPFLAGS) $(CFLAGS) $(ASAN_CFLAGS) $(PIE_CFLAGS) $(SSP_CFLAGS) $(srcdir)/utmp.c
utmp.i: $(srcdir)/utmp.c $(incdir)/compat/stdbool.h $(incdir)/sudo_compat.h \
        $(incdir)/sudo_conf.h $(incdir)/sudo_debug.h $(incdir)/sudo_fatal.h \
        $(incdir)/sudo_gettext.h $(incdir)/sudo_queue.h $(incdir)/sudo_util.h \
        $(srcdir)/sudo.h $(srcdir)/sudo_exec.h $(top_builddir)/config.h \
        $(top_builddir)/pathnames.h
	$(CC) -E -o $@ $(CPPFLAGS) $<
utmp.plog: utmp.i
	rm -f $@; pvs-studio --cfg $(PVS_CFG) --sourcetree-root $(top_srcdir) --skip-cl-exe yes --source-file $(srcdir)/utmp.c --i-file $< --output-file $@
