kdj_modules=__init__ constants finder tools muxer demuxer tester options ui_main ui_editor ui_options

# dummy - this is just for automake to copy py-compile, as it won't do it
# if it doesn't see anything in a PYTHON variable. KateDJ is Python, but
# is installed as a normal script manually. This works as automake doesn't
# do anything for Python sources at build time, only at install time.
noinst_PYTHON=KateDJ

install-exec-local:
	${mkinstalldirs} "$(DESTDIR)$(pythondir)/kdj"
	for module in $(kdj_modules); do \
	  $(INSTALL_DATA) "${top_srcdir}/tools/KateDJ/kdj/$$module.py" "$(DESTDIR)$(pythondir)/kdj"; \
	  if test -z "${DESTDIR}"; then \
	    ${top_srcdir}/misc/autotools/py-compile --basedir "${pythondir}/kdj" "$$module.py"; \
	  else \
	    ${top_srcdir}/misc/autotools/py-compile --destdir "$(DESTDIR)" --basedir "${pythondir}/kdj" "$$module.py"; \
	  fi \
	done
	${mkinstalldirs} "$(DESTDIR)$(bindir)"
	${INSTALL_SCRIPT} "${top_srcdir}/tools/KateDJ/KateDJ" "$(DESTDIR)$(bindir)"

uninstall-local:
	for module in $(kdj_modules); do \
	  rm "$(DESTDIR)$(pythondir)/kdj/$$module.py"; \
	  rm "$(DESTDIR)$(pythondir)/kdj/$$module.pyc"; \
	  rm "$(DESTDIR)$(pythondir)/kdj/$$module.pyo"; \
	done
	rmdir "$(DESTDIR)$(pythondir)/kdj"
	rm "$(DESTDIR)$(bindir)/KateDJ"

EXTRA_DIST=KateDJ $(foreach module, $(kdj_modules), kdj/$(module).py)
