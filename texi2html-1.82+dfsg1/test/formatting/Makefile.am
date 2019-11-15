EXTRA_DIST = def_cmds.texi menus.texi quotation.texi \
 float_with_at_commands.texi float_copying.texi macro_in_menu.texi \
 ref_in_anchor.texi tex.texi block_EOL.texi detailmenus.texi \
 commands_in_ifset.texi simplest.texi punctuation.texi def_end_of_line.texi \
 center.texi tables.texi formats_in_menu.texi heading.texi quotes.texi \
 indicateurl_paragraph.texi complex_command_in_simple_command.texi \
 symbol_after_block.texi html-extrali.texi html-para.texi html-title.texi \
 images.texi index_in_item_line_table.texi index_in_item_line_vtable.texi \
 index_in_item_line_table_in_code.texi table_in_table_item.texi \
 nested_formats.texi inter_item_commands.texi multitables.texi \
 double_style_paragraph.texi \
 f--ile.gif f--ile.jpeg f--ile.png f---ile.gr--a f--ile.jpg f--ile.txt \
 simple_menu.init weird_quotes.init redefine_need.init file.css tests.txt res

DISTCLEANFILES = l2h_tmp_dir.init tests.log tests.out

distclean-local:
	rm -rf out diffs

dist-hook:
	rm -rf `find $(distdir)/res -name CVS`
