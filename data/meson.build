autostart_files = [
    'scarecrow-initial-setup-copy-worker.desktop',
    'scarecrow-initial-setup-first-login.desktop',
    'scarecrow-welcome-tour.desktop'
]

gis_shell_component = 'io.github.scarecrow_de.Shell'
gis_scarecrow_session_required_components = [
    'io.github.scarecrow_de.SettingsDaemon.A11ySettings',
    'io.github.scarecrow_de.SettingsDaemon.Color',
    'io.github.scarecrow_de.SettingsDaemon.Datetime',
    'io.github.scarecrow_de.SettingsDaemon.Housekeeping',
    'io.github.scarecrow_de.SettingsDaemon.Keyboard',
    'io.github.scarecrow_de.SettingsDaemon.MediaKeys',
    'io.github.scarecrow_de.SettingsDaemon.Power',
    'io.github.scarecrow_de.SettingsDaemon.PrintNotifications',
    'io.github.scarecrow_de.SettingsDaemon.Rfkill',
    'io.github.scarecrow_de.SettingsDaemon.ScreensaverProxy',
    'io.github.scarecrow_de.SettingsDaemon.Sharing',
#    'io.github.scarecrow_de.SettingsDaemon.Smartcard',
    'io.github.scarecrow_de.SettingsDaemon.Sound',
    'io.github.scarecrow_de.SettingsDaemon.UsbProtection',
    'io.github.scarecrow_de.SettingsDaemon.Wacom',
    'io.github.scarecrow_de.SettingsDaemon.XSettings',
]

gis_user_session_wanted_components = gis_scarecrow_session_required_components

desktop_conf = configuration_data()
desktop_conf.set('LIBEXECDIR', libexec_dir)
desktop_conf.set('systemd_hidden', enable_systemd ? 'true' : 'false')

foreach desktop_file: autostart_files
    i18n.merge_file(
        'desktop',
        input: configure_file(
            input: files(desktop_file + '.in.in'),
            output: desktop_file + '.in',
            configuration: desktop_conf
        ),
        output: desktop_file,
        install_dir: join_paths(get_option('sysconfdir'), 'xdg', 'autostart'),
        po_dir: po_dir,
        install: true,
        type: 'desktop'
    )
endforeach

i18n.merge_file(
    'desktop',
    input: configure_file(
        input: files('scarecrow-initial-setup.desktop.in.in'),
        output: 'scarecrow-initial-setup.desktop.in',
        configuration: desktop_conf
    ),
    output: 'scarecrow-initial-setup.desktop',
    install_dir: join_paths(data_dir, 'scdm', 'greeter', 'applications'),
    po_dir: po_dir,
    install: true,
    type: 'desktop'
)

if enable_systemd
    unitconf = configuration_data()
    unitconf.set('libexecdir', libexec_dir)

    unit_files = {
        'scarecrow-initial-setup-first-login.service' : [ 'scarecrow-session.target.wants/' ],
        'scarecrow-initial-setup-copy-worker.service' : [ 'scarecrow-session.target.wants/' ],
        'scarecrow-welcome-tour.service' : [ 'scarecrow-session.target.wants/' ],
    }

    foreach unit, wants: unit_files
        configure_file(
            input: unit + '.in',
            output: unit,
            configuration: unitconf,
            install_dir: systemd_userunitdir
        )

        foreach target: wants
            meson.add_install_script('meson-add-wants.sh', systemd_userunitdir, target, unit)
        endforeach
    endforeach

    gis_user_session_wanted_targets = []
    foreach component: gis_user_session_wanted_components
        gis_user_session_wanted_targets += 'Wants=@0@.target'.format(component)
    endforeach

    configure_file(
        input: '@0@.session.conf.in'.format(meson.project_name()),
        output: 'session.conf',
        configuration: {
            'this_component': meson.project_name(),
            'requires_component': gis_shell_component,
            'wants_required_components': '\n'.join(
                gis_user_session_wanted_targets),
        },
        install_dir: systemd_userunitdir / 'scarecrow-session@@0@.target.d'.format(
            meson.project_name()),
    )
endif


rules_dir = join_paths(data_dir, 'polkit-1', 'rules.d')
install_data('20-scarecrow-initial-setup.rules', install_dir: rules_dir)

session_dir = join_paths(data_dir, 'scarecrow-session', 'sessions')
configure_file(
  input: '@0@.session.in'.format(meson.project_name()),
  output: '@BASENAME@',
  configuration: {
    'this_component': meson.project_name(),
    'scarecrow_session_required_components': ';'.join([
        gis_shell_component,
        meson.project_name(),
      ] +
      gis_scarecrow_session_required_components),
  },
  install_dir: session_dir,
)

mode_dir = join_paths(data_dir, 'scarecrow-shell', 'modes')
install_data('initial-setup.json', install_dir: mode_dir)

install_data('scarecrow-welcome-tour', install_dir: get_option('libexecdir'))
