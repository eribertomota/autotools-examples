SUFFIXES = .1 .1in
datarootdir ?= $(prefix)/share

man_MANS = dbacl.1 bayesol.1 mailcross.1 mailinspect.1 mailtoe.1 mailfoot.1 hmine.1 hypex.1
EXTRA_DIST = dbacl.1in bayesol.1in mailcross.1in mailinspect.1in mailfoot.1in mailtoe.1in hmine.1in hypex.1in spherecl.1in

pkgdocdir = /usr/share/doc/dbacl

.1in.1:
	cat $< \
		| sed -e "s|[@]VERSION@|$(VERSION)|g" \
		| sed -e "s|[@]PKGDATADIR@|$(pkgdatadir)|g" \
		| sed -e "s|[@]PKGDOCDIR@|$(pkgdocdir)|g" \
		> $@

CLEANFILES = dbacl.1 bayesol.1 mailcross.1 mailinspect.1 mailtoe.1 mailfoot.1 hmine.1 hypex.1
