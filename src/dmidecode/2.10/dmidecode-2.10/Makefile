VERSION = 2.10
SRCDIR  = ../dmidecode-$(VERSION)-src
SRCDIRSL = $(SRCDIR)/
BUILDDIR = .
VPATH   = $(SRCDIR)
INCLUDES = -I$(BUILDDIR) -I$(SRCDIR)
EXEEXT = .exe


include $(SRCDIR)/Makefile

CFLAGS +=  -fms-extensions -mms-bitfields -fno-exceptions \
	-fomit-frame-pointer -march=i386 -ffast-math \
	-D__USE_MINGW_ACCESS -D_LARGEFILE_SOURCE=1 \
	-D_LARGEFILE64_SOURCE=1 -D_FILE_OFFSET_BITS=64 \
	-DENABLE_RELOCATABLE -DINSTALLPREFIX=\"$(prefix)\" \
	-DINSTALLDIR=\"$(bindir)\" -DEXEEXT=\"$(EXEEXT)\" \
	-DNO_XMALLOC  -DMT -ID:/Progra~1/GnuWin32/include 

MAJOR=$(shell echo $(VERSION) | sed -e "s/\..*$$//")
MINOR=$(shell echo $(VERSION) | sed -e "s/^[^\.]*\.0*\([0-9]\+\).*$$/\1/") 
LDFLAGS += -Wl,--major-image-version=$(MAJOR) -Wl,--minor-image-version=$(MINOR)

LDFLAGS += -Wl,-s -Wl,--force-exe-suffix -Wl,--enable-auto-import \
	-Wl,--enable-runtime-pseudo-reloc -Wl,--allow-multiple-definition \
	-Wl,--enable-stdcall-fixup -LD:/Progra~1/GnuWin32/lib

.SUFFIXES:
.SUFFIXES: .c .o .rc
 
# Rule to make compiled resource (Windows)
resdir = ./resource
vpath %.rc $(resdir)
.rc.o:
	windres --include-dir $(resdir) -i $< -o $@
