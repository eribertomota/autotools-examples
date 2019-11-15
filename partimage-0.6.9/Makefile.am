SUBDIRS = m4 po src

doc_DATA = AUTHORS BUGS COPYING ChangeLog README README.partimaged partimage.lsm

EXTRA_DIST = config.rpath mkinstalldirs autogen.sh ABOUT-NLS \
             FORMAT INSTALL THANKS $(doc_DATA)

certificates:
	if test -f $(opensslpath) ; then \
	echo "generating certificate for partimage/partimaged ssl" ;\
	$(mkinstalldirs) $(DESTDIR)${sysconfdir} ;\
	$(mkinstalldirs) $(DESTDIR)${sysconfdir}/partimaged ;\
	$(opensslpath) req -new -x509 -outform PEM > \
           $(DESTDIR)${sysconfdir}/partimaged/partimaged.csr ;\
	$(opensslpath) rsa -in privkey.pem -out \
           $(DESTDIR)${sysconfdir}/partimaged/partimaged.key ;\
	rm -f privkey.pem ;\
	$(opensslpath) x509 -in $(DESTDIR)${sysconfdir}/partimaged/partimaged.csr -out \
		$(DESTDIR)${sysconfdir}/partimaged/partimaged.cert \
		-signkey $(DESTDIR)${sysconfdir}/partimaged/partimaged.key ;\
	rm -f $(DESTDIR)${sysconfdir}/partimaged/partimaged.csr ;\
	chmod 600 $(DESTDIR)${sysconfdir}/partimaged/partimaged.key || true;\
	chmod 600 $(DESTDIR)${sysconfdir}/partimaged/partimaged.cert || true;\
	else \
	echo "SSL disabled, no certificate will be generated." ;\
	fi
	

pamfile:
	@echo "# PAM config file for Partimaged" > partimaged.pam
	@echo >> partimaged.pam
	@echo "auth 	required	pam_unix.so" >> partimaged.pam
	@echo "auth	required	pam.warn.so" >> partimaged.pam
	@echo "auth 	required	pam_listfile.so \\" >> partimaged.pam
	@echo "	onerr=fail item=user sense=allow \\" >> partimaged.pam
	@echo "	file=@SYSCONFDIR@/partimaged/partimagedusers" >> partimaged.pam
	@echo "Now you have to 'su root' and put partimaged.pam into"
	@echo "/etc/pam.d/partimaged"
	
install-data-local:
	$(mkinstalldirs) $(DESTDIR)${sysconfdir}
	$(mkinstalldirs) $(DESTDIR)${sysconfdir}/partimaged

	if test ! -f $(DESTDIR)${sysconfdir}/partimaged/partimagedusers ; then \
	echo "# note: '#' introduces comments" > \
          $(DESTDIR)${sysconfdir}/partimaged/partimagedusers ;\
	echo -n "#add only users allowed to " >>  \
           $(DESTDIR)${sysconfdir}/partimaged/partimagedusers ;\
	echo "connect partimaged" >> $(DESTDIR)${sysconfdir}/partimaged/partimagedusers ;\
	echo "# (only one login per line)" >> \
           $(DESTDIR)${sysconfdir}/partimaged/partimagedusers ;\
	echo "" >> $(DESTDIR)${sysconfdir}/partimaged/partimagedusers ;\
	echo "#sample # user 'sample' is allowed to connect partimaged" >> \
           $(DESTDIR)${sysconfdir}/partimaged/partimagedusers ;\
	chmod 600 $(DESTDIR)${sysconfdir}/partimaged/partimagedusers || true;\
	fi 

distclean-local:
	rm -rf autom4te.cache

AUTOMAKE_OPTIONS = foreign

MAINTAINERCLEANFILES = Makefile.in config.h.in configure stamp-h.in aclocal.m4\
     install-sh missing depcomp

ACLOCAL_AMFLAGS = -I m4
