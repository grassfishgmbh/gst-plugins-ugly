# sidplay plugin works with libsidplay 1.36.x (not 2.x.x)
have_sidplay = false
if add_languages('cpp')
  cxx = meson.get_compiler('cpp')
  if cxx.has_argument('-fvisibility=hidden')
    cxx_vis_args = ['-fvisibility=hidden']
  else
    cxx_vis_args = []
  endif

  if cxx.has_header('sidplay/player.h')
    sid_code = '''#include <sidplay/player.h>
                  void somefunc (void) {
                    sidTune tune = sidTune(0);
                  }'''
    sidplay_dep = cxx.find_library('sidplay', required: false)
    if sidplay_dep.found()
      have_sidplay = cxx.compiles(sid_code, dependencies: sidplay_dep, name : 'sidplay')
    endif
  endif
endif

if have_sidplay
  shared_module('gstsid', 'gstsiddec.cc',
    cpp_args : ugly_args + cxx_vis_args,
    include_directories : [configinc],
    dependencies : [gstaudio_dep, sidplay_dep],
    install : true,
    install_dir : plugins_install_dir)
endif
