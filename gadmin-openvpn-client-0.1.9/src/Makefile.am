## Process this file with automake to produce Makefile.in

INCLUDES = \
	-DPACKAGE_DATA_DIR=\""$(datadir)"\" \
	-DPACKAGE_LOCALE_DIR=\""$(prefix)/$(DATADIRNAME)/locale"\" \
	@PACKAGE_CFLAGS@

sbin_PROGRAMS = gadmin-openvpn-client

gadmin_openvpn_client_SOURCES = \
	gadmin-openvpn.c gadmin-openvpn.h \
	populate_gadmin_openvpn.c populate_gadmin_openvpn.h \
	widgets.c widgets.h \
	support.c support.h \
	create_main_window.c create_main_window.h \
	create_client_tab.c create_client_tab.h \
	create_client_settings.c create_client_settings.h \
	populate_client_settings.c populate_client_settings.h \
	apply_client_settings.c apply_client_settings.h \
	make_settings_entries.c make_settings_entries.h \
	make_settings_combos.c make_settings_combos.h \
	make_settings_spinbuttons.c make_settings_spinbuttons.h \
	make_settings_buttons.c make_settings_buttons.h \
	make_settings_checkbuttons.c make_settings_checkbuttons.h \
	make_settings_progressbars.c make_settings_progressbars.h \
	make_settings_labels.c make_settings_labels.h \
	make_settings_hseparators.c make_settings_hseparators.h \
	status_update.c status_update.h \
	create_log_tab.c create_log_tab.h \
	populate_log_tab.c populate_log_tab.h \
	clear_log_tab.c clear_log_tab.h \
	create_conf_tab.c create_conf_tab.h \
	populate_conf_tab.c populate_conf_tab.h \
	save_conf_tab.c save_conf_tab.h \
	set_version.c set_version.h \
	apply_button_clicked.c apply_button_clicked.h \
	delete_connection_clicked.c delete_connection_clicked.h \
	commands.c commands.h \
	functions.c functions.h \
	credits_window.c credits_window.h \
	activate_button_clicked.c activate_button_clicked.h \
	deactivate_button_clicked.c deactivate_button_clicked.h \
	show_info.c show_info.h \
	file_chooser.c file_chooser.h \
	show_import_window.c show_import_window.h \
	allocate.c allocate.h \
	show_help.c show_help.h

gadmin_openvpn_client_LDADD = @PACKAGE_LIBS@
