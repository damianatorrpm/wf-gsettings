project('wf-gsettings', ['cpp'], version: '0.0.1', license: 'Unlicense',
	default_options: ['cpp_std=c++17', 'warning_level=2'])

wayfire = dependency('wayfire')
wlroots = dependency('wlroots', fallback: ['wlroots', 'wlroots'])
gio = dependency('gio-2.0')
gnome = import('gnome')

plugin_gsettings = shared_module('gsettings', 'gsettings.cpp',
	dependencies: [wayfire, wlroots, gio],
	install: true,
	install_dir: 'get_option('datadir')/wayfire')

script = custom_target(
	'wf-gsettings-gen-schemas',
	input: ['wf-gsettings-gen-schemas.in'],
	output: ['wf-gsettings-gen-schemas'],
	capture: true,
	command: ['sed', '-e', 's|@PREFIX@|' + get_option('prefix') + '|', '@INPUT@'],
	install: true,
	install_mode: 'rwxr-xr-x',
	install_dir: 'bin')

install_data('genschema.xsl', install_dir: 'share/wf-gsettings')
install_data('org.wayfire.gsettings.gschema.xml', install_dir: 'share/glib-2.0/schemas')
