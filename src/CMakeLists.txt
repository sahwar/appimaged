# required for pkg_check_module's IMPORTED_TARGET
cmake_minimum_required(VERSION 3.6)


find_package(PkgConfig)
pkg_check_modules(GLIB glib-2.0 IMPORTED_TARGET)

add_executable(appimaged main.c notify.c notify.h)
target_link_libraries(appimaged PRIVATE inotify-tools libappimage_static xdg-basedir dl PkgConfig::GLIB)

install(
    TARGETS appimaged
    RUNTIME DESTINATION bin COMPONENT appimaged
)
