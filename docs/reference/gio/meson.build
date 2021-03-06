if get_option('with-docs')
  subdir('xml')

  ignore_headers = [
    'fam',
    'fen',
    'gdbus-2.0',
    'gvdb',
    'inotify',
    'kqueue',
    'libasyncns',
    'tests',
    'win32',
    'xdgmime',
    'gappinfoprivate.h',
    'gapplicationimpl.h',
    'gasynchelper.h',
    'gcontenttypeprivate.h',
    'gcontextspecificgroup.h',
    'gcredentialsprivate.h',
    'gdbus-daemon-generated.h',
    'gdbusactiongroup-private.h',
    'gdbusauth.h',
    'gdbusauthmechanismanon.h',
    'gdbusauthmechanismexternal.h',
    'gdbusauthmechanism.h',
    'gdbusauthmechanismsha1.h',
    'gdbusdaemon.h',
    'gdbusprivate.h',
    'gdelayedsettingsbackend.h',
    'gdummyfile.h',
    'gdummyproxyresolver.h',
    'gdummytlsbackend.h',
    'gfileattribute-priv.h',
    'gfileinfo-priv.h',
    'ghttpproxy.h',
    'giomodule-priv.h',
    'gioprivate.h',
    'giowin32-priv.h',
    'glocaldirectorymonitor.h',
    'glocalfileenumerator.h',
    'glocalfile.h',
    'glocalfileinfo.h',
    'glocalfileinputstream.h',
    'glocalfileiostream.h',
    'glocalfilemonitor.h',
    'glocalfileoutputstream.h',
    'glocalvfs.h',
    'gmountprivate.h',
    'gnativevolumemonitor.h',
    'gnetworkingprivate.h',
    'gnetworkmonitorbase.h',
    'gnetworkmonitornetlink.h',
    'gnetworkmonitornm.h',
    'gnotificationbackend.h',
    'gnotification-private.h',
    'gpollfilemonitor.h',
    'gregistrysettingsbackend.h',
    'gresourcefile.h',
    'gsettingsbackendinternal.h',
    'gsettings-mapping.h',
    'gsettingsschema-internal.h',
    'gsocketinputstream.h',
    'gsocketoutputstream.h',
    'gsocks4aproxy.h',
    'gsocks4proxy.h',
    'gsocks5proxy.h',
    'gsubprocesslauncher-private.h',
    'gthreadedresolver.h',
    'gunionvolumemonitor.h',
    'gunixmount.h',
    'gunixresolver.h',
    'gunixvolume.h',
    'gunixvolumemonitor.h',
    'gwin32appinfo.h',
    'gwin32inputstream.h',
    'gwin32mount.h',
    'gwin32outputstream.h',
    'gwin32registrykey.h',
    'gwin32resolver.h',
    'gwin32volumemonitor.h',
    'thumbnail-verify.h',
    'xdp-dbus.h',
  ]
  # FIXME: More win32 headers were added to fix building gio-scan

  # FIXME: ExampleAnimal docs aren't built

  docpath = join_paths(glib_datadir, 'gtk-doc', 'html')
  version_conf = configuration_data()
  version_conf.set('VERSION', meson.project_version())
  configure_file(
    input: 'version.xml.in',
    output: 'version.xml',
    configuration: version_conf
  )

  gnome.gtkdoc('gio',
    main_xml : 'gio-docs.xml',
    namespace : 'g',
    gobject_typesfile : 'gio.types',
    mode : 'none',
    dependencies : [libgio_dep, libgobject_dep, libglib_dep],
    src_dir : 'gio',
    scan_args : [
      '--rebuild-types',
      '--deprecated-guards=G_DISABLE_DEPRECATED',
      '--ignore-decorators=G_GNUC_WARN_UNUSED_RESULT',
      '--ignore-headers=' + ' '.join(ignore_headers),
    ],
    content_files : [
      'overview.xml',
      'migrating-posix.xml',
      'migrating-gnome-vfs.xml',
      'migrating-gconf.xml',
      'migrating-gdbus.xml',
      'gio-querymodules.xml',
      'glib-compile-schemas.xml',
      'glib-compile-resources.xml',
      'gapplication.xml',
      'gsettings.xml',
      'gresource.xml',
      'gdbus.xml',
      'gdbus-codegen.xml',
    ],
    expand_content_files : [
      'overview.xml',
      'migrating-posix.xml',
      'migrating-gnome-vfs.xml',
      'migrating-gconf.xml',
      'migrating-gdbus.xml',
      'gdbus-codegen.xml',
    ],
    html_assets : [
      'gvfs-overview.png',
      'menu-example.png',
      'menu-model.png',
    ],
    fixxref_args: [
      '--html-dir=' + docpath,
      '--extra-dir=' + join_paths(meson.current_build_dir(), '../glib/html'),
      '--extra-dir=' + join_paths(meson.current_build_dir(), '../gobject/html'),
    ],
    install: true
  )
endif


if get_option('with-man')
  custom_target('gapplication-man',
    input: 'gapplication.xml',
    output: 'gapplication.1',
    command: xsltproc_command,
    install: true,
    install_dir: man1_dir,
  )

  custom_target('gio-querymodules-man',
    input: 'gio-querymodules.xml',
    output: 'gio-querymodules.1',
    command: xsltproc_command,
    install: true,
    install_dir: man1_dir,
  )

  custom_target('glib-compile-schemas-man',
    input: 'glib-compile-schemas.xml',
    output: 'glib-compile-schemas.1',
    command: xsltproc_command,
    install: true,
    install_dir: man1_dir,
  )

  custom_target('glib-compile-resources-man',
    input: 'glib-compile-resources.xml',
    output: 'glib-compile-resources.1',
    command: xsltproc_command,
    install: true,
    install_dir: man1_dir,
  )

  custom_target('gsettings-man',
    input: 'gsettings.xml',
    output: 'gsettings.1',
    command: xsltproc_command,
    install: true,
    install_dir: man1_dir,
  )

  custom_target('gresource-man',
    input: 'gresource.xml',
    output: 'gresource.1',
    command: xsltproc_command,
    install: true,
    install_dir: man1_dir,
  )

  custom_target('gdbus-man',
    input: 'gdbus.xml',
    output: 'gdbus.1',
    command: xsltproc_command,
    install: true,
    install_dir: man1_dir,
  )

  custom_target('gio',
    input: 'gio.xml',
    output: 'gio.1',
    command: xsltproc_command,
    install: true,
    install_dir: man1_dir,
  )

  custom_target('gdbus-codegen-man',
    input: 'gdbus-codegen.xml',
    output: 'gdbus-codegen.1',
    command: xsltproc_command,
    install: true,
    install_dir: man1_dir,
  )
endif
