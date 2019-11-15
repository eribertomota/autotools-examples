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
# Shipped data
#
# Installed cf subdirectories
CF_DIRS = cf debian domain feature hack m4 mailer ostype
#
# Local customisation... not automake friendly
#
install-data-hook:
	$(INSTALL) -d ${DESTDIR}${pkgdatadir}/cf;
	cp -a ${top_srcdir}/../${buildtree}/cf/* ${DESTDIR}${pkgdatadir}/cf;
	chmod a+x ${DESTDIR}${pkgdatadir}/cf/sh/makeinfo.sh;
	$(RM) ${DESTDIR}${pkgdatadir}/cf/README;
	$(RM) ${DESTDIR}${pkgdatadir}/cf/sendmail.schema;
	$(RM) ${DESTDIR}${pkgdatadir}/cf/cf/Build;
	$(RM) ${DESTDIR}${pkgdatadir}/cf/cf/Makefile;
	$(RM) ${DESTDIR}${pkgdatadir}/cf/cf/*.cf;
	for dir in ${CF_DIRS}; do \
		$(INSTALL) -d ${DESTDIR}${pkgdatadir}/cf/$$dir; \
		find $$dir -type f -name '*.mc' -o  -name '*.m4' \
			| xargs -ri \
			$(INSTALL_DATA) '{}' ${DESTDIR}${pkgdatadir}/cf/'{}'; \
		done;
	if [ -f ${top_srcdir}/../${buildtree}/contrib/domainmap.m4 ]; then \
		$(INSTALL_DATA) ${top_srcdir}/../${buildtree}/contrib/domainmap.m4 \
			${DESTDIR}${pkgdatadir}/cf/feature; \
		fi;
	if [ -f ${top_srcdir}/../${buildtree}/contrib/dnsblaccess.m4 ]; then \
		$(INSTALL_DATA) ${top_srcdir}/../${buildtree}/contrib/dnsblaccess.m4 \
			${DESTDIR}${pkgdatadir}/cf/hack; \
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
