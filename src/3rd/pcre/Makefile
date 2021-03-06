ROOT := ../../../

include $(TOP)$(ROOT)config/global.mk

LIBNAME := hbpcre

HB_BUILD_WARN := no
HB_BUILD_MODE := c

C_SOURCES := \
   pcre_byte_order.c \
   pcre_chartables.c \
   pcre_compile.c \
   pcre_config.c \
   pcre_dfa_exec.c \
   pcre_exec.c \
   pcre_fullinfo.c \
   pcre_get.c \
   pcre_globals.c \
   pcre_maketables.c \
   pcre_newline.c \
   pcre_ord2utf8.c \
   pcre_refcount.c \
   pcre_study.c \
   pcre_tables.c \
   pcre_ucd.c \
   pcre_valid_utf8.c \
   pcre_version.c \
   pcre_xclass.c \

ifneq ($(HB_HAS_PCRE_LOCAL),)

   HB_CFLAGS += -DSUPPORT_UTF -DSUPPORT_UCP
   # only needed for win/wce, for other platforms this is no-op
   HB_CFLAGS_STA := -DPCRE_STATIC

   ifneq ($(filter $(HB_COMPILER),gcc clang clang64 mingw mingw64 sunpro),)
      ifeq ($(filter $(HB_PLATFORM)-$(HB_COMPILER),win-clang win-clang64),)
         HB_CFLAGS += -DHAVE_INTTYPES_H
      endif
   endif

   HB_CFLAGS += -DHAVE_CONFIG_H

   # workaround for problems in sunpro x86 PIC builds exploited by hbpcre library code
   ifeq ($(HB_COMPILER),sunpro)
      ifeq ($(HB_PLATFORM),sunos)
         ifeq ($(findstring sparc,$(shell isalist)),)
            HB_CFLAGS += -xbuiltin=%none
         endif
      else
         HB_CFLAGS += -xbuiltin=%none
      endif
   endif

   # suppress bcc warnings
   ifeq ($(HB_COMPILER),bcc)
      HB_CFLAGS += -w-use -w-csu -w-aus -w-sig
   endif

   include $(TOP)$(ROOT)config/lib.mk
else
   HB_SKIP_REASON := local copy unused
   include $(TOP)$(ROOT)config/none.mk
endif

# ORIGIN https://pcre.org/
# URL    https://ftp.pcre.org/pub/pcre/pcre-8.41.tar.bz2
#
# MAP    LICENCE
# MAP    config.h.generic        config.h
# MAP    pcre.h.generic          pcre.h
# MAP    pcre_internal.h
# MAP    ucp.h
# MAP    pcre_chartables.c.dist  pcre_chartables.c
# MAP    pcre_byte_order.c
# MAP    pcre_compile.c
# MAP    pcre_config.c
# MAP    pcre_dfa_exec.c
# MAP    pcre_exec.c
# MAP    pcre_fullinfo.c
# MAP    pcre_get.c
# MAP    pcre_globals.c
# MAP    pcre_maketables.c
# MAP    pcre_newline.c
# MAP    pcre_ord2utf8.c
# MAP    pcre_refcount.c
# MAP    pcre_study.c
# MAP    pcre_tables.c
# MAP    pcre_ucd.c
# MAP    pcre_valid_utf8.c
# MAP    pcre_version.c
# MAP    pcre_xclass.c
