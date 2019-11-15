EXTRA_DIST = custhtml.texi  ifo.texi       options.texi    texi2html.texi \
custpage.texi  initfile.texi  reference.texi  version.texi \
custhtml-header.htmltexi \
 tests.txt res

DISTCLEANFILES = l2h_tmp_dir.init tests.log tests.out

distclean-local:
	rm -rf out diffs

dist-hook:
	rm -rf `find $(distdir)/res -name CVS`
