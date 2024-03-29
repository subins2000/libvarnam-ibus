
cmake_minimum_required (VERSION 2.8.8)

project(ibus-engine-varnam)
message ("Generating project ${PROJECT_NAME}")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_HOME_DIRECTORY} )
set(CMAKE_INSTALL_PREFIX "/usr" CACHE PATH "Install dir prefix")
set(IBUS_INSTALL_PREFIX "/usr" CACHE PATH "IBus install dir prefix")
set(GLIB_VER 2.0)
set(IBUS_VER 1.3)
set(VARNAM_VER 3.0.0)
set(GTK_VER 3.10)
set(COMMON_INCLUDE_DIRS ${CMAKE_SOURCE_DIR}/common)
set(sync_executable_name varnam-sync)
set(preferences_executable_name ibus-engine-varnam-prefs)

##################################
# Finding required packages
#################################

FIND_PACKAGE(CURL)
FIND_PACKAGE(PkgConfig)
PKG_CHECK_MODULES(GLIB REQUIRED glib-2.0>=${GLIB_VER})
PKG_CHECK_MODULES(IBUS REQUIRED ibus-1.0>=${IBUS_VER})
PKG_CHECK_MODULES(VARNAM REQUIRED varnamstatic>=${VARNAM_VER})
PKG_CHECK_MODULES(GTK+ REQUIRED gtk+-3.0>=${GTK_VER})

IF(CMAKE_COMPILER_IS_GNUCC)
    set(CMAKE_C_FLAGS "-Wall")
    set(CMAKE_C_FLAGS_DEBUG "-g")
    set(CMAKE_C_FLAGS_RELEASE "-O2")
ENDIF()

# Making a directory for learnings file
file(MAKE_DIRECTORY $ENV{HOME}/.local/share/varnam/suggestions)

add_subdirectory(common)
add_subdirectory(engine)
add_subdirectory(preferences)

install(FILES icons/varnam.png DESTINATION ${CMAKE_INSTALL_PREFIX}/share/varnam/ibus/icons)


