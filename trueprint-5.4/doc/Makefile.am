## Makefile.am -- Process this file with automake to produce Makefile.in

man_MANS		= trueprint.1

MAINTAINERCLEANFILES	= Makefile.in
info_TEXINFOS		= trueprint.texi

# We can make a trueprint.html, but this isn't done as part of a
# normal distribution

SUFFIXES		= .html

html_docs		= trueprint.html

.texi.html:
	$(MAKEINFO) --html $<
