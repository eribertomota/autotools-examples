EXTRA_DIST = brace_not_closed.texi recursive_copying.texi \
 bad_nesting.texi code_not_closed.texi formats_not_closed.texi \
 commands_not_closed.texi math_not_closed.texi not_closed_in_menu.texi \
 macro_call_not_closed.texi macro_def_not_closed.texi ignored_not_closed.texi \
 verb_not_closed.texi tex_not_closed.texi html_not_closed.texi \
 verbatim_not_closed.texi copying_not_closed.texi node_in_copying.texi \
 tex_in_copying.texi titlepage_not_closed.texi footnote_not_closed.texi \
 caption_not_closed.texi def_cmd_dble.texi style_not_closed_in_table_line.texi \
 style_not_closed_in_cartouche.texi multitable_too_much_col.texi \
 tests.txt res

DISTCLEANFILES = l2h_tmp_dir.init tests.log tests.out

distclean-local:
	rm -rf out diffs

dist-hook:
	rm -rf `find $(distdir)/res -name CVS`
