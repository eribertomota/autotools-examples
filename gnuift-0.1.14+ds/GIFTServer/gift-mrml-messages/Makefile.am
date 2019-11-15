data_DATA= gift-ihandshake.mrml gift-iconfigure.mrml

#MRMLCONFIG=sed "s:__DATADIR__:@datadir@:g" < $< > $@
MRMLCONFIG=sed "s:__EXECBINDIR__:@DEBEXECBINDIR@:g;s:__PERL_LOCATION__:@PERL@:g;s:__BINDIR__:@DEBPERLLIBDIR@:g;s:__DATADIR__:@DEBDATADIR@:g;s:__LIBDIR__:@DEBSHAREDIR@:g;s:__HOME__:${HOME}:g;s:__WEB_PUBLISHING_DIRECTORY__:@WEB_PUBLISHING_DIRECTORY@:g;s=__WEB_PUBLISHING_LOCATION__=@WEB_PUBLISHING_LOCATION@=g;" < $< > $@
 

EXTRA_DIST= gift-ihandshake.pre-mrml gift-iconfigure.pre-mrml	

gift-ihandshake.mrml:gift-ihandshake.pre-mrml
	$(MRMLCONFIG)

gift-iconfigure.mrml:gift-iconfigure.pre-mrml	
	$(MRMLCONFIG)
