VS_CPP_PATH=com/xuggle
VS_CPP_PACKAGE=com.xuggle
VS_CPP_NAMESPACE=com::xuggle

include @top_builddir@/mk/Makefile.global
# defines VS_PKG_LIBRARIES.  Must be in a file that automake does not
# process at autoreconf time.
include @builddir@/Makefile.dependencies

SUBDIRS=ferry xuggler

xuggledir=$(includedir)/$(VS_CPP_PATH)
xuggle_HEADERS= \
  Xuggle.h

#noinst_PROGRAMS=xuggle-xuggler-main

lib_LTLIBRARIES = 

#xuggle_xuggler_main_SOURCES = Main.cpp
#xuggle_xuggler_main_LDADD = libxuggle.la

lib_LTLIBRARIES+= libxuggle.la
libxuggle_la_SOURCES = Xuggle.cpp
libxuggle_la_LIBADD = $(builddir)/xuggler/libxuggle-xuggler.la \
	$(builddir)/xuggler/io/libxuggle-xuggler-io.la \
	$(builddir)/ferry/libxuggle-ferry.la

libxuggle_la_LDFLAGS = \
	-no-undefined -shared \
	-static-libtool-libs -nostdlib \
	-version-number @LIB_MAJOR_VERSION@:@LIB_MINOR_VERSION@:0 \
	-XCClinker -static \
	-XCClinker -static-libgcc \
	-XCClinker -static-libstdc++ \
	-Wl,-Bstatic \
	$(VS_PKG_LIBRARIES) \
	$(VS_LDFLAGS)

if VS_OS_WINDOWS
libxuggle_la_LDFLAGS+= \
	-Wl,--add-stdcall-alias \
	-Wl,--enable-runtime-pseudo-reloc \
	-Wl,--enable-auto-image-base \
	-Wl,-Bsymbolic \
	-Wl,--warn-common \
	-Wl,--as-needed \
	-XCClinker -lmingwex \
	-XCClinker -lmingw32 \
	-XCClinker -lmoldname \
	-XCClinker -lpthread \
	-XCClinker -lmsvcrt \
	-XCClinker -ladvapi32 \
	-XCClinker -lshell32 \
	-XCClinker -luser32 \
	-XCClinker -lkernel32
endif
