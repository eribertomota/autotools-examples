if XMLSEC_ENABLED
XMLSEC_DIR = xmlsec
else
XMLSEC_DIR =
endif

if GLOBUSUTILS_ENABLED
GLOBUSUTILS_DIR = globusutils
else
GLOBUSUTILS_DIR =
endif

# order is important!
SUBDIRS = common loader message crypto cryptomod \
	credential credentialmod data security \
	ws-addressing $(XMLSEC_DIR) ws-security delegation \
	communication compute infosys $(GLOBUSUTILS_DIR) \
	credentialstore scitokens
DIST_SUBDIRS = common loader message crypto cryptomod \
	credential credentialmod data security \
	ws-addressing xmlsec ws-security delegation \
	communication compute infosys globusutils \
	credentialstore scitokens
