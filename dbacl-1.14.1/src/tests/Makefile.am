AUTOMAKE_OPTIONS = 1.4 gnits
ACLOCAL = -I ../../config
datarootdir ?= $(prefix)/share


BTESTS = dbacl-V.sh \
	bayesol-V.sh \
	mailinspect-V.sh

LTESTS = dbacl-l.sh \
	dbacl-j.sh \
	dbacl-w3.sh \
	dbacl-alpha.sh \
	dbacl-alnum.sh \
	dbacl-graph.sh \
	dbacl-cef.sh \
	dbacl-adp.sh \
	dbacl-cef2.sh \
	dbacl-g.sh \
	dbacl-jap.sh \
	dbacl-a.sh \
	dbacl-o.sh \
	dbacl-O.sh \
	dbacl-z.sh \
	dbacl-zo.sh

MLTESTS = html.sh html-links.sh html-alt.sh \
	xml.sh 

EMTESTS = email-mbox.sh email-maildir.sh \
	email-l.sh email-pgp.sh email-uu.sh \
	email-headers.sh email-xheaders.sh email-theaders.sh \
	email-badmime1.sh email-badmime2.sh \
	email-uri.sh email-forms.sh email-scripts.sh \
	email-2047.sh email-style.sh

CTESTS = icheck.sh lscheck.sh model-sym1.sh model-sym2.sh \
	model-sym3.sh model-sum1.sh \
	class-unknown1.sh class-unknown2.sh \
	shannon.sh shannon-1.sh shannon-2.sh \
	score-1.sh score-2.sh reservoir.sh

HTESTS = pcheck-822g.sh pcheck-822b.sh \
	pcheck-821g.sh pcheck-821b.sh \
	pcheck-2822g.sh pcheck-2822b.sh \
	pcheck-2821g.sh pcheck-2821b.sh

TESTS = $(BTESTS) $(LTESTS) $(MLTESTS) $(EMTESTS) $(CTESTS) $(HTESTS)

# tests expected to fail in OSes with incomplete unicode
#XFAIL_TESTS= email-forms.sh email-pgp.sh html-alt.sh email-badmime1.sh

SAMPLEIN = sample.spam-1 sample.spam-2 sample.spam-3 sample.spam-4 \
	sample.email-5 sample.email-6 sample.spam-7 sample.spam-8 \
	sample.spam-9 sample.spam-10 sample.spam-11 \
	sample.headers-821g sample.headers-821b \
	sample.headers-822g sample.headers-822b \
	sample.headers-2821g sample.headers-2821b \
	sample.headers-2822g sample.headers-2822b

SAMPLEOUT = verify.html verify.html-links verify.html-alt \
	verify.xml \
	verify.email-l verify.email-pgp verify.email-uu verify.email-style \
	verify.email-headers verify.email-xheaders verify.email-theaders \
	verify.email-badmime1 verify.email-badmime2 \
	verify.email-uri verify.email-forms verify.email-scripts

# this is a hack. GNU make makes CURDIR available, but that doesn't exist
# on BSD make, which uses .CURDIR instead, and vice versa. So if we 
# concatenate both together, we should only get one value. 
#CURDIR = $(CURDIR)$(.CURDIR)
# this line below is another way of doing the same thing, but apparently
# it is broken on IRIX. I don't have the hardware to investigate this.
CURDIR ?= $(.CURDIR)

# use this for debugging test scripts
#TESTS_ENVIRONMENT = TESTBIN=$(srcdir)/.. DOCDIR=$(srcdir)/../../doc $(SHELL) -x
TESTS_ENVIRONMENT = TESTBIN=$(CURDIR)/.. DOCDIR=$(srcdir)/../../doc sourcedir=$(srcdir)

check_SCRIPTS = $(BTESTS) $(LTESTS) $(MLTESTS) $(EMTESTS) $(CTESTS) $(HTESTS)

EXTRA_DIST = dbacl-V.shin bayesol-V.shin mailinspect-V.shin \
	dbacl-l.shin dbacl-j.shin dbacl-w3.shin \
	dbacl-alpha.shin dbacl-alnum.shin dbacl-graph.shin \
	dbacl-cef.shin dbacl-adp.shin dbacl-cef2.shin \
	dbacl-g.shin dbacl-jap.shin \
	dbacl-a.shin dbacl-o.shin dbacl-O.shin dbacl-z.shin dbacl-zo.shin \
	html.shin html-links.shin html-alt.shin \
	xml.shin \
	email-mbox.shin email-maildir.shin \
	email-l.shin email-pgp.shin email-uu.shin email-style.shin \
	email-headers.shin email-xheaders.shin email-theaders.shin \
	email-badmime1.shin email-badmime2.shin \
	email-uri.shin email-forms.shin email-scripts.shin \
	email-2047.shin \
	icheck.shin lscheck.shin model-sym1.shin model-sym2.shin \
	model-sym3.shin model-sum1.shin \
	class-unknown1.shin class-unknown2.shin \
	shannon.shin shannon-1.shin shannon-2.shin \
	score-1.shin score-2.shin reservoir.shin \
	pcheck-822g.shin pcheck-822b.shin \
	pcheck-821g.shin pcheck-821b.shin \
	pcheck-2822g.shin pcheck-2822b.shin \
	pcheck-2821g.shin pcheck-2821b.shin \
	$(SAMPLEIN) $(SAMPLEOUT)

SUFFIXES = .shin .sh
.shin.sh:
	cat $< \
		| sed -e "s|[@]VERSION@|$(VERSION)|g" \
		> $@
	chmod +x $@
