# $FreeBSD: src/lib/libthr/Makefile,v 1.40.2.1.6.1 2010/12/21 17:09:25 kensmith Exp $
#
# All library objects contain FreeBSD revision strings by default; they may be
# excluded as a space-saving measure.  To produce a library that does
# not contain these strings, add -DSTRIP_FBSDID (see <sys/cdefs.h>) to CFLAGS
# below.  Note, there are no IDs for syscall stubs whose sources are generated.
# To included legacy CSRG sccsid strings, add -DLIBC_SCCS and -DSYSLIBC_SCCS
# (for system call stubs) to CFLAGS below.  -DSYSLIBC_SCCS affects just the
# system call stubs.

SHLIBDIR?= /lib

.include <bsd.own.mk>
MK_SSP=	no

LIB=thr
SHLIB_MAJOR= 3
WARNS?=	3
CFLAGS+=-DPTHREAD_KERNEL
CFLAGS+=-I${.CURDIR}/../libc/include -I${.CURDIR}/thread \
	-I${.CURDIR}/../../include
CFLAGS+=-I${.CURDIR}/arch/${MACHINE_ARCH}/include
CFLAGS+=-I${.CURDIR}/sys
CFLAGS+=-I${.CURDIR}/../../libexec/rtld-elf
CFLAGS+=-I${.CURDIR}/../../libexec/rtld-elf/${MACHINE_ARCH}
CFLAGS+=-I${.CURDIR}/../libthread_db
CFLAGS+=-Winline
LDFLAGS+=-Wl,-znodelete

VERSION_DEF=${.CURDIR}/../libc/Versions.def
SYMBOL_MAPS=${.CURDIR}/pthread.map

MAN=	libthr.3

# enable extra internal consistancy checks
CFLAGS+=-D_PTHREADS_INVARIANTS
#CFLAGS+=-g

PRECIOUSLIB=

.include "${.CURDIR}/arch/${MACHINE_ARCH}/Makefile.inc"
.include "${.CURDIR}/sys/Makefile.inc"
.include "${.CURDIR}/thread/Makefile.inc"

.if ${MK_INSTALLLIB} != "no"
SYMLINKS+=lib${LIB}.a ${LIBDIR}/libpthread.a
.endif
.if !defined(NO_PIC)
SYMLINKS+=lib${LIB}.so ${LIBDIR}/libpthread.so
.endif
.if ${MK_PROFILE} != "no"
SYMLINKS+=lib${LIB}_p.a ${LIBDIR}/libpthread_p.a
.endif

.if !defined(WITHOUT_SYSCALL_COMPAT)
CFLAGS+=-DSYSCALL_COMPAT
.endif

.if ${MACHINE_ARCH} == "avm2"
CFLAGS+=-DPREVENT_SYMBOL_HIDING
.endif

.include <bsd.lib.mk>
