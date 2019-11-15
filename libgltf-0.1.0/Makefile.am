ACLOCAL_AMFLAGS = -I m4

pkgconfdir = $(libdir)/pkgconfig

pkgconf_DATA = libgltf-@GLTF_MAJOR_VERSION@.@GLTF_MINOR_VERSION@.pc

SUBDIRS = build inc src

if TESTS
SUBDIRS += qa
endif

EXTRA_DIST = \
	AUTHORS \
	COPYING \
	LICENSE \
	NEWS \
	README \
	autogen.sh \
	libgltf.pc.in

distclean-local:
	rm -rf *.cache *~ *.pc

dist-hook:
	git log --date=short --pretty="format:@%cd %an <%ae> [%H]%n%n%s%n%n%e%b" | sed -e "s|^\([^@]\)|\t\1|" -e "s|^@||" >$(distdir)/ChangeLog
