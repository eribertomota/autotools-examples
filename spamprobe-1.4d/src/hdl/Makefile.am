AUTOMAKE_OPTIONS=foreign
INCLUDES= -I@top_srcdir@/src/includes -I@top_srcdir@/src
noinst_LIBRARIES=libhdl.a
libhdl_a_SOURCES=\
	HdlArgumentConstraint.cc\
	HdlArgumentConstraint.h\
	HdlError.cc\
	HdlParser.cc\
	HdlPrinter.cc\
	HdlStatement.cc\
	HdlStatementConstraint.cc\
	HdlStatementConstraint.h\
	HdlStandardStatementConstraint.cc\
	HdlStandardStatementConstraint.h\
	HdlRecursiveStatementConstraint.h\
	HdlSyntaxChecker.cc\
	HdlToken.cc\
	HdlTokenizer.cc

LDADD = libhdl.a ../input/libinput.a ../utility/libutility.a

#noinst_PROGRAMS=testhdl
#testhdl_SOURCES=\
#	testhdl.cc
