SUBDIRS = fr

SOURCES = idjc.1_ idjc-run.1_ idjc-new.1_ idjc-rm.1_ idjc-ls.1_ idjc-auto.1_ idjc-noauto.1_
TARGETS = idjc.1 idjc-run.1 idjc-new.1 idjc-rm.1 idjc-ls.1 idjc-auto.1 idjc-noauto.1
COMMON  = reporting_bugs.part see_also.part

SUFFIXES = .1_ .1

dist_noinst_DATA = $(SOURCES) $(COMMON)
nodist_man_MANS = $(TARGETS)

$(TARGETS) : $(COMMON) Makefile.am

.1_.1:
	@sed  -e 's|VERSION|${PACKAGE_NAME}-${PACKAGE_VERSION}|'			\
		  -e '/.SH REPORTING BUGS/r ./reporting_bugs.part'				\
		  -e '/.SH SEE ALSO/r ./see_also.part'	$<	|					\
	awk -v S="$(SOURCES)" -v R=$<										\
			'BEGIN{sub(R,"",S);gsub(".1_","",S);split(S,A)}				\
			$$0=="SEE_ALSO"{printf".BR %s (1), \\ %s (1), \\ %s (1)\n",	\
			A[++i],A[++i],A[++i]}$$0!="SEE_ALSO"{print}' >$@

clean-local:
	rm -f $(TARGETS)

