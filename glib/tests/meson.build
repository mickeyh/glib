glib_tests = [
  'array-test',
  'asyncqueue',
  'base64',
  'bitlock',
  'bookmarkfile',
  'bytes',
  'cache',
  'checksum',
  'collate',
  'cond',
  'convert',
  'dataset',
  'date',
  'dir',
  'environment',
  'error',
  'fileutils',
  'gdatetime',
  'gvariant',
  'hash',
  'hmac',
  'hook',
  'hostutils',
  'keyfile',
  'list',
  'logging',
  'mainloop',
  'mappedfile',
  'markup',
  'markup-parse',
  'markup-collect',
  'markup-escape',
  'markup-subparser',
  'mem-overflow',
  'mutex',
  'node',
  'once',
  'option-context',
  'option-argv0',
  'overflow',
#  'overflow-fallback', # FIXME
  'pattern',
  'private',
  'protocol',
  'queue',
  'rand',
  'rec-mutex',
  'regex',
  'rwlock',
  'scannerapi',
  'search-utils',
  'sequence',
  'shell',
  'slice',
  'slist',
  'sort',
  'spawn-multithreaded',
  'spawn-singlethread',
  'strfuncs',
  'string',
  'testing',
  'test-printf',
  'thread',
  'timeout',
  'timer',
  'tree',
  'utf8-performance',
  'utf8-pointer',
  'utf8-validate',
  'utf8-misc',
  'utils',
  'unicode',
  'uri',
  '1bit-mutex',
  '642026',
]

test_env = [
  'G_TEST_SRCDIR=' + meson.current_source_dir(),
  'G_TEST_BUILDDIR=' + meson.current_build_dir(),
]

foreach test_name : glib_tests
  deps = [ libm, thread_dep ]
  if test_name == 'regex'
    deps += [ pcre ]
  endif
  exe = executable(test_name, '@0@.c'.format(test_name),
      include_directories : inc_dirs,
      c_args : [ '-DHAVE_CONFIG_H=1', '-DG_LOG_DOMAIN="GLib"' ],
      link_with : libglib,
      dependencies : deps,
  )
  test(test_name, exe, env : test_env)
endforeach

c_args_atomic = [ ]
if cc.get_id() == 'gcc'
  c_args_atomic += [ '-Wstrict-aliasing=2' ]
endif
test('atomic', executable('atomic', 'atomic.c',
                          include_directories : inc_dirs,
                          c_args : [ '-DHAVE_CONFIG_H=1' ] + c_args_atomic,
                          link_with : libglib,
                          dependencies : deps),
      env : test_env)

# test-spawn-echo helper binary required by the spawn tests
executable('test-spawn-echo', 'test-spawn-echo.c',
           include_directories : inc_dirs,
           c_args : [ '-DHAVE_CONFIG_H=1', '-DG_LOG_DOMAIN="GLib"' ],
           link_with : libglib,
           dependencies : deps,
)
