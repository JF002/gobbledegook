cmake_minimum_required(VERSION 3.5)


project(gobbledegook LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(PkgConfig REQUIRED)
find_package(Threads REQUIRED)

pkg_search_module(GLib REQUIRED glib-2.0)
pkg_search_module(GTK REQUIRED gtk+-3.0)
pkg_search_module(GIO REQUIRED gio-2.0 gio-unix-2.0)

include_directories(${GLib_INCLUDE_DIRS}
  ${GTK_INCLUDE_DIRS}
  ${GIO_INCLUDE_DIRS})

link_directories(${GLib_LIBRARY_DIRS}
  ${GTK_LIBRARY_DIRS}
  ${GIO_LIBRARY_DIRS})

add_definitions(${GTK_CFLAGS_OTHER})

add_library(gobbledegook STATIC
  src/DBusInterface.cpp
  src/DBusInterface.h
  src/DBusMethod.cpp
  src/DBusMethod.h
  src/DBusObject.cpp
  src/DBusObject.h
  src/DBusObjectPath.h
  src/GattCharacteristic.cpp
  src/GattCharacteristic.h
  src/GattDescriptor.cpp
  src/GattDescriptor.h
  src/GattInterface.cpp
  src/GattInterface.h
  src/GattProperty.cpp
  src/GattProperty.h
  src/GattService.cpp
  src/GattService.h
  src/GattUuid.h
  src/Globals.h
  src/Gobbledegook.cpp
  src/HciAdapter.cpp
  src/HciAdapter.h
  src/HciSocket.cpp
  src/HciSocket.h
  src/Init.cpp
  src/Init.h
  src/Logger.cpp
  src/Logger.h
  src/Mgmt.cpp
  src/Mgmt.h
  src/Server.cpp
  src/Server.h
  src/ServerUtils.cpp
  src/ServerUtils.h
  src/TickEvent.h
  src/Utils.cpp
  src/Utils.h
)

target_link_libraries(gobbledegook PRIVATE
  ${GLib_LIBRARIES}
  ${GKT_LIBRARIES}
  ${GIO_LIBRARIES}
  pthread
  )

add_executable(standalone src/standalone.cpp)
target_link_libraries(standalone
  gobbledegook
  )
