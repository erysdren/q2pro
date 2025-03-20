project('vmlib', version: '2.0.0')

cmake   = import('cmake')
opt_var = cmake.subproject_options()

opt_var.add_cmake_defines({'WAMR_BUILD_AOT': false})
opt_var.add_cmake_defines({'WAMR_BUILD_LIBC_BUILTIN': false})
opt_var.add_cmake_defines({'WAMR_BUILD_LIBC_WASI': false})
opt_var.add_cmake_defines({'WAMR_BUILD_SIMD': false})

sub_pro = cmake.subproject('libvmlib_cmake', options: opt_var)

libvmlib_dep = sub_pro.dependency('iwasm_static')
