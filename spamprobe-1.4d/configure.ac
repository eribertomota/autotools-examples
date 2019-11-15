AC_INIT
AM_INIT_AUTOMAKE(spamprobe,1.4d)
AC_PROG_CC
AC_PROG_CXX
AC_PROG_RANLIB

AC_CHECK_HEADERS(unistd.h)
AC_CHECK_HEADERS(dirent.h)

AC_EGREP_HEADER([regcomp], [regex.h], AC_DEFINE(HAVE_REGEX_H),
  AC_MSG_ERROR([POSIX regcomp() function not available]))

AC_ARG_ENABLE(default-8bit,
  [  --enable-default-8bit   Changes the default character handling to store 8 bit chars ],
  AC_DEFINE(USE_8BIT))

AC_ARG_ENABLE(cdb,
  [  --enable-cdb   Enables use of Berkeley DB concurrent data store ],
  AC_DEFINE(USE_CDB))

want_assert=0
AC_ARG_WITH(assert,
  [  --with-assert         Enables assertions for testing ],
  [ 
    if test "x$withval" != "xno" ; then
      want_assert=1
    fi
  ]
)
if test $want_assert != 1 ; then
  CPPFLAGS="-DNDEBUG $CPPFLAGS"
fi

AC_ARG_ENABLE(no-deprecated,
  [  --enable-no-deprecated         Enables annoying deprecated warning ],
  [ CXXFLAGS="-Wno-deprecated $CXXFLAGS" ])

AC_ARG_ENABLE(big-endian,
  [  --enable-big-endian   Causes all database reads and writes to use big-endian byte order ],
  AC_DEFINE(FORCE_NETWORK_ORDER))

have_database=0

AC_ARG_WITH(pbl,
  [  --with-pbl=PATH          Specify path to PBL install ],
  [
    if test "x$withval" != "xno" ; then
      if test -d "$withval/lib"; then
        LDFLAGS="-L${withval}/lib $LDFLAGS"
      else
        LDFLAGS="-L${withval} $LDFLAGS"
      fi
      if test -d "$withval/include"; then
        CPPFLAGS="-I${withval}/include $CPPFLAGS"
      else
        CPPFLAGS="-I${withval} $CPPFLAGS"
      fi
      AC_CHECK_LIB(pbl, pblIsamCommit, LIBS="$LIBS -lpbl",
        AC_CHECK_LIB(pbl, pblIsamClose, LIBS="$LIBS -lpbl",
          AC_MSG_ERROR([No suitable PBL library found.])))
      AC_TRY_LINK_FUNC(pblIsamOpen, AC_DEFINE([USE_PBL]) have_database=1)
    fi
  ]
)

if test $have_database = 0 ; then
  AC_ARG_WITH(db,
    [  --with-db=PATH          Specify path to BerkelyDB install directory ],
    [
      if test "x$withval" != "xno" ; then
        if test -d "$withval/lib"; then
          LDFLAGS="-L${withval}/lib $LDFLAGS"
        else
          LDFLAGS="-L${withval} $LDFLAGS"
        fi
        if test -d "$withval/include"; then
          CPPFLAGS="-I${withval}/include $CPPFLAGS"
        else
          CPPFLAGS="-I${withval} $CPPFLAGS"
        fi
      fi
    ],
    [
      AC_EGREP_HEADER([DB_VERSION_MAJOR *3|4], [db.h],,
        AC_MSG_ERROR([No suitable BerkeleyDB db.h header file found.
  Use --with-db=PATH to specify the path to a version 3 or later install directory.
  You can download BerkeleyDB from http://www.sleepycat.com])
      )
    ]
  )
  DAC_SEARCH_LIBS(BerkeleyDB,
                  AC_LANG_PROGRAM([[#include <db.h>]],
                    [[DB *db; DB_ENV *dbEnv; db_create(&db, dbEnv, 0);]]),
                  [db db4 db-4 db3 db-3],
                  AC_DEFINE([USE_DB]) have_database=1,
                  [],[])
fi

if test $have_database = 0 ; then
AC_ARG_WITH(gdbm,
  [  --with-gdbm=PATH        Specify path to GDBM install directory - not a good idea ],
  [
    if test "x$withval" != "xno" ; then
      if test -d "$withval/lib"; then
        LDFLAGS="-L${withval}/lib $LDFLAGS"
      else
        LDFLAGS="-L${withval} $LDFLAGS"
      fi
      if test -d "$withval/include"; then
        CPPFLAGS="-I${withval}/include $CPPFLAGS"
      else
        CPPFLAGS="-I${withval} $CPPFLAGS"
      fi
      AC_SEARCH_LIBS(dbm_store,[gdbm ndbm], AC_DEFINE([USE_DBM]) have_database=1)
    fi
  ]
)
fi

AC_TRY_LINK_FUNC(mmap,AC_DEFINE([USE_MMAP]) have_database=1)

if test $have_database = 0 ; then
  AC_MSG_ERROR([No suitable database library (PDL or BerkeleyDB version 3 or higher) found.
  Specify location of proper package location using --with-db=PATH])
fi

want_gif=1
AC_ARG_WITH(gif,
  [  --with-gif            Enables processing of gif images (default) ],
  [ 
    if test "x$withval" = "xno" ; then
      want_gif=0
    fi
  ]
)
if test $want_gif = 1 ; then
  AC_CHECK_HEADER([gif_lib.h],AC_CHECK_LIB(ungif, DGifOpen, AC_DEFINE([HAVE_UNGIF]) LIBS="$LIBS -lungif",AC_CHECK_LIB(gif, DGifOpen, AC_DEFINE([HAVE_UNGIF]) LIBS="$LIBS -lgif")))
fi

want_png=1
AC_ARG_WITH(png,
  [  --with-png            Enables processing of png images (default) ],
  [ 
    if test "x$withval" = "xno" ; then
      want_png=0
    fi
  ]
)
if test $want_png = 1 ; then
  AC_CHECK_HEADER([png.h],AC_CHECK_LIB(png, png_set_progressive_read_fn, AC_DEFINE([HAVE_PNG]) LIBS="$LIBS -lpng"))
fi

want_jpeg=1
AC_ARG_WITH(jpeg,
  [  --with-jpeg           Enables processing of jpeg images (default) ],
  [ 
    if test "x$withval" = "xno" ; then
      want_jpeg=0
    fi
  ]
)
if test $want_jpeg = 1 ; then
  AC_CHECK_HEADER([jpeglib.h],AC_CHECK_LIB(jpeg, jpeg_read_header, AC_DEFINE([HAVE_JPEG]) LIBS="$LIBS -ljpeg"))
fi

AC_PROG_INSTALL
AC_OUTPUT(Makefile src/Makefile src/database/Makefile src/hdl/Makefile src/includes/Makefile src/input/Makefile src/parser/Makefile src/utility/Makefile src/spamprobe/Makefile)
