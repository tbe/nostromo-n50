install(
    DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/
    DESTINATION ${INSTALL_DOCDIR}
    FILES_MATCHING
        PATTERN "*.png"
        PATTERN "*.html"
)
