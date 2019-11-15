if GRIDFTP_ENABLED
GRIDFTP_SD = gridftp
endif
if LDAP_ENABLED
LDAP_SD = ldap
endif
if SRM_DMC_ENABLED
SRM_SD=srm
endif
if XROOTD_ENABLED
XROOTD_SD=xrootd
endif
if GFAL_ENABLED
GFAL_SD=gfal
endif
if MOCK_DMC_ENABLED
MOCK_SD=mock
endif
if S3_DMC_ENABLED
 S3_SD=s3
endif

SUBDIRS = http file rucio acix $(LDAP_SD) $(GRIDFTP_SD) $(SRM_SD) $(XROOTD_SD) $(GFAL_SD) $(MOCK_SD) $(S3_SD)
DIST_SUBDIRS = http file rucio acix s3 ldap gridftp srm xrootd gfal mock
