sources += gnome.gdbus_codegen(
  'timedated',
  'timedated1-interface.xml',
  interface_prefix: 'org.freedesktop.',
)

sources += gnome.compile_resources(
    'cc-datetime-resources',
    files('datetime.gresource.xml'),
    c_name: 'datetime'
)

sources += gnome.compile_resources(
    'timezone-resources',
    files('timezone.gresource.xml'),
    c_name: 'timezone'
)

sources += files(
    'cc-timezone-map.c',
    'cc-timezone-map.h',
    'tz.c',
    'tz.h',
    'scis-bubble-widget.c',
    'scis-bubble-widget.h',
    'scis-timezone-page.c',
    'scis-timezone-page.h'
)
