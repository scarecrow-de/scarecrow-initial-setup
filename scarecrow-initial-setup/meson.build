sources = []

subdir('pages')

resources = gnome.compile_resources(
    'scis-assistant-resources',
    files('scis-assistant.gresource.xml'),
    c_name: 'gis_assistant'
)

sources += [
    resources,
    'cc-common-language.c',
    'scarecrow-initial-setup.c',
    'scis-assistant.c',
    'scis-page.c',
    'scis-page-header.c',
    'scis-driver.c',
    'scis-keyring.c',
    'scarecrow-initial-setup.h',
    'scis-assistant.h',
    'scis-page.h',
    'scis-page-header.h',
    'scis-driver.h',
    'scis-keyring.h'
]

dependencies = [
    dependency ('libnm', version: '>= 1.2'),
    dependency ('libnma', version: '>= 1.0'),
    dependency ('polkit-gobject-1', version: '>= 0.103'),
    dependency ('accountsservice'),
    dependency ('scarecrow-desktop-3.0', version: '>= 3.7.5'),
    dependency ('scarecrow-gsettings-desktop-schemas', version: '>= 3.37.1'),
    dependency ('fontconfig'),
    dependency ('gweather4'),
    dependency ('goa-1.0'),
    dependency ('goa-backend-1.0'),
    dependency ('gtk+-3.0', version: '>= 3.11.3'),
    dependency ('glib-2.0', version: '>= 2.63.1'),
    dependency ('gio-unix-2.0', version: '>= 2.53.0'),
    dependency ('scdm', version: '>= 3.8.3'),
    dependency ('geocode-glib-2.0'),
    dependency ('libgeoclue-2.0', version: '>= 2.3.1'),
    cc.find_library('m', required: false),
    dependency ('pango', version: '>= 1.32.5'),
    dependency ('rest-1.0'),
    dependency ('json-glib-1.0'),
    dependency ('krb5'),
    dependency ('libsecret-1', version: '>= 0.18.8'),
    dependency ('pwquality'),
    dependency ('webkit2gtk-4.0', version: '>= 2.26.0'),
    cheese_dep,
    cheese_gtk_dep,
    ibus_dep,
    libmalcontent_dep,
    libmalcontent_ui_dep,
]

executable(
    'scarecrow-initial-setup',
    sources,
    include_directories: config_h_dir,
    dependencies: dependencies,
    install: true,
    install_dir: get_option('libexecdir')
)

executable(
    'scarecrow-initial-setup-copy-worker',
    ['scarecrow-initial-setup-copy-worker.c'],
    include_directories: config_h_dir,
    dependencies: dependencies,
    install: true,
    install_dir: get_option('libexecdir')
)
