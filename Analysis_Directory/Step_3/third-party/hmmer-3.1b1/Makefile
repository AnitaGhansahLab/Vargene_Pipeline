# Top level Makefile for HMMER3
# 
# On most systems, to build H3 you should only need:
#     % ./configure; make
#
# Optionally, you can run a test suite:
#     % make check
#
# And optionally, you can install everything more permanently:
#     % make install
#
# For more information, see the Installation chapter of the HMMER
# User's Guide.
#


# VPATH and shell configuration
#
top_srcdir     = .
srcdir         = .

SHELL          = /bin/sh

# location of easel
ESLDIR         = easel

# location of libdivsufsort for suffix array creation
SADIR          = libdivsufsort


# Package information
#
PACKAGE         = HMMER
PACKAGE_VERSION = 3.1b1
PACKAGE_TARNAME = hmmer

# Installation targets
#
prefix      = /usr/local
exec_prefix = ${prefix}
datarootdir = ${prefix}/share
bindir      = ${exec_prefix}/bin
libdir      = ${exec_prefix}/lib
includedir  = ${prefix}/include
mandir      = ${datarootdir}/man
docdir      = ${datarootdir}/doc/${PACKAGE_TARNAME}
pdfdir      = ${docdir}
mandir      = ${datarootdir}/man
man1dir     = ${mandir}/man1
man1ext     = .1

# Compiler configuration
#
CC        = /usr/bin/gcc -std=gnu99
CFLAGS    = -O3 -fomit-frame-pointer -fstrict-aliasing -march=k8 -pthread -fPIC
LDFLAGS   = -static 
SIMDFLAGS = -msse2
CPPFLAGS  = 

# Other tools
#
AR        = /usr/bin/ar 
RANLIB    = ranlib
INSTALL   = /usr/bin/install -c

# beautification magic stolen from git 
#
QUIET_SUBDIR0 = +${MAKE} -C #space separator after -c
QUIET_SUBDIR1 = 
ifndef V
	QUIET_CC      = @echo '    ' CC $@;
	QUIET_GEN     = @echo '    ' GEN $@;
	QUIET_AR      = @echo '    ' AR $@;
	QUIET_SUBDIR0 = +@subdir=
	QUIET_SUBDIR1 = ; echo '    ' SUBDIR $$subdir; \
		        ${MAKE} -C $$subdir
endif

# Programs installed by HMMER (stable, documented)
#
PROGS = alimask\
	hmmalign\
	hmmbuild\
	hmmconvert\
	hmmemit\
	hmmfetch\
	hmmpress\
	hmmscan\
	hmmsearch\
	hmmsim\
	hmmstat\
	jackhmmer\
	phmmer\
	nhmmer\
	nhmmscan\
	hmmpgmd

.PHONY: all dev check pdf install uninstall clean distclean TAGS

# all: Compile all documented executables.
#      (Excludes test programs.)
#
all: 
	${QUIET_SUBDIR0}${ESLDIR}     ${QUIET_SUBDIR1} all
	${QUIET_SUBDIR0}${SADIR}      ${QUIET_SUBDIR1} all
	${QUIET_SUBDIR0}src           ${QUIET_SUBDIR1} all
	${QUIET_SUBDIR0}profmark      ${QUIET_SUBDIR1} all

# dev: compile all executables, including drivers.
#
dev: 
	${QUIET_SUBDIR0}${ESLDIR}  ${QUIET_SUBDIR1} dev
	${QUIET_SUBDIR0}${SADIR}   ${QUIET_SUBDIR1} all
	${QUIET_SUBDIR0}src        ${QUIET_SUBDIR1} dev
	${QUIET_SUBDIR0}profmark   ${QUIET_SUBDIR1} dev

# tests: compile all test drivers for 'make check'
#
tests:
	${QUIET_SUBDIR0}${ESLDIR}  ${QUIET_SUBDIR1} tests
	${QUIET_SUBDIR0}src        ${QUIET_SUBDIR1} tests

# check: Run test suites.
#
check:
	${QUIET_SUBDIR0}${ESLDIR}  ${QUIET_SUBDIR1} tests
	${QUIET_SUBDIR0}${SADIR}   ${QUIET_SUBDIR1} all	
	${QUIET_SUBDIR0}src        ${QUIET_SUBDIR1} tests
	${QUIET_SUBDIR0}${ESLDIR}  ${QUIET_SUBDIR1} check
	${QUIET_SUBDIR0}testsuite  ${QUIET_SUBDIR1} check

# pdf: compile the User Guides.
#
pdf:
	${QUIET_SUBDIR0}documentation ${QUIET_SUBDIR1} pdf

