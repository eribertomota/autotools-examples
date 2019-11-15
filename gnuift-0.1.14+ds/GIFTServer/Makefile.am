
# the bin programs to be made in this directory

SUBDIRS = gift-config gift-mrml-messages

# data_DATA= gift-config gift-mrml-messages

bin_PROGRAMS = gift gift-endianize gift-generate-inverted-file gift-modify-distance-matrix gift-one-minus 

#gift-debug-test

# generateDistanceMatrix
# should be generated, too, but
# at present this file is not maintained.
# it is not necessary for running the basic version of gift

# include directories for all programs in this dir

INCLUDES = -I$(top_srcdir)/libMRML/include -I$(top_srcdir)/libGIFTAcInvertedFile/include -I$(top_srcdir)/libGIFTAcURL2FTS/include -I$(srcdir)   -I.

#-------------------------------------------------

# the gift server

#
# remark: The perl accessor has to be linked at compile time,
# as it is unlikely that the user has a shared perl library
# installed.
#
# The -L lines will be gone when libtool 1.4 is shipping
# 1.3.5 does needs them
#
# # removed ../expat/xmlparse/*.o ../expat/xmltok/*.o  
gift_LDADD = @PRE_INSTALL_LIBDIRS@ @PRE_INSTALL_LIBDIRS@ \
	@UNPUBLISHED_DIR@ @UNPUBLISHED@ @BAYESIAN@ \
        -lGIFTQuPerl -lGIFTAcPerl -lMRML\
	@BAYESIAN_LD_ADD@\
	@PERL_LD_ADD@ -L$(libdir) 

#-lwdbi

#	-lefence \
# -lGIFTAcURL2FTS -lGIFTAcInvertedFile \
# -lGIFTAcHierarchy \
# -lGIFTQuInvertedFile  -lGIFTQuHierarchy

#@PERL_LD_ADD@

#`echo $LDFLAGS \`perl -MExtUtils::Embed -e ldopts  \`|sed 's:-Dbool=char::'` 


gift_SOURCES =  Server.cc CSocket.cc CDomainSocket.cc CTCPSocket.cc processMessage.cc CProcessMessageParameters.cc CMultiServer.cc


#-------------------------------------------------

# generate inverted file

gift_generate_inverted_file_LDADD = @PRE_INSTALL_LIBDIRS@ -lMRML -lGIFTAcInvertedFile -lGIFTAcPerl -lGIFTQuPerl @PERL_LD_ADD@ 

#	 -lGIFTAcURL2FTS -lGIFTAcInvertedFile -lGIFTQuInvertedFile\
#	 
#	 -lGIFTAcHierarchy -lGIFTQuHierarchy\
#@PRE_INSTALL_LIBDIRS@  @UNPUBLISHED_DIR@ @BAYESIAN@ @UNPUBLISHED@ -lMRML\
#	 @BAYESIAN_LD_ADD@\
#	 

gift_generate_inverted_file_LDFLAGS = 

# removed ../expat/xmlparse/*.o ../expat/xmltok/*.o

gift_generate_inverted_file_SOURCES=generateInvertedFile.cc 


# change the "endianicity" 
# (useful when exchanging files across a heterogeneous network)
# relies on files consisting of 4-byte-variables only
gift_endianize_SOURCES = endianize.cc

# Generate a distance matrix from a given database
# (this is needed for the scheme in libBayesian.
# we suggest this for research only. it was mainly
# for having a reasonably fast experimental platform
# that I (WM) did this.
# generateDistanceMatrix_SOURCES = generateDistanceMatrix.cc
# generateDistanceMatrix_LDADD = -L../libGIFTInvertedFile/cc -L../libBayesian/cc -lInvertedFile @BAYESIAN@  

# symmetrify raw distance matrix (or things like that)
gift_modify_distance_matrix_SOURCES = modifyDistanceMatrix.cc


# for curing sign (+-) errors in the distance matrix. 
# it reads a sequence of floats and puts out 
# (1-x) for each float x read
# YESSIR, this is a HACK. 
gift_one_minus_SOURCES = oneMinus.cc


#gift_debug_test_SOURCES = gift-debug-test.cc

#gift_debug_test_LDADD = ../expat/xmlparse/*.o ../expat/xmltok/*.o  \
#	-lefence \
#	@PRE_INSTALL_LIBDIRS@ @PRE_INSTALL_LIBDIRS@\
#	@UNPUBLISHED_DIR@ @UNPUBLISHED@ @BAYESIAN@ \
#        -lGIFTQuPerl -lGIFTAcPerl -lMRML\
#	@PERL_LD_ADD@ 


noinst_HEADERS =  CSocket.h CDomainSocket.h CTCPSocket.h CMultiServer.h processMessage.h CProcessMessageParameters.h 