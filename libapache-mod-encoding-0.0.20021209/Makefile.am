
LIBS     = @LIBS@
CPPFLAGS = @CPPFLAGS@

EXTRA_DIST = mod_encoding.c Makefile.simple

all-local: mod_encoding.so

mod_encoding.so: mod_encoding.c
	$(APXS) -c $(CPPFLAGS) $(APXSFLAGS) $(LIBS) $<

install-exec-local:
	$(APXS) -i mod_encoding.so

clean-local:
	rm -f *~ *.o *.so
