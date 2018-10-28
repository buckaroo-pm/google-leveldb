prebuilt_cxx_library(
  name = 'pthread',
  header_only = True,
  exported_linker_flags = [
    '-lpthread',
  ],
)

cxx_library(
  name = 'leveldb',
  licenses = [
    'LICENSE',
  ],
  header_namespace = '',
  exported_headers = subdir_glob([
    ('include', 'leveldb/**/*.h'),
  ]),
  headers = subdir_glob([
    ('', 'db/**/*.h'),
    ('', 'helpers/**/*.h'),
    ('', 'port/**/*.h'),
    ('', 'table/**/*.h'),
    ('', 'util/**/*.h'),
  ]),
  srcs = glob([
    'db/**/*.cc',
    'helpers/**/*.cc',
    'table/**/*.cc',
    'util/**/*.cc',
    'port/**/*.cc',
  ], 
  excludes = [
    'db/db_bench.cc', 
    'db/leveldbutil.cc', 
    '**/*_test.cc',
    '**/testharness.cc',
    '**/testutil.cc',
  ]),
  compiler_flags = [
    '-std=c++11',
  ],
  platform_compiler_flags = [
    ('macos.*', [ '-DOS_MACOSX', '-fno-builtin-memcmp', '-DLEVELDB_PLATFORM_POSIX', '-DLEVELDB_ATOMIC_PRESENT' ]),
    ('iphoneos.*', [ '-DOS_MACOSX', '-fno-builtin-memcmp', '-DLEVELDB_PLATFORM_POSIX', '-DLEVELDB_ATOMIC_PRESENT' ]),
    ('iphonesimulator.*', [ '-DOS_MACOSX', '-fno-builtin-memcmp', '-DLEVELDB_PLATFORM_POSIX', '-DLEVELDB_ATOMIC_PRESENT' ]),
    ('linux.*', [ '-DOS_LINUX', '-DLEVELDB_PLATFORM_POSIX', '-pthread' ]),
    ('android.*', [ '-D_REENTRANT', '-DOS_ANDROID', '-DLEVELDB_PLATFORM_POSIX', '-fno-builtin-memcmp', '-Wno-sign-compare' ]),
    ('windows.*', [ '-lpthread', '-DOS_LINUX', '-DCYGWIN' ]),
  ],
  platform_deps = [
    ('linux.*', [ ':pthread' ]), 
    ('android.*', [ ':pthread' ]), 
  ], 
  visibility = [
    'PUBLIC',
  ],
)

cxx_binary(
  name = 'autocompact-test',
  headers = subdir_glob([
    ('', 'db/**/*.h'),
    ('', 'helpers/**/*.h'),
    ('', 'port/**/*.h'),
    ('', 'table/**/*.h'),
    ('', 'util/**/*.h'),
  ]),
  srcs = glob([
    'db/autocompact_test.cc',
    'util/testharness.cc', 
  ]),
  compiler_flags = [
    '-std=c++11',
  ],
  platform_compiler_flags = [
    ('macos.*', [ '-DOS_MACOSX', '-fno-builtin-memcmp', '-DLEVELDB_PLATFORM_POSIX', '-DLEVELDB_ATOMIC_PRESENT' ]),
    ('linux.*', [ '-DOS_LINUX', '-DLEVELDB_PLATFORM_POSIX' ]),
  ],
  deps = [
    ':leveldb',
  ],
)
