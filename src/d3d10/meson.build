d3d10_res      = wrc_generator.process('version10.rc')
d3d10_1_res    = wrc_generator.process('version10_1.rc')
d3d10_core_res = wrc_generator.process('version10_core.rc')

d3d10_core_src = [
  'd3d10_core.cpp',
]

d3d10_main_src = [
  'd3d10_main.cpp',
  'd3d10_reflection.cpp',
  'd3d10_state_block.cpp',
]

version_script_args = []

if dxvk_native and dxvk_platform != 'windows'
  version_script_args = [
    '-Wl,--version-script=@0@/d3d10core.ver'.format(meson.current_source_dir()),
  ]
endif

d3d10_core_dll = shared_library('d3d10core'+dll_ext, d3d10_core_src, d3d10_core_res,
  name_prefix         : '',
  dependencies        : [ d3d11_dep ],
  gnu_symbol_visibility: 'hidden',
  include_directories : dxvk_include_path,
  install             : true,
  link_args           : version_script_args,
  vs_module_defs      : 'd3d10core'+def_spec_ext,
  override_options    : ['cpp_std='+dxvk_cpp_std])

d3d10_core_dep = declare_dependency(
  link_with           : [ d3d10_core_dll ])

if dxvk_native and dxvk_platform != 'windows'
  version_script_args = [
    '-Wl,--version-script=@0@/d3d10.ver'.format(meson.current_source_dir()),
  ]
endif

d3d10_deps = [ lib_d3dcompiler_43, lib_dxgi, dxbc_dep, dxvk_dep, d3d10_core_dep ]

d3d10_dll = shared_library('d3d10'+dll_ext, d3d10_main_src, d3d10_res,
  name_prefix         : '',
  dependencies        : [ d3d10_deps ],
  gnu_symbol_visibility: 'hidden',
  include_directories : dxvk_include_path,
  install             : true,
  link_args           : version_script_args,
  vs_module_defs      : 'd3d10'+def_spec_ext,
  override_options    : ['cpp_std='+dxvk_cpp_std])

if dxvk_native and dxvk_platform != 'windows'
  version_script_args = [
    '-Wl,--version-script=@0@/d3d10_1.ver'.format(meson.current_source_dir()),
  ]
endif

d3d10_1_dll = shared_library('d3d10_1'+dll_ext, d3d10_main_src, d3d10_1_res,
  name_prefix         : '',
  dependencies        : [ d3d10_deps ],
  gnu_symbol_visibility: 'hidden',
  include_directories : dxvk_include_path,
  install             : true,
  link_args           : version_script_args,
  vs_module_defs      : 'd3d10_1'+def_spec_ext,
  override_options    : ['cpp_std='+dxvk_cpp_std])

d3d10_dep = declare_dependency(
  link_with           : [ d3d10_dll, d3d10_1_dll, d3d10_core_dll ],
  include_directories : [ dxvk_include_path ])
