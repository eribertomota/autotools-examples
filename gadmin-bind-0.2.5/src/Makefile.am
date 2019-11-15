## Process this file with automake to produce Makefile.in

INCLUDES = \
	-DPACKAGE_DATA_DIR=\""$(datadir)"\" \
	-DPACKAGE_LOCALE_DIR=\""$(prefix)/$(DATADIRNAME)/locale"\" \
	@PACKAGE_CFLAGS@

sbin_PROGRAMS = gadmin-bind

gadmin_bind_SOURCES = \
	widgets.c widgets.h \
	gadmin-bind.c gadmin-bind.h \
	create_main_window.c create_main_window.h \
	create_domain_tab.c create_domain_tab.h \
	populate_domain_treeview.c populate_domain_treeview.h \
	domain_treeview_row_clicked.c domain_treeview_row_clicked.h \
	add_domain.c add_domain.h \
	delete_domain.c delete_domain.h \
	delete_domain_from_btn.c delete_domain_from_btn.h \
	populate_resource_treeview.c populate_resource_treeview.h \
	resource_treeview_row_clicked.c resource_treeview_row_clicked.h \
	resource_combo_changed.c resource_combo_changed.h \
	add_resource.c add_resource.h \
	delete_resource.c delete_resource.h \
	delete_resource_from_btn.c delete_resource_from_btn.h \
	domain_settings_window.c domain_settings_window.h \
	domain_settings_type_combo_changed.c domain_settings_type_combo_changed.h \
	settings_window.c settings_window.h \
	credits_window.c credits_window.h \
	activate_button_clicked.c activate_button_clicked.h \
	dialog_if_files_missing.c dialog_if_files_missing.h \
	functions.c functions.h \
	ip_handling.c ip_handling.h \
	reverse_address.c reverse_address.h \
	commented.c commented.h \
	add_standard_user.c add_standard_user.h \
	add_configuration_dialog.c add_configuration_dialog.h \
	add_configuration.c add_configuration.h \
	add_configuration_canceled.c add_configuration_canceled.h \
	clear_log_tab.c clear_log_tab.h \
	create_log_tab.c create_log_tab.h \
	create_verify_tab.c create_verify_tab.h \
	run_verify_cmd.c run_verify_cmd.h \
	create_root_servers_tab.c create_root_servers_tab.h \
	create_resolvers_tab.c create_resolvers_tab.h \
	populate_resolvers.c populate_resolvers.h \
	save_resolvers.c save_resolvers.h \
	populate_root_servers_tab.c populate_root_servers_tab.h \
	update_root_servers.c update_root_servers.h \
	save_root_servers.c save_root_servers.h \
	select_first_domain.c select_first_domain.h \
	select_first_resource.c select_first_resource.h \
	deactivate_button_clicked.c deactivate_button_clicked.h \
	populate_log_tab.c populate_log_tab.h \
	reread_button_clicked.c reread_button_clicked.h \
	reread_conf.c reread_conf.h \
	set_version.c set_version.h \
	show_help.c show_help.h \
	show_info.c show_info.h \
	status_update.c status_update.h \
	new_rndc_key.c new_rndc_key.h \
	load_settings.c load_settings.h \
	save_settings.c save_settings.h \
	locate_icons.c locate_icons.h \
	commands.c commands.h \
	rndc_reload.c rndc_reload.h \
	allocate.c allocate.h \
	chars_are_digits.c chars_are_digits.h \
	make_settings_entries.c make_settings_entries.h \
	make_settings_combos.c make_settings_combos.h \
	make_settings_buttons.c make_settings_buttons.h

gadmin_bind_LDADD = @PACKAGE_LIBS@
