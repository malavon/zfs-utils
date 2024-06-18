cmake_minimum_required(VERSION 3.5)

project(zfs-utils LANGUAGES C)

add_executable(zfs-utils main.c)

include(GNUInstallDirs)
install(
  TARGETS zfs-utils
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})
