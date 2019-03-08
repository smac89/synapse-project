vala_sources = files('common-actions.vala',
    'config-service.vala',
    'data-sink.vala',
    'dbus-service.vala',
    'desktop-file-service.vala',
    'match.vala',
    'plugin.vala',
    'query.vala',
    'relevancy-service.vala',
    'result-set.vala',
    'utils.vala',
    'volume-service.vala'
)

deps = dependencies

foreach vflag : synapse_common_vala_flags
    add_project_arguments(vflag, language: 'vala')
endforeach

foreach vflag : synapse_modules_vala_flags
    add_project_arguments(vflag, language: 'vala')
endforeach

if conf.has('HAVE_ZEITGEIST')
    vala_sources += files('relevancy-backend-zg.vala')
    add_project_arguments(zeitgeist_vala_flags, language: 'vala')
    deps += zeitgeist_dep
endif

shared_library('synapsecore',
    vala_sources,
    dependencies: deps,
    install: false
)
