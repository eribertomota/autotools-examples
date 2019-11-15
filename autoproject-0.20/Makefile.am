#                                       -*- makefile -*-
# Note: `lib' in the following triggers a bug in automake 1.4
EXTRA_DIST=autoproject.lsm autoproject.lsm.in autoproject.in 	\
	aclocal.m4 autoproject.1 lib chk chkag chkar chkclig chkcc

install-data-local:
	for f in `(cd $(srcdir)/lib; find . -type d)`; do		\
	  $(INSTALL) -d $(DESTDIR)$(datadir)/autoproject/$$f;			\
	done;								\
	for f in `(cd $(srcdir)/lib; find . -type f)`; do		\
	  $(INSTALL_DATA) $(srcdir)/lib/$$f $(DESTDIR)$(datadir)/autoproject/$$f;	\
	done

uninstall-local:
	rm -rf $(DESTDIR)$(datadir)/autoproject

bin_SCRIPTS=autoproject
#  if you write a self-test script named `chk', uncomment the
#  following and add `chk' to the EXTRA_DIST list
TESTS=chk chkag chkar chkclig chkcc

#  build and install the .info pages
#info_TEXINFOS = autoproject.texinfo
#  install the man page
man_MANS=autoproject.1

distclean: cleantestdirs
clean: cleantestdirs
cleantestdirs:
	rm -rf  testplain testag testar testclig testcc

autoproject.lsm autoproject: configure.in

all: autoproject
	chmod +x autoproject