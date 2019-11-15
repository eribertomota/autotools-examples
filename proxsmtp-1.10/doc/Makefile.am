
man_MANS = proxsmtpd.8 proxsmtpd.conf.5
EXTRA_DIST = $(man_MANS) proxsmtpd.conf

# Simple way to make docs
html:
	perl man2html.pl proxsmtpd.8 > proxsmtpd.html
	perl man2html.pl proxsmtpd.conf.5 > proxsmtpd.conf.html

