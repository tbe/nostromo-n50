include_directories(
    ${FLTK_INCLUDE_DIR}
    ${GTK2_INCLUDE_DIRS}
    ${LIBXML2_INCLUDE_DIR}
    ${X11_Xi_INCLUDE_PATH}
    ${X11_XTest_INCLUDE_PATH}
    ${CMAKE_CURRENT_SOURCE_DIR}
)

SET(nostromo_config_SOURCES
    ui_support.cxx
    save.cxx
    load.cxx
    NewMapWindow.cxx
)

SET(nostromo_daemon_SOURCES
    daemon.cxx
    docklet.cxx
    eggtrayicon.c
    load.cxx
)

SET(nostromo_remote_SOURCES
    remote.cxx
    load.cxx
)

fltk_wrap_ui(nostromo_config ui.fl)

add_executable(nostromo_config ${nostromo_config_SOURCES} ${nostromo_config_FLTK_UI_SRCS})

target_link_libraries(nostromo_config
    ${FLTK_LIBRARIES}
    ${LIBXML2_LIBRARIES}
)

target_compile_definitions(nostromo_config PRIVATE 
    "-DVERSION=\"${nostromo_version}\""
    ${LIBXML2_DEFINITIONS}
)



add_executable(nostromo_daemon ${nostromo_daemon_SOURCES})

target_link_libraries(nostromo_daemon
    ${X11_XTest_LIB}
    ${X11_Xi_LIB}
    ${LIBXML2_LIBRARIES}
    ${X11_X11_LIB}
    ${CMAKE_THREAD_LIBS_INIT}
    ${GTK2_LIBRARIES}
)

target_compile_definitions(nostromo_daemon PRIVATE
    "-DIMG_PATH=\"${INSTALL_DATADIR}\""
)

add_executable(nostromo_remote ${nostromo_remote_SOURCES})
target_link_libraries(nostromo_remote
    ${X11_XTest_LIB}
    ${X11_Xi_LIB}
    ${X11_X11_LIB}
    ${CMAKE_THREAD_LIBS_INIT}
    ${LIBXML2_LIBRARIES}
)

install(
    TARGETS
        nostromo_config
        nostromo_daemon
        nostromo_remote
    RUNTIME DESTINATION bin   
)


install(
    DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/
    DESTINATION ${INSTALL_DATADIR}
    FILES_MATCHING
        PATTERN "*.png"
)
