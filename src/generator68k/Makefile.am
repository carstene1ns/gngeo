## Process this file with automake to produce Makefile.in

EXTRA_DIST = def68k.def compile.cg ccg/alpha ccg/asm-i386.h ccg/asm-sparc.h \
             ccg/asm-ppc.h ccg/asm-cache.h ccg/asm-common.h ccg/ccg.c \
             ccg/insns-i386.h ccg/insns-ppc.h ccg/insns-sparc.h

noinst_PROGRAMS = def68k gen68k

AM_CPPFLAGS = -I../ -I.

gcc_build_verbose = $(gcc_build_verbose_$(V))
gcc_build_verbose_ = $(gcc_build_verbose_$(AM_DEFAULT_VERBOSITY))
gcc_build_verbose_0 = @echo "  HCC    $@";

## stage one - create iibs, funcs and proto header files from def68k.def

BUILT_SOURCES = def68k-iibs.h def68k-funcs.h def68k-proto.h

def68k_SOURCES = def68k.c tab68k2.c

def68k-iibs.h : def68k def68k.def
	$(AM_V_GEN)./def68k 2>&1 >/dev/null
def68k-proto.h : def68k-iibs.h
def68k-funcs.h : def68k-iibs.h

## stage two - create cpu C files and create library

gen68k_SOURCES = gen68k.c tab68k2.c

CPU_SOURCE = cpu68k-0.c cpu68k-1.c cpu68k-2.c cpu68k-3.c cpu68k-4.c \
             cpu68k-5.c cpu68k-6.c cpu68k-7.c cpu68k-8.c cpu68k-9.c \
             cpu68k-a.c cpu68k-b.c cpu68k-c.c cpu68k-d.c cpu68k-e.c \
             cpu68k-f.c

cpu68k-0.c : gen68k
	$(AM_V_GEN)./gen68k 2>&1 >/dev/null
cpu68k-1.c : cpu68k-0.c
cpu68k-2.c : cpu68k-0.c
cpu68k-3.c : cpu68k-0.c
cpu68k-4.c : cpu68k-0.c
cpu68k-5.c : cpu68k-0.c
cpu68k-6.c : cpu68k-0.c
cpu68k-7.c : cpu68k-0.c
cpu68k-8.c : cpu68k-0.c
cpu68k-9.c : cpu68k-0.c
cpu68k-a.c : cpu68k-0.c
cpu68k-b.c : cpu68k-0.c
cpu68k-c.c : cpu68k-0.c
cpu68k-d.c : cpu68k-0.c
cpu68k-e.c : cpu68k-0.c
cpu68k-f.c : cpu68k-0.c

noinst_LIBRARIES = libgenerator68k.a
libgenerator68k_a_SOURCES = cpu68k.c reg68k.c registers.h diss68k.c \
                            mem68k.h generator.h cpu68k.h compile.h \
                            tab68k.c cpu68k-inline.h reg68k.h
nodist_libgenerator68k_a_SOURCES = def68k-iibs.h

libgenerator68k_a_LIBADD = $(CPU_SOURCE:.c=.o) #compile.o

cpu68k.c : def68k-proto.h

CLEANFILES = $(BUILT_SOURCES) $(CPU_SOURCE)

#ccg/ccg : ccg/ccg.c
#	$(COMPILE) -DCCGVERSION="\"1.1\""  ccg/ccg.c -o ccg/ccg

#compile.c : compile.cg ccg/ccg
#	./ccg/ccg -o compile.c compile.cg

#def68k.o gen68k.o tab68k2.o : %.o : %.c
#	$(gcc_build_verbose)$(CC_FOR_BUILD) -c $< -o $@ -I .. -I ../.. -I . `sdl-config --cflags`

#def68k$(EXEEXT) : def68k.o tab68k2.o
#	$(gcc_build_verbose)$(CC_FOR_BUILD) def68k.o tab68k2.o -o $@

#gen68k$(EXEEXT) : gen68k.o tab68k2.o
#	$(gcc_build_verbose)$(CC_FOR_BUILD) gen68k.o tab68k2.o -o $@

#$(CPU_SOURCE:.c=.o) : %.o : %.c
#	$(AM_V_CC)$(COMPILE) -c $< -o $@

#compile.o : compile.c 
#	$(COMPILE) -c $< -o $@