# install: installs the binaries in ${bindir}/
#          When man pages are done, will install man pages in MANDIR/man1/  (e.g. if MANSUFFIX is 1)
#          Creates these directories if they don't exist.
#          Prefix those paths with ${DESTDIR} (rarely used, usually null;
#          may be set on a make command line when building contrib RPMs).
install: 
	${INSTALL} -d ${DESTDIR}${bindir}
	${INSTALL} -d ${DESTDIR}${libdir}
	${INSTALL} -d ${DESTDIR}${includedir}
	${INSTALL} -d ${DESTDIR}${man1dir}
	${INSTALL} -d ${DESTDIR}${pdfdir}
	${QUIET_SUBDIR0}src           ${QUIET_SUBDIR1} install
	${QUIET_SUBDIR0}documentation ${QUIET_SUBDIR1} install

# uninstall: Reverses the steps of "make install".
#
uninstall: 
	${QUIET_SUBDIR0}src           ${QUIET_SUBDIR1} uninstall
	${QUIET_SUBDIR0}documentation ${QUIET_SUBDIR1} uninstall

# "make clean" removes almost everything except configuration files.
#
clean:
	${QUIET_SUBDIR0}src           ${QUIET_SUBDIR1} clean
	${QUIET_SUBDIR0}profmark      ${QUIET_SUBDIR1} clean
	${QUIET_SUBDIR0}testsuite     ${QUIET_SUBDIR1} clean
	${QUIET_SUBDIR0}documentation ${QUIET_SUBDIR1} clean
	${QUIET_SUBDIR0}${ESLDIR}     ${QUIET_SUBDIR1} clean
	${QUIET_SUBDIR0}${SADIR}      ${QUIET_SUBDIR1} clean
	-rm -f *.o *~ Makefile.bak core TAGS gmon.out

# "make distclean" leaves a pristine source distribution.
#
distclean:
	${QUIET_SUBDIR0}src           ${QUIET_SUBDIR1} distclean
	${QUIET_SUBDIR0}profmark      ${QUIET_SUBDIR1} distclean
	${QUIET_SUBDIR0}testsuite     ${QUIET_SUBDIR1} distclean
	${QUIET_SUBDIR0}documentation ${QUIET_SUBDIR1} distclean
	${QUIET_SUBDIR0}${ESLDIR}     ${QUIET_SUBDIR1} distclean
	${QUIET_SUBDIR0}${SADIR}      ${QUIET_SUBDIR1} distclean
	-rm config.log config.status
	-rm -rf autom4te.cache
	-rm -f *.o *~ Makefile.bak core TAGS gmon.out
	-rm -f cscope.po.out cscope.out cscope.in.out cscope.files
	-rm -f release-notes/LICENSE.sh
	-rm -f src/impl
	-rm Makefile

TAGS:
	-rm -f ${top_srcdir}/TAGS
	make tags-append	

tags-append:
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/Makefile.in
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/COPYRIGHT
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/INSTALL
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/LICENSE
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/README
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/configure.ac

	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/*.c
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/*.h
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/*.in
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/*.pl

	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/impl_sse/*.c
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/impl_sse/*.h
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/impl_sse/*.in

	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/impl_dummy/*.c
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/impl_dummy/*.h
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/impl_dummy/*.in

	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/impl_vmx/*.c
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/impl_vmx/*.h
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/src/impl_vmx/*.in

	etags -o ${top_srcdir}/TAGS -a ${srcdir}/documentation/man/*.in
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/documentation/man/*.man
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/documentation/man/boilerplate-tail

	etags -o ${top_srcdir}/TAGS -a ${srcdir}/documentation/userguide/*.in
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/documentation/userguide/*.tex

	etags -o ${top_srcdir}/TAGS -a ${srcdir}/libdivsufsort/README
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/libdivsufsort/*.in
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/libdivsufsort/*.c

	etags -o ${top_srcdir}/TAGS -a ${srcdir}/profmark/00README
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/profmark/*.in
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/profmark/*.c
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/profmark/x-*
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/profmark/pmark-*

	etags -o ${top_srcdir}/TAGS -a ${srcdir}/testsuite/*.in
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/testsuite/*.pl
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/testsuite/*.sh
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/testsuite/*.pm
	etags -o ${top_srcdir}/TAGS -a ${srcdir}/testsuite/*.sqc

	${QUIET_SUBDIR0}easel ${QUIET_SUBDIR1} tags-append

################################################################
# HMMER - Biological sequence analysis with profile HMMs
# Version 3.1b1; May 2013
# Copyright (C) 2013 Howard Hughes Medical Institute.
# Other copyrights also apply. See the COPYRIGHT file for a full list.
# 
# HMMER is distributed under the terms of the GNU General Public License
# (GPLv3). See the LICENSE file for details.
#
# SVN $URL: https://svn.janelia.org/eddylab/eddys/src/hmmer/branches/3.1/Makefile.in $
# SVN $Id: Makefile.in 4404 2013-02-21 20:41:46Z wheelert $
################################################################
