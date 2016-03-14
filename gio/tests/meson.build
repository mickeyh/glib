#  Test programs buildable on all platforms
gio_tests = [
  'appmonitor',
  'async-close-output-stream',
  'async-splice-output-stream',
  'buffered-input-stream',
  'buffered-output-stream',
  'cancellable',
  'contexts',
  'contenttype',
  'converter-stream',
  'credentials',
  'data-input-stream',
  'data-output-stream',
  #'defaultvalue',           # FIXME: needs giotypefuncs.c generated
  'fileattributematcher',
  'filter-streams',
  'giomodule',
  'gsubprocess',
  'g-file',
  'g-file-info',
  'g-icon',
  'gdbus-addresses',
  'gdbus-message',
  'inet-address',
  'io-stream',
  'memory-input-stream',
  'memory-output-stream',
  'monitor',
  'network-address',
  'network-monitor',
  'permission',
  'pollable',
  'proxy-test',
  'readwrite',
  'simple-async-result',
  'simple-proxy',
  'sleepy-stream',
  'socket',
  'socket-listener',
  'socket-service',
  'srvtarget',
  'task',
  'vfs',
  'volumemonitor',
  'glistmodel',
  'testfilemonitor',
]

#if host_machine.system() != 'windows'
#  gio_tests += [ 'unix', 'include' ]
#endif

if cc.get_id() == 'gcc' or cc.get_id() == 'clang'
#  conflicts with glib/tests/autoptr apparently?!
#  gio_tests += [ 'autoptr' ]
endif

test_env = [
  'G_TEST_SRCDIR=' + meson.current_source_dir(),
  'G_TEST_BUILDDIR=' + meson.current_build_dir(),
]

test_c_args = [
  '-DHAVE_CONFIG_H=1',
  '-DG_LOG_DOMAIN="GLib-GIO"',
  '-DTEST_SERVICES="@0@/gio/tests/services"'.format(meson.build_root()),
]

foreach test_name : gio_tests
  exe = executable(test_name, '@0@.c'.format(test_name),
      include_directories : inc_dirs,
      install : false,
      c_args : test_c_args,
      link_with : [ libgio, libgmodule, libglib ],
      dependencies : deps,
  )
  if test_name == 'testfilemonitor'
    test(test_name, exe, env : test_env, timeout : 45)
  else
    test(test_name, exe, env : test_env)
  endif
endforeach

uninstalled_test_extra_programs = [
  'gio-du',
  'echo-server',
  'filter-cat',
  'gapplication-example-actions',
  'gapplication-example-cmdline',
  'gapplication-example-cmdline2',
  'gapplication-example-cmdline3',
  'gapplication-example-dbushooks',
  'gapplication-example-open',
  'gdbus-example-export',
  'gdbus-example-own-name',
  'gdbus-example-peer',
  'gdbus-example-proxy-subclass',
  'gdbus-example-server',
  'gdbus-example-subtree',
  'gdbus-example-watch-name',
  'gdbus-example-watch-proxy',
  'gsubprocess-testprog',
  'httpd',
  'proxy',
  'resolver',
  'send-data',
  'socket-server',
]

foreach extra_program : uninstalled_test_extra_programs
  exe = executable(extra_program, '@0@.c'.format(extra_program),
      include_directories : inc_dirs,
      c_args : test_c_args,
      link_with : [ libgio, libgmodule, libglib ],
      dependencies : deps,
  )
endforeach

foo = '''
c_args_atomic = [ ]
if cc.get_id() == 'gcc'
  c_args_atomic += [ '-Wstrict-aliasing=2' ]
endif

exe = executable('atomic', 'atomic.c',
  include_directories : inc_dirs,
  c_args : [ '-DHAVE_CONFIG_H=1' ] + c_args_atomic,
  link_with : libglib,
  dependencies : deps,
)
test('atomic', exe, env : test_env)

# FIXME: consolidate all of these into the array
exe = executable('overflow-fallback', 'overflow.c',
  include_directories : inc_dirs,
  c_args : [ '-DHAVE_CONFIG_H=1', '-D_GLIB_TEST_OVERFLOW_FALLBACK' ],
  link_with : libglib,
  dependencies : deps,
)
test('overflow-fallback', exe, env : test_env)

exe = executable('642026-ec', '642026.c',
  include_directories : inc_dirs,
  c_args : [ '-DHAVE_CONFIG_H=1', '-DG_ERRORCHECK_MUTEXES' ],
  link_with : libglib,
  dependencies : deps,
)
test('642026-ec', exe, env : test_env)

exe = executable('1bit-emufutex', '1bit-mutex.c',
  include_directories : inc_dirs,
  c_args : [ '-DHAVE_CONFIG_H=1', '-DTEST_EMULATED_FUTEX' ],
  link_with : libglib,
  dependencies : deps,
)
test('1bit-emufutex', exe, env : test_env)

if glib_conf.has('HAVE_EVENTFD')
  exe = executable('gwakeup-fallback', 'gwakeuptest.c', '../gwakeup.c',
    include_directories : inc_dirs,
    c_args : [ '-DHAVE_CONFIG_H=1', '-DTEST_EVENTFD_FALLBACK' ],
    link_with : libglib,
    dependencies : deps,
  )
  test('gwakeup-fallback', exe, env : test_env)
endif

# test-spawn-echo helper binary required by the spawn tests
executable('test-spawn-echo', 'test-spawn-echo.c',
           include_directories : inc_dirs,
           c_args : [ '-DHAVE_CONFIG_H=1', '-DG_LOG_DOMAIN="GLib"' ],
           link_with : libglib,
           dependencies : deps,
)
'''

subdir('modules')
