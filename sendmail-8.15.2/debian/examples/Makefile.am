#!/usr/bin/make -f
#------------------------------------------------------------------------------
# vim: syntax=make
#
# $Sendmail: Makefile,v @sm_version@ @sm_date@ @sm_time@ cowboy Exp $
#
# Copyright (c) 1998-@SM_CPYRT@ Richard Nelson.  All Rights Reserved.
#
# @configure_input@
#
# Rules file for Sendmail @sm_version@@sm_revision@(@sm_version_math@)
#			 on  @sm_dist_name@ @sm_dist_vers@
#			 via Debhelper V@DEBIAN_DH@
#
# Note: the .in file supports Sendmail @SM_MINVERS@ - @SM_MAXVERS@
#		on Debian slink, potato, woody, testing, sid, ...
#		but the generated file is customized to the version noted above.
#
# Richard Nelson <cowboy@debian.org> @sm_date@ @sm_time@ (@sm_utc@)
#------------------------------------------------------------------------------
#
# Shipped programs
#
dist_sbin_SCRIPTS = checksendmail/checksendmail
#
# Shipped manpages
#
dist_man_MANS = checksendmail/checksendmail.8
#
# Shipped data
#
# Installed example subdirectories
EXAMPLES_DIRS = amavis db dhcp \
	ldap logcheck milter network \
	pam.d ppp resolvconf sasl tls
#
# Sigh... I wanted to use sysconf_SCRIPTS, but automake says NO!
nobase_dist_sysconf_DATA = dhcp/dhclient-exit-hooks.d/sendmail \
	logcheck/ignore.d.paranoid/sendmail \
	logcheck/ignore.d.server/sendmail \
	logcheck/ignore.d.workstation/sendmail \
	logcheck/violations.ignore.d/logcheck-sendmail \
	network/if-down.d/sendmail network/if-post-down.d/sendmail \
	network/if-up.d/sendmail pam.d/smtp ppp/ip-down.d/sendmail \
	ppp/ip-up.d/sendmail resolvconf/update-libc.d/sendmail
#
# Local customisation... not automake friendly
#
install-data-hook:
	$(INSTALL) -d ${DESTDIR}${pkgdatadir}/examples;
	for dir in ${EXAMPLES_DIRS}; do \
		$(INSTALL) -d ${DESTDIR}${pkgdatadir}/examples/$$dir; \
		find $$dir -type f \
			! -name '*.in' -a ! -name '*.am' -a ! -name '*.old' \
			| xargs -ri \
			$(INSTALL_DATA) '{}' ${DESTDIR}${pkgdatadir}/examples/'{}'; \
		done;
	chmod a+rx ${DESTDIR}${pkgdatadir}/examples/milter/Makefile;
	chmod a+rx ${DESTDIR}${pkgdatadir}/examples/dhcp/dhclient-exit-hooks.d/sendmail;
	chmod a+rx ${DESTDIR}${pkgdatadir}/examples/network/if-down.d/sendmail;
	chmod a+rx ${DESTDIR}${pkgdatadir}/examples/network/if-post-down.d/sendmail;
	chmod a+rx ${DESTDIR}${pkgdatadir}/examples/network/if-up.d/sendmail;
	chmod a+rx ${DESTDIR}${pkgdatadir}/examples/ppp/ip-down.d/sendmail;
	chmod a+rx ${DESTDIR}${pkgdatadir}/examples/ppp/ip-up.d/sendmail;
	chmod a+rx ${DESTDIR}${pkgdatadir}/examples/resolvconf/update-libc.d/sendmail;
	chmod a+rx ${DESTDIR}${sysconfdir}/dhcp/dhclient-exit-hooks.d/sendmail;
	chmod a+rx ${DESTDIR}${sysconfdir}/network/if-down.d/sendmail;
	chmod a+rx ${DESTDIR}${sysconfdir}/network/if-post-down.d/sendmail;
	chmod a+rx ${DESTDIR}${sysconfdir}/network/if-up.d/sendmail;
	chmod a+rx ${DESTDIR}${sysconfdir}/ppp/ip-down.d/sendmail;
	chmod a+rx ${DESTDIR}${sysconfdir}/ppp/ip-up.d/sendmail;
	chmod a+rx ${DESTDIR}${sysconfdir}/resolvconf/update-libc.d/sendmail;
	$(INSTALL_DATA) checksendmail/address.resolve \
		${DESTDIR}${sysconfdir}/mail/;
