## btscanner - Displays the output of Bluetooth scans
## Copyright (C) 2003 Pentest Limited
## 
## Written 2003 by Tim Hurman <timh at pentest.co.uk>
## 
## This program is free software; you can redistribute it and/or modify
## it under the terms of the GNU General Public License version 2 as
## published by the Free Software Foundation;
## 
## THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
## IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
## FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT OF THIRD PARTY
## RIGHTS.  IN NO EVENT SHALL THE COPYRIGHT HOLDER(S) AND AUTHOR(S) BE LIABLE
## FOR ANY CLAIM, OR ANY SPECIAL INDIRECT OR CONSEQUENTIAL DAMAGES, OR ANY
## DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN
## AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
## OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
## 
## ALL LIABILITY, INCLUDING LIABILITY FOR INFRINGEMENT OF ANY PATENTS,
## COPYRIGHTS, TRADEMARKS OR OTHER RIGHTS, RELATING TO USE OF THIS SOFTWARE
## IS DISCLAIMED.
##

bin_PROGRAMS = btscanner

INCLUDES = -I$(top_srcdir)

btscanner_SOURCES = main.c main.h \
	threader.c threader.h \
	cfg.c cfg.h \
	store.c store.h \
	misc.c misc.h \
	oui.c oui.h \
	screen.c screen.h \
	ll.c ll.h \
	sdp.c sdp.h \
	scan.c scan.h \
	log.c log.h

oui.txt: $(srcdir)/mk_oui_list.pl
	$(PERL) mk_oui_list.pl

sysconf_DATA = btscanner.xml btscanner.dtd
