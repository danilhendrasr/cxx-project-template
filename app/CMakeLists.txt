set(EXE_SOURCES main.cc)

add_executable(${EXECUTABLE_NAME} ${EXE_SOURCES})

target_link_libraries(${EXECUTABLE_NAME} PUBLIC 
    ${LIBRARY_NAME} 
    nlohmann_json)

if(${ENABLE_WARNINGS})
    target_set_warnings(
        TARGET ${EXECUTABLE_NAME} 
        ENABLE ${ENABLE_WARNINGS} 
        AS_ERRORS ${ENABLE_WARNINGS_AS_ERRORS})
endif()

if(${ENABLE_LTO})
    target_enable_lto(
        TARGET ${EXECUTABLE_NAME} 
        ENABLE ${ENABLE_LTO})
endif()