install-exec-hook:
	sed -e "s?/etc/sendmail.cf?${sysconfdir}/mail/sendmail.cf?g" \
		-e "s?address.resolve?${sysconfdir}/mail/address.resolve?g" \
		checksendmail/checksendmail \
		> ${DESTDIR}${sbindir}/checksendmail;
	chmod 0755 ${DESTDIR}${sbindir}/checksendmail;
	if [ -f ${top_srcdir}/../${buildtree}/contrib/buildvirtuser ]; then \
		$(INSTALL_SCRIPT) ${top_srcdir}/../${buildtree}/contrib/buildvirtuser \
			${DESTDIR}${pkgdatadir}/; \
		fi;
	sed 's?/bin/perl?/usr/bin/perl?g' \
		${top_srcdir}/../${buildtree}/contrib/passwd-to-alias.pl \
		> ${DESTDIR}${pkgdatadir}/examples/passwd-to-alias;
	chmod 0755 ${DESTDIR}${pkgdatadir}/examples/passwd-to-alias;
	sed -e 's?/usr/\(local\|perl5\)/bin/perl?/usr/bin/perl?g' \
		-e "s?/etc/sendmail.cf?${sysconfdir}/mail/sendmail.cf?g" \
		${top_srcdir}/../${buildtree}/contrib/etrn.pl \
		> ${DESTDIR}${sbindir}/etrn;
		chmod 0755 ${DESTDIR}${sbindir}/etrn;
	if [ -f ${top_srcdir}/../${buildtree}/contrib/etrn.0 ]; then \
		sed -e 's?/usr/\(local\|perl5\)/bin/perl?/usr/bin/perl?g' \
			-e 's?etrn(1M)?etrn(8)?g' \
			${top_srcdir}/../${buildtree}/contrib/etrn.0 \
			> ${DESTDIR}${mandir}/man8/etrn.8; \
	else \
		sed -e 's?/usr/\(local\|perl5\)/bin/perl?/usr/bin/perl?g' \
			-e 's?etrn(1M)?etrn(8)?g' \
			${top_srcdir}/../${buildtree}/contrib/etrn.pl \
			> ${DESTDIR}${mandir}/man8/etrn.8; \
		fi;
	sed -e 's?/usr/local/bin/perl?/usr/bin/perl?g' \
		${top_srcdir}/../${buildtree}/contrib/expn.pl \
		> ${DESTDIR}${bindir}/expn;
	chmod 0755 ${DESTDIR}${bindir}/expn;
	sed -e 's?/usr/local/bin/perl?/usr/bin/perl?g' \
		${top_srcdir}/../${buildtree}/contrib/expn.pl \
		> ${DESTDIR}${mandir}/man1/expn.1;
	sed -e 's?/usr/local/bin/perl?/usr/bin/perl?g' \
		-e 's?/usr/sbin/sendmail -q30m -bd?/etc/init.d/sendmail start?g' \
		${top_srcdir}/../${buildtree}/contrib/smcontrol.pl \
		> ${DESTDIR}${pkgdatadir}/smcontrol.pl;
	chmod 0755 ${DESTDIR}${pkgdatadir}/smcontrol.pl;
	$(INSTALL_SCRIPT) ${top_srcdir}/../${buildtree}/contrib/doublebounce.pl \
		${DESTDIR}${pkgdatadir};
	if [ -f ${top_srcdir}/../${buildtree}/contrib/qtool.pl ]; then \
		sed -e 's?/usr/bin/env perl?/usr/bin/perl?g' \
			${top_srcdir}/../${buildtree}/contrib/qtool.pl \
			> ${DESTDIR}${pkgdatadir}/qtool.pl; \
		chmod 0755 ${DESTDIR}${datadir}/sendmail/qtool.pl; \
		$(INSTALL_DATA) ${top_srcdir}/../${buildtree}/contrib/qtool.8 \
			${DESTDIR}${mandir}/man8/; \
		fi;
#
# Debian targets, phase out (this needs to be treated as -arch, not -indep)
#
.PHONY: build-indep build-arch
.PHONY: install-indep install-arch
build-indep:
build-arch:
install-indep: install
install-arch:
