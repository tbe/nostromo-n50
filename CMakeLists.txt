cmake_minimum_required (VERSION 2.8.11)
project(nostromo_n50)
set(nostromo_version 1.5) 

if(NOT DEFINED INSTALL_LIBEXECDIR)
   message(STATUS "Set default libexec as prefix")
   set(INSTALL_LIBEXECDIR "${CMAKE_INSTALL_PREFIX}")
 endif(NOT DEFINED INSTALL_LIBEXECDIR)
 # libdir = ${libexec}/lib
 set(INSTALL_LIBDIR "${INSTALL_LIBEXECDIR}/lib")
 # incdir = ${libexec}/include
 if(NOT DEFINED INSTALL_INCLUDEDIR)
   set(INSTALL_INCLUDEDIR "${INSTALL_LIBEXECDIR}/include")
 endif(NOT DEFINED INSTALL_INCLUDEDIR)
 # datadir = ${libexec}/share or ${prefix}/share/WaveDump
 if(NOT DEFINED INSTALL_DATADIR)
   set(INSTALL_DATADIR "${CMAKE_INSTALL_PREFIX}/share/nostromo")
 endif(NOT DEFINED INSTALL_DATADIR)
 # docdir = ${prefix}/share/doc/WaveDump
 if(NOT DEFINED INSTALL_DOCDIR)
   set(INSTALL_DOCDIR "${CMAKE_INSTALL_PREFIX}/share/doc/nostromo")
 endif(NOT DEFINED INSTALL_DOCDIR)


find_package(FLTK REQUIRED)
find_package(GTK2 REQUIRED)
find_package(LibXml2 REQUIRED)
find_package(X11 REQUIRED)
find_package(Threads REQUIRED)

if(NOT X11_XTest_FOUND)
  message(FATAL_ERROR, "XTest not found")
endif(NOT X11_XTest_FOUND)

if(NOT X11_Xi_FOUND)
  message(FATAL_ERROR, "XInput2 not found")
endif(NOT X11_Xi_FOUND)

add_subdirectory(src)
add_subdirectory(doc)
