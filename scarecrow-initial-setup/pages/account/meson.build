realmd_namespace = 'org.freedesktop.realmd'
sources += gnome.gdbus_codegen(
  'um-realm-generated',
  realmd_namespace + '.xml',
  interface_prefix: realmd_namespace + '.',
  namespace: 'UmRealm',
  object_manager: true,
  annotations: ['org.freedesktop.realmd.Realm', 'org.gtk.GDBus.C.Name', 'Common']
)

sources += gnome.compile_resources(
   'account-resources',
   files('account.gresource.xml'),
   c_name: 'account'
)

sources += files(
    'scis-account-page.c',
    'scis-account-page.h',
    'scis-account-pages.c',
    'scis-account-pages.h',
    'scis-account-page-local.c',
    'scis-account-page-local.h',
    'scis-account-page-enterprise.c',
    'scis-account-page-enterprise.h',
    'um-realm-manager.c',
    'um-realm-manager.h',
    'um-utils.c',
    'um-photo-dialog.c',
    'um-photo-dialog.h'
)

account_sources_dir = meson.current_source_dir()
