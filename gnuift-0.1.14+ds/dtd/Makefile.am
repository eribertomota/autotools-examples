
noinst_DATA= ../libMRML/cc/mrml_const.cc

#	
# making a new mrml_const.cc if mrml.dtd has been changed
#
../libMRML/cc/mrml_const.cc: mrml.dtd
	$(PERL) ../scripts/perl/gift-dtd-to-keywords.pl ../dtd/mrml.dtd mrml mrml_const charmer.mrml
	mv mrml_const.h ../libMRML/include
	mv mrml_const.cc ../libMRML/cc
	mv mrml_const.java ../

EXTRA_DIST=mrml.dtd

data_DATA=mrml.dtd