TEXI_XML = ./texi_xml
EXTRA_DIST = README liece.xml liece.info
DISTCLEANFILES = liece.info
CLEANFILES = *~

SUFFIXES = .xml .txml .texi .info

DOCBOOK2TEXIXSLT_DIR = xslt/texi
SAXON = java -classpath $(CLASSPATH):$(DOCBOOK2TEXIXSLT_DIR) com.icl.saxon.StyleSheet

all: liece.info

%.txml: %.xml
	$(SAXON) -o $@ $*.xml $(DOCBOOK2TEXIXSLT_DIR)/docbook.xsl

%.texi:	%.txml
	$(TEXI_XML) $*.txml
	-recode -df utf8..texi < $@ > tmp
	mv tmp $@

