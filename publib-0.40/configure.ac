#  Copyright (c) 2012 Antti-Juhani Kaijanaho
#
#  Redistribution and use in source and binary forms, with or without
#  modification, are permitted provided that the following conditions
#  are met:
#
#  1. Redistributions of source code must retain the above copyright
#     notice, this list of conditions and the following disclaimer.
#
#  2. Redistributions in binary form must reproduce the above
#     copyright notice, this list of conditions and the following
#     disclaimer in the documentation and/or other materials provided
#     with the distribution.
#
#  THIS SOFTWARE IS PROVIDED BY THE AUTHOR ``AS IS'' AND ANY EXPRESS
#  OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
#  WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
#  ARE DISCLAIMED.  IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY
#  DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
#  DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE
#  GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
#  INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
#  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
#  NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
#  SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

AC_PREREQ([2.68])
AC_INIT([publib],[0.40],[publib@lists.kaijanaho.info])
AC_CONFIG_SRCDIR([man/publib.3])


AC_PROG_CC
AX_CFLAGS_WARN_ALL

# Test for -MD
AC_MSG_CHECKING([checking whether $CC -MD -MF works])
AC_LANG(C)
rm -f main/conftest.d
AC_LANG_CONFTEST([AC_LANG_SOURCE([@%:@include "publib.h"])])
mv conftest.c main/conftest.c
$CC -Iincludes $CPPFLAGS $CFLAGS \
  -MD -MF main/conftest.d -c main/conftest.c -o main/conftest.o
if test -r main/conftest.d ; then
   MDMF='-MD -MF @S|@*.d'
   AC_MSG_RESULT(yes)
else
   MDMF=""
   AC_MSG_RESULT(no)
fi
rm -f main/conftest.d main/conftest.c main/conftest.o
AC_SUBST(MDMF)

AC_PROG_INSTALL
AC_PROG_RANLIB
AC_PROG_MKDIR_P
AC_CHECK_PROG(MAKE,gmake,gmake,make)
AC_CONFIG_FILES([Makefile])
AC_OUTPUT
