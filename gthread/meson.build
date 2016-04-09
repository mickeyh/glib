# Just a skeleton lib for backwards compatibility since all the functionaliy
# has been moved into glib now
libgthread = shared_library('gthread',
  sources : [ 'gthread-impl.c' ],
  version : glib_version,
  soversion : interface_version,
  install : true,
  dependencies : [libglib_dep],
  c_args : ['-DG_LOG_DOMAIN="GThread"' ],
)
