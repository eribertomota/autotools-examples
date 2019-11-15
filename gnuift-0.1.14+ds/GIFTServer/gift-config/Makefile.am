#MRMLCONFIG=sed "s:__PERL_LOCATION__:@PERL@:g;s:__BINDIR__:@bindir@:g;s:__DATADIR__:@datadir@:g;s:__HOME__:${HOME}:g" < $< > $@
MRMLCONFIG=sed "s:__EXECBINDIR__:@DEBEXECBINDIR@:g;s:__PERL_LOCATION__:@PERL@:g;s:__BINDIR__:@DEBPERLLIBDIR@:g;s:__DATADIR__:@DEBDATADIR@:g;s:__LIBDIR__:@DEBSHAREDIR@:g;s:__HOME__:${HOME}:g;s:__WEB_PUBLISHING_DIRECTORY__:@WEB_PUBLISHING_DIRECTORY@:g;s=__WEB_PUBLISHING_LOCATION__=@WEB_PUBLISHING_LOCATION@=g;" < $< > $@
 
EXTRA_DIST=gift-config.pre-mrml

data_DATA= gift-config.mrml 

gift-config.mrml: gift-config.pre-mrml
	$(MRMLCONFIG)

CLEANFILES= gift-config.mrml