HEADERFILESCHECK:

./$(DEPDIR)/HEADERFILES: HEADERFILESCHECK
	echo "HEADERFILES = \\" > HEADERFILES
	find $(srcdir) -name \*.h -a ! -name ArcVersion.h -print | sort | \
		sed -e 's|^$(srcdir)/||' -e 's/$$/ \\/' >> HEADERFILES
	echo "./$(DEPDIR)/HEADERFILES" >> HEADERFILES
	if diff ./$(DEPDIR)/HEADERFILES HEADERFILES >/dev/null 2>&1 ; then \
		rm -f HEADERFILES ; \
	else \
		mkdir -p ./$(DEPDIR) ; \
		mv HEADERFILES ./$(DEPDIR)/HEADERFILES ; \
	fi

include ./$(DEPDIR)/HEADERFILES

EXTRA_DIST = $(HEADERFILES)
