CTAGS = ctags

EXTRA_DIST = cpufreqd.conf \
             README \
             INSTALL \
             NEWS \
             AUTHORS \
             TODO \
             ChangeLog
#             scripts/debian/cpufreqd \
#             scripts/gentoo/cpufreqd \
#             scripts/mandrake/cpufreqd.init.mdk \
#             scripts/suse/cpufreqd.initd-SUSE \
#             scripts/suse/cpufreqd.sysconfig \
#             examples/cpufreqd.conf-2.4 \
#             examples/cpufreqd.conf-2.6

SUBDIRS = src utils manpages

#man8_MANS = manpages/cpufreqd.8
#man5_MANS = manpages/cpufreqd.conf.5

install-data-local:
	if [ -f $(DESTDIR)/$(sysconfdir)/cpufreqd.conf ]; then \
	 echo "** preserving old configuration file **"; \
	else \
	 install -Dm 0644 $(top_srcdir)/cpufreqd.conf $(DESTDIR)/$(sysconfdir)/cpufreqd.conf; \
	fi;

tags:
	if [ -f ./tags ]; then \
		rm ./tags; \
	fi; \
	ctags -f tags src/*.[ch] utils/*.[ch];

cscope:
	if [ -f ./cscope.out ] ; then \
		rm ./cscope.out; \
	fi; \
	cscope -R -b -fcscope.out

#sysconf_DATA = cpufreqd.conf
