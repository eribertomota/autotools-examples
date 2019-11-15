install-redhat:
	$(INSTALL_SCRIPT) cpqarrayd /etc/rc.d/init.d
	$(INSTALL_SCRIPT) cpqarrayd.sysconfig /etc/sysconfig/cpqarrayd
	/sbin/chkconfig --add cpqarrayd

uninstall-redhat:
	/sbin/chkconfig --del cpqarrayd
	rm -f /etc/rc.d/init.d/cpqarrayd
	rm -f /etc/sysconfig/cpqarrayd
