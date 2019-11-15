SUBDIRS = config src 
ACLOCAL_AMFLAGS = -I m4
EXTRA_DIST = autogen.sh LICENSE

rpmbuild_dir=@WORKDIR@/rpmbuild
debbuild_dir=@WORKDIR@/debbuild

spec=spec/voms-mysql-plugin.spec
rpmdist=""

stage_dir=dist

distsrc: dist
	mv $(distdir).tar.gz $(DISTTAR)/$(distdir)_src.tar.gz

distclean-local:
	rm -f configure aclocal.m4 $(distdir).tar.gz
	rm -f m4/libtool.m4 m4/ltoptions.m4 m4/ltsugar.m4 m4/ltversion.m4 m4/lt~obsolete.m4
	rm -rf autom4te.cache aux src/autogen $(rpmbuild_dir) $(debbuild_dir)
	find . -name Makefile.in -exec rm {} \;

clean-local:
	rm -rf $(rpmbuild_dir) $(debbuild_dir) $(distdir).tar.gz dist

rpm: dist
	mkdir -p $(rpmbuild_dir)/BUILD $(rpmbuild_dir)/RPMS $(rpmbuild_dir)/SOURCES $(rpmbuild_dir)/SPECS $(rpmbuild_dir)/SRPMS
	cp $(distdir).tar.gz $(rpmbuild_dir)/SOURCES
	rpmbuild --nodeps -v -ba $(spec) --define "_topdir $(rpmbuild_dir)" --define "dist $(rpmdist)"

stage:
	mkdir -p $(stage_dir)
	
	for r in $(shell find $(rpmbuild_dir)/RPMS -name '*.rpm') ; do \
		echo "Istalling `basename $$r` in $(stage_dir)..."; \
		pushd . ; cp $$r $(stage_dir); cd $(stage_dir); \
		rpm2cpio `basename $$r` | cpio -idm; \
		rm `basename $$r`; popd; \
	done

etics: clean rpm 
	mkdir -p tgz RPMS
	cp $(distdir).tar.gz tgz
	cp -r $(rpmbuild_dir)/RPMS/* $(rpmbuild_dir)/SRPMS/* RPMS
