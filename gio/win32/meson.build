giowin32_sources = [
  'gwin32fsmonitorutils.c',
  'gwin32filemonitor.c',
  'gwinhttpvfs.c',
  'gwinhttpfile.c',
  'gwinhttpfileinputstream.c',
  'gwinhttpfileoutputstream.c',
]

giowin32_lib = static_library('giowin32',
  sources : [giowin32_sources, gioenumtypes_h],
  include_directories : [configinc, glibinc, gioinc, gmoduleinc],
  pic : true,
  c_args : [ '-DHAVE_CONFIG_H', '-DG_DISABLE_DEPRECATED' ] + gio_c_args)
