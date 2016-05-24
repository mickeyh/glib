gdbus_codegen_files = [
  '__init__.py',
  'codegen.py',
  'codegen_main.py',
  'codegen_docbook.py',
  'dbustypes.py',
  'parser.py',
  'utils.py',
]

gdbus_codegen_conf = configuration_data()
gdbus_codegen_conf.set('abs_top_srcdir', meson.source_root())
gdbus_codegen_conf.set('abs_top_builddir', meson.build_root())
gdbus_codegen_conf.set('prefix', glib_prefix)
gdbus_codegen_conf.set('datadir', glib_datadir)
gdbus_codegen_conf.set('datarootdir', glib_datadir)
gdbus_codegen_conf.set('VERSION', glib_version)
gdbus_codegen_conf.set('PYTHON', python.path())

# Install gdbus-codegen executable
# FIXME: Set permissions
gdbus_codegen = configure_file(input : 'gdbus-codegen.in',
  output : 'gdbus-codegen',
  install : true,
  install_dir : 'bin', configuration : gdbus_codegen_conf)

configure_file(input : 'config.py.in',
  output : 'config.py',
  install : true,
  install_dir : 'share/glib-2.0/codegen', configuration : gdbus_codegen_conf)

install_data(gdbus_codegen_files, install_dir : 'share/glib-2.0/codegen')
