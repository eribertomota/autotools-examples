
info_TEXINFOS = licenseutils.texi

CLEANFILES = *.ps *.html *.dvi *~ licenseutils.pdf gendocs_template licenseutils.fl licenseutils.pg licenseutils.fn licenseutils.toc licenseutils.aux licenseutils.ky licenseutils.tp licenseutils.cp licenseutils.log licenseutils.vr licenseutils.cps licenseutils.op stamp-vti


MAKEINFO = @MAKEINFO@ --no-split --force

EXTRA_DIST=fdl.texi gendocs

manuals: gendocs_template
	${top_builddir}/build-aux/gendocs.sh licenseutils licenseutils

gendocs_template: gendocs
	cp gendocs gendocs_template
