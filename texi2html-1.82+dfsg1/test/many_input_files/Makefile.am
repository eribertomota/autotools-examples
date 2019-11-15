EXTRA_DIST = $(TESTS) indices_res index_split_res tex_l2h_res tex_t4ht_res

TESTS = indices.sh tex_l2h.sh tex_t4ht.sh
#TESTS = tex_l2h.sh tex_t4ht.sh

test_dirs = indices index_split tex_l2h tex_t4ht
#test_dirs = tex_l2h tex_t4ht

copy-tests:
	for dir in $(test_dirs); do \
		if [ -d "$$dir" ]; then \
			if [ -d "$${dir}_res" ]; then \
				rm -f "$${dir}_res/"*.* ;\
			else \
				mkdir "$${dir}_res/" ; \
			fi ;\
			cp -p "$$dir/"*.* "$${dir}_res/"; \
			rm -f "$${dir}_res/"*.png "$${dir}_res/"*_l2h.css; \
		else \
			echo "No dir $$dir/"; \
		fi; \
	done

DISTCLEANFILES = l2h_tmp_dir.init *.log *.out

distclean-local:
	rm -rf diffs $(test_dirs)

dist-hook:
	for dir in $(test_dirs); do \
		rm -rf `find "$(distdir)/$${dir}_res" -name CVS` ;\
	done
