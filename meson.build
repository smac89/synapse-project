project('synapse project', 'vala', 'c',
    license: ['GPL2', 'LGPL2.1'],
    meson_version: '>=0.47.2',
    version: '0.4.7'
)

# Configuration file
conf = configuration_data()

glib_version      = '>=2.40.0'
gtk_version       = '>=3.0.0'
gee_version       = '>=0.5.2'
json_version      = '>=0.10.0'
zeitgeist_version = '>=0.9.14'

# dependencies
dependencies = [
    dependency('glib-2.0', version: glib_version),
    dependency('gdk-x11-3.0', version: gtk_version),
    dependency('gtk+-3.0', version: gtk_version),
    dependency('gio-2.0', version: glib_version),
    dependency('gio-unix-2.0'),
    dependency('gobject-2.0'),
    dependency('gthread-2.0'),  
    dependency('gee-0.8', version: gee_version),
    dependency('json-glib-1.0', version: json_version),
    dependency('keybinder-3.0'),
    dependency('libnotify'),
]

if get_option('enable-librest')
    rest_dep = dependency('rest-0.7',
        not_found_message: 'rest-0.7 is not installed')
    rest_vala_flags = '--pkg rest-0.7 -D HAVE_LIBREST'
    conf.set('HAVE_LIBREST', 1, description: 'Have AppIndicator')
endif

if get_option('enable-indicator')
    indicator_dep = dependency('appindicator3-0.1',
        not_found_message: 'appindicator3-0.1 is not installed')
    indicator_vala_flags = '--pkg appindicator3-0.1 -D HAVE_INDICATOR'
    conf.set('HAVE_INDICATOR', 1, description: 'Have Indicator')
endif

if get_option('enable-zeitgeist')
    zeitgeist_dep = dependency('zeitgeist-2.0',
        version: zeitgeist_version,
        not_found_message: 'zeitgeist-2.0 is not installed')
    zeitgeist_vala_flags = '--pkg zeitgeist-2.0 -D HAVE_ZEITGEIST'
    conf.set('HAVE_ZEITGEIST', 1, description: 'Have Zeitgeist')
endif

# Write configuration to config.h
configure_file(output: 'config.h',
               configuration: conf)

add_project_arguments('-include', 'config.h', 
    language : 'c')

subdir('vapi')
subdir('src')
subdir('data')
subdir('po')

# -include $(CONFIG_HEADER) \
#     -DDATADIR=\"$(datadir)\" \
#     -DPKGDATADIR=\"$(pkgdatadir)\" \
#     -DLIBDIR=\"$(libdir)\" \
#     -DPKGLIBDIR=\"$(pkglibdir)\" \
