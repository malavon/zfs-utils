cmake_minimum_required(VERSION 3.5)

project(zfs-utils LANGUAGES C)

set(ZFS_SYSTEM_INCLUDES
    /usr/src/sys/contrib/openzfs/include
    /usr/src/sys/contrib/openzfs/lib/libspl/include/os/freebsd
    /usr/src/sys/contrib/openzfs/lib/libspl/include)

include_directories(SYSTEM
    /usr/include
    /usr/local/include # shouldn't be necessary? todo: lz4.h found by cmake
   ${ZFS_SYSTEM_INCLUDES})

add_executable(zfs-utils main.c)

add_executable(zfs-dump zdump.c)

find_library(LIBRARY_LZ4    lz4)
find_library(LIBRARY_JSONC  json-c)

# target_link_directories(zfs-walk /usr/local/lib)
target_link_libraries(zfs-dump	${LIBRARY_LZ4} ${LIBRARY_JSONC} nvpair spl zfs zfs_core zpool)
target_compile_options(zfs-dump PUBLIC -Werror-implicit-function-declaration )

include(GNUInstallDirs)
install(
  TARGETS zfs-utils
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})
