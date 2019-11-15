EXTRA_DIST = contents_at_begin.texi contents_at_end.texi \
 contents_in_middle_chapter.texi contents_in_middle_section.texi \
 double_contents.texi double_contents_setcontentsaftertitlepage.texi \
 no_content.texi no_content_setcatpage.texi \
 do_contents.init inline.init tests.txt res

DISTCLEANFILES = l2h_tmp_dir.init tests.log tests.out

distclean-local:
	rm -rf out diffs

dist-hook:
	rm -rf `find $(distdir)/res -name CVS`
