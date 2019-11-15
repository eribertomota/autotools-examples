bin_SCRIPTS = gkdebconf-term

gkdebconf-term.pot: gkdebconf-term
	xgettext -L Shell -o gkdebconf-term.pot gkdebconf-term

update-po: gkdebconf-term.pot
	for i in *.po; do \
		msgmerge -o $$i $$i gkdebconf-term.pot; \
	done

update-gmo: update-po
	for i in *.po; do \
		msgfmt --statistics -o $${i/po/gmo} $$i; \
	done

install-data-local:
	for i in *.gmo; do \
		install -D -m 644 ./$$i \
		 ${DESTDIR}${prefix}/share/locale/`basename $$i .gmo`/LC_MESSAGES/gkdebconf-term.mo; \
	done

all: update-gmo

.PHONY: update-po update-gmo
