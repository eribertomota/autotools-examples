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
dist_pkgdata_SCRIPTS = \
	Parse_conf.pm \
	Parse_mc.pm \
	dynamic \
    parse_mc \
    sendmail \
	update_auth update_authm4 \
    update_conf \
    update_db \
	update_ldap \
    update_mc \
    update_mk \
    update_notices \
    update_sendmail \
    update_smrsh \
    update_sys \
    update_tcpd \
	update_tls update_tlsm4
dist_sbin_SCRIPTS = \
	sendmailconfig
#
# Shipped manpages
#
dist_man_MANS = \
	runq.sendmail.8 \
	sendmailconfig.8
#
# Shipped data
#
nobase_dist_sysconf_DATA = \
	mail/service.switch \
	mail/service.switch-nodns \
	mail/peers/provider
#
# Local customisation... not automake friendly (should all be SCRIPTS) :(
#
install-data-hook:
	${LN_S} sendmail ${DESTDIR}${pkgdatadir}/hoststat;
	${LN_S} sendmail ${DESTDIR}${pkgdatadir}/mailstats;
	${LN_S} sendmail ${DESTDIR}${pkgdatadir}/mailq;
	${LN_S} sendmail ${DESTDIR}${pkgdatadir}/newaliases;
	${LN_S} sendmail ${DESTDIR}${pkgdatadir}/purgestat;
	${LN_S} sendmail ${DESTDIR}${pkgdatadir}/runq;
	${LN_S} sendmail ${DESTDIR}${pkgdatadir}/status;
#
# Debian targets, phase out
#
.PHONY: build-indep build-arch
.PHONY: install-indep install-arch
build-indep:
build-arch:
install-indep: install
install-arch:
