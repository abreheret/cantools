# Make cantools.					-*-Makefile-*-

# Copyright (C) 2007-2016 Andreas Heitmann

# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.	See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

## Process this file with automake to produce Makefile.in

SUBDIRS = . tests

AUTOMAKE_OPTIONS= foreign subdir-objects
ACLOCAL_AMFLAGS= -I m4

LEX=@LEX@
YACC=@YACC@

#	
# What to build and install
#
lib_LTLIBRARIES = libcandbc.la libcanasc.la libcanmdf.la libcanvsb.la

bin_PROGRAMS	= dbccopy dbcls cantomat mdftomat matdump

#
# dbcls
#
dbcls_SOURCES = src/dbcls/dbcls.c
dbcls_LDADD   = libcandbc.la -lm

#
# dbccopy
#
dbccopy_SOURCES = src/dbccopy/dbccopy.c
dbccopy_LDADD	= libcandbc.la -lm

#
# cantomat
#
cantomat_SOURCES = src/cantomat/cantomat.c \
		   src/cantomat/messageDecoder.c \
		   src/cantomat/busAssignment.c \
		   src/cantomat/matWrite.c \
		   src/cantomat/messageHash.c \
		   src/cantomat/measurement.c \
		   src/cantomat/signalFormat.c \
		   src/cantomat/measurement.h \
		   src/cantomat/signalFormat.h \
		   src/cantomat/busAssignment.h \
		   src/cantomat/matWrite.h \
		   src/cantomat/messageHash.h \
		   src/hashtable/hashtable.c \
		   src/hashtable/hashtable_itr.c \
		   src/hashtable/hashtable.h \
		   src/hashtable/hashtable_itr.h \
		   src/hashtable/hashtable_private.h

cantomat_LDADD = libcandbc.la libcanasc.la libcanvsb.la
cantomat_LDADD +=  $(MATIO_LIB) $(Z_LIB) $(HDF5_LIB) @LIBOBJS@ -lm

#
# mdftomat
#
mdftomat_SOURCES = src/mdftomat/mdftomat.c \
                   src/mdftomat/mdftomat.h

mdftomat_LDADD	   = libcanmdf.la $(MATIO_LIB) $(Z_LIB) $(HDF5_LIB) @LIBOBJS@

#
# matdump
#
matdump_SOURCES = src/matdump/matdump.c \
                   src/matdump/matdump.h

matdump_LDADD	   = $(MATIO_LIB) $(Z_LIB) $(HDF5_LIB) @LIBOBJS@

# additional include pathes necessary
AM_CPPFLAGS = -I$(top_srcdir)/src/libcandbc \
	   -I$(top_srcdir)/src/libcanmdf \
	   -I$(top_srcdir)/src/libcanvsb \
	   -I$(top_srcdir)/src/libcanasc \
	   -I$(top_srcdir)/hashtable

DEFS = $(YYDEBUG) @DEFS@

# YACC: generate token defines for LEX
AM_YFLAGS = -d

## Uncomment to enable debugging of linker script parser
YYDEBUG = -DYYDEBUG=1

#
# library headers, source, etc.
#
include_HEADERS= src/libcandbc/dbcModel.h \
		 src/libcandbc/dbcTypes.h \
		 src/libcandbc/dbcReader.h \
		 src/libcandbc/dbcWriter.h \
		 src/libcanmdf/mdfcg.h \
		 src/libcanmdf/mdfdg.h \
		 src/libcanmdf/mdffile.h \
		 src/libcanmdf/mdffilter.h \
		 src/libcanasc/ascReader.h \
		 src/libcanvsb/vsbReader.h \
		 src/cantomat/messageDecoder.h \
		 src/libcanmdf/mdfcn.h \
		 src/libcanmdf/mdfswap.h \
		 src/libcanmdf/mdftypes.h

libcandbc_la_SOURCES= \
	src/libcandbc/dbcModel.c \
	src/libcandbc/dbcReader.c \
	src/libcandbc/dbcWriter.c \
	src/libcandbc/parser.y \
	src/libcandbc/lexer.l

libcandbc_la_LIBADD= -lm

libcanasc_la_SOURCES= \
	src/libcanasc/ascReader.c

libcanvsb_la_SOURCES= \
	src/libcanvsb/vsbReader.c

libcanmdf_la_SOURCES= \
	src/libcanmdf/mdfcg.c \
	src/libcanmdf/mdfcn.c \
	src/libcanmdf/mdfdg.c \
	src/libcanmdf/mdffile.c \
	src/libcanmdf/mdffilter.c \
	src/libcanmdf/mdfmodel.c \
	src/libcanmdf/mdfsg.c

libcandbc_la_CPPFLAGS= -I$(top_builddir)/src/libcandbc \
                       -I$(top_srcdir)/src/libcandbc
libcandbc_la_LDFLAGS= -no-undefined -version-info @version_info@

libcanasc_la_CPPFLAGS= -I$(top_builddir)/src/libcanasc \
		       -I$(top_srcdir)/src/libcandbc
libcanasc_la_LDFLAGS= -no-undefined -version-info @version_info@

libcanvsb_la_CPPFLAGS= -I$(top_builddir)/src/libcanvsb \
		       -I$(top_srcdir)/src/libcandbc
libcanvsb_la_LDFLAGS= -no-undefined -version-info @version_info@

libcanmdf_la_CPPFLAGS= -I$(top_builddir)/src/libcanmdf
libcanmdf_la_LDFLAGS= -no-undefined -version-info @version_info@

MAINTAINERCLEANFILES = \
	src/libcandbc/parser.c \
	src/libcandbc/parser.h \
	src/libcandbc/lexer.c

src/libcandbc/parser.h src/libcandbc/parser.c: src/libcandbc/parser.y

install-exec-hook:
	cd $(DESTDIR)$(bindir) && \
		$(LN_S) cantomat$(EXEEXT) asctomat$(EXEEXT)
	cd $(DESTDIR)$(bindir) && \
		$(LN_S) cantomat$(EXEEXT) vsbtomat$(EXEEXT)
