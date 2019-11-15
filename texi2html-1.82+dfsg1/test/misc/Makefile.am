EXTRA_DIST = testkb.texi viper.texi verbatim_html.texi templates.texi \
 tests.txt res

DISTCLEANFILES = l2h_tmp_dir.init tests.log tests.out

distclean-local:
	rm -rf out diffs

dist-hook:
	rm -rf `find $(distdir)/res -name CVS`
