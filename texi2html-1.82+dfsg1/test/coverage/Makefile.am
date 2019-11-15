EXTRA_DIST = formatting.texi comments.texi pass0_macros.texi float.texi \
 imbrications.texi \
 f--ile.e--xt f--ile.jpg simplest.texi tests.txt res

DISTCLEANFILES = l2h_tmp_dir.init tests.log tests.out

distclean-local:
	rm -rf out diffs

dist-hook:
	rm -rf `find $(distdir)/res -name CVS`
