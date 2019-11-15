SUBDIRS = prelims

am__py_compile = $(top_srcdir)/py-compile

python_PYTHON = idjcmonitor.py

idjcpkgpython_PYTHON = dialogs.py gtkstuff.py irc.py jingles.py licence_window.py \
		maingui.py midicontrols.py mutagentagger.py songdb.py playergui.py \
		popupwindow.py preferences.py sourceclientgui.py tooltips.py utils.py \
		format.py

nodist_idjcpkgpython_PYTHON = __init__.py

dist_noinst_PYTHON = __init__.py.in.in

__init__.py: __init__.py.in
	sed -e 's|$${pkgdatadir}|${pkgdatadir}|g'	\
		 -e 's|$${pkglibdir}|${pkglibdir}|g'	\
		 -e 's|$${exec_prefix}|${exec_prefix}|g' \
	     -e 's|$${prefix}|${prefix}|g'			\
	     -e 's|$${datarootdir}|${datarootdir}|g' \
	      $? >$@

clean-local:
	rm -f __init__.py

.PHONY: __init__.py $pkgpython_PYTHON
