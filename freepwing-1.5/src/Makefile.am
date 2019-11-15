pkgperllibdir = ${perllibdir}/FreePWING

pkgperllib_DATA = BaseText.pm BaseUserChar.pm BaseWord.pm CharConv.pm \
	ColorGraphic.pm Control.pm EndWord.pm FullUserChar.pm \
	HalfUserChar.pm Heading.pm Index.pm KeyWord.pm Link.pm RefSound.pm \
	RefUserChar.pm Reference.pm Sort.pm Sound.pm Tag.pm Text.pm \
	Word.pm Word2.pm

EXTRA_DIST = BaseText.pm BaseUserChar.pm BaseWord.pm CharConv.pm \
	ColorGraphic.pm Control.pm EndWord.pm FullUserChar.pm \
	HalfUserChar.pm Heading.pm Index.pm KeyWord.pm Link.pm RefSound.pm \
	RefUserChar.pm Reference.pm Sort.pm.in Sound.pm Tag.pm Text.pm \
	Word.pm Word2.pm

CLEANFILES = Sort.pm

Sort.pm: Sort.pm.in
	rm -f $@
	sed -e 's;\@SORT\@;$(SORT);' $(srcdir)/$@.in > $@.tmp
	cp $@.tmp $@
	chmod 644 $@
	rm -f $@.tmp
