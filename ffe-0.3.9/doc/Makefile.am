AUTOMAKE_OPTIONS = info-in-builddir
man_MANS = ffe.1
info_TEXINFOS = ffe.texi
ffe_TEXINFOS = texinfo.css
CLEANFILES = ffe.html ffe.info

htmldir=$(docdir)
html_DATA = ffe.html 
AM_MAKEINFOHTMLFLAGS = --no-split --css-include=texinfo.css --no-headers

EXTRA_DIST = $(man_MANS) $(info_TEXINFOS) $(html_DATA)
