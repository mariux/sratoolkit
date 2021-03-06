# ===========================================================================
#
#                            PUBLIC DOMAIN NOTICE
#               National Center for Biotechnology Information
#
#  This software/database is a "United States Government Work" under the
#  terms of the United States Copyright Act.  It was written as part of
#  the author's official duties as a United States Government employee and
#  thus cannot be copyrighted.  This software/database is freely available
#  to the public for use. The National Library of Medicine and the U.S.
#  Government have not placed any restriction on its use or reproduction.
#
#  Although all reasonable efforts have been taken to ensure the accuracy
#  and reliability of the software and data, the NLM and the U.S.
#  Government do not and cannot warrant the performance or results that
#  may be obtained by using this software or data. The NLM and the U.S.
#  Government disclaim all warranties, express or implied, including
#  warranties of performance, merchantability or fitness for any particular
#  purpose.
#
#  Please cite the author in any work or product based on this material.
#
# ===========================================================================

default: all

TOP ?= $(shell ../../build/abspath.sh ../..)
MODULE = libs/kns

INT_LIBS = \

EXT_LIBS = \
	libkns \
	libkurl

ALL_LIBS = \
	$(INT_LIBS) \
	$(EXT_LIBS)

include $(TOP)/build/Makefile.env

#-------------------------------------------------------------------------------
# outer targets
#

# we are building it on all platforms now, because dependency on libcurl is removed
all std: makedirs
	@ $(MAKE_CMD) $(TARGDIR)/std

$(INT_LIBS): makedirs
	@ $(MAKE_CMD) $(ILIBDIR)/$@

$(EXT_LIBS): makedirs
	@ $(MAKE_CMD) $(LIBDIR)/$@

.PHONY: all std $(ALL_LIBS)

#-------------------------------------------------------------------------------
# std
#
$(TARGDIR)/std: \
	$(addprefix $(ILIBDIR)/,$(INT_LIBS)) \
	$(addprefix $(LIBDIR)/,$(EXT_LIBS))

.PHONY: $(TARGDIR)/std

#-------------------------------------------------------------------------------
# clean
#
clean: stdclean

.PHONY: clean

#-------------------------------------------------------------------------------
# kns
#
$(LIBDIR)/libkns: $(addprefix $(LIBDIR)/libkns.,$(LIBEXT))

KNS_SRC = \
	kns_manager \
	stream \
	stream-from-files \
	stream-from-streams \
#	sysstream \

KNS_OBJ = \
	$(addsuffix .$(LOBX),$(KNS_SRC))

KNS_LIB = \
    -lkfs \
	-dklib

$(LIBDIR)/libkns.$(SHLX): $(KNS_OBJ)
	$(LD) --dlib --vers $(SRCDIR) -o $@ $^ $(KNS_LIB)

$(LIBDIR)/libkns.$(LIBX): $(KNS_OBJ)
	$(LD) --slib --vers $(SRCDIR) -o $@ $^ $(KNS_LIB)


#-------------------------------------------------------------------------------
# kurl
#
$(LIBDIR)/libkurl: $(addprefix $(LIBDIR)/libkurl.,$(LIBEXT))

KURL_SRC = \
	KCurlFile \
	KCurlRequest \
	url-fetcher \
	url-fetcher-curl \
	entrez-fetcher

KURL_OBJ = \
	$(addsuffix .$(LOBX),$(KURL_SRC))

KURL_LIB = \
	-skns \
	-dkfs \
	-dklib \
	-dz

$(LIBDIR)/libkurl.$(SHLX): $(KURL_OBJ)
	$(LD) --dlib --vers $(SRCDIR) -o $@ $^ $(KURL_LIB)

$(LIBDIR)/libkurl.$(LIBX): $(KURL_OBJ)
	$(LD) --slib --vers $(SRCDIR) -o $@ $^ $(KURL_LIB)
