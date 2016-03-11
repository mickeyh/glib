gobject_tests = [
  'qdata',
  'boxed',
  'enums',
  'param',
  'threadtests',
  'dynamictests',
  'binding',
  'properties',
  'reference',
  'value',
  'type',
  'private',
  'closure',
  'object',
  'signal-handler',
  'ifaceproperties',
]

test_env = [
  'G_TEST_SRCDIR=' + meson.current_source_dir(),
  'G_TEST_BUILDDIR=' + meson.current_build_dir(),
]

foreach test_name : gobject_tests
  deps = [ libm, thread_dep ]
  test_src = '@0@.c'.format(test_name)
  # private is an existing or reserved target it seems
  if test_name == 'private'
    test_name = 'gobject-private'
  endif
  exe = executable(test_name, test_src,
      include_directories : inc_dirs,
      c_args : [ '-DHAVE_CONFIG_H=1', '-DG_LOG_DOMAIN="GLib-GObject"' ],
      link_with : [ libglib, libgobject ],
      dependencies : deps,
  )
  test(test_name, exe, env : test_env)
endforeach
