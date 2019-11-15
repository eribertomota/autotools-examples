EXTRA_DIST = cvs.texi info-stnd.texi texinfo.texi mini_ker.texi \
 version-stnd.texi version.texi fdl.texi \
 mini_ker_t2h.init cvs.init tests.txt res

DISTCLEANFILES = l2h_tmp_dir.init tests.log tests.out

distclean-local:
	rm -rf out diffs

dist-hook:
	rm -rf `find $(distdir)/res -name CVS`
