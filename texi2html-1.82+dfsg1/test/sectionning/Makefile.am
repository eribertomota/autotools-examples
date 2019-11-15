EXTRA_DIST = sectionning.texi novalidate.texi first_section_no_node.texi \
 nodes_before_top.texi nodes_after_top.texi section_nodes_before_top.texi \
 nodes_after_top_before_section.texi nodes_test.texi no_section.texi \
 no_node.texi no_section_no_top.texi one_section.texi one_node.texi \
 one_node_and_section.texi first_section_and_nodes.texi double_top.texi \
 rec_nodes.texi lower_subsub.texi raiselowersections.texi \
 top_without_node.texi before_node_and_section.texi \
 section_before_chapter.texi node_footnote.texi at_commands_in_refs.texi \
 test_refs.texi equivalent_nodes.texi nodename_parentheses.texi \
 section_file.texi html-top.texi menu-whitespace.texi nodes_id.texi \
 node-whitespace.texi two_footnotes_in_nodes.texi section_in_unnumbered.texi \
 top.texi more_nodes_than_sections.texi \
 placed_things_before_element.texi menutextorder.texi semi_auto.texi \
 no_element.texi \
 test_directions.init tests.txt res

DISTCLEANFILES = l2h_tmp_dir.init tests.log tests.out

distclean-local:
	rm -rf out diffs

dist-hook:
	rm -rf `find $(distdir)/res -name CVS`
