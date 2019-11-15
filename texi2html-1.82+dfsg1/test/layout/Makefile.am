EXTRA_DIST = no_monolithic.texi navigation.texi formatting_regions.texi \
 only_toc_out.init vertical_nav.init tests.txt res

DISTCLEANFILES = l2h_tmp_dir.init tests.log tests.out

distclean-local:
	rm -rf out diffs

dist-hook:
	rm -rf `find $(distdir)/res -name CVS`
