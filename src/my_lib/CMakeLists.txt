
set(LIBRARY_SOURCES my_lib.cc)
set(LIBRARY_HEADERS my_lib.h)
set(LIBRARY_INCLUDES 
    "./"
    "${CMAKE_BINARY_DIR}/configured_files/include"
    spdlog::spdlog)

add_library(${LIBRARY_NAME} STATIC ${LIBRARY_SOURCES} ${LIBRARY_HEADERS})
target_include_directories(${LIBRARY_NAME} PUBLIC ${LIBRARY_INCLUDES})
target_link_libraries(${LIBRARY_NAME} PUBLIC 
    spdlog::spdlog
    nlohmann_json::nlohmann_json
    Catch2::Catch2)

if(${ENABLE_WARNINGS})
    target_set_warnings(
        TARGET ${LIBRARY_NAME} 
        ENABLE ${ENABLE_WARNINGS} 
        AS_ERRORS ${ENABLE_WARNINGS_AS_ERRORS})
endif()

if(${ENABLE_LTO})
    target_enable_lto(
        TARGET ${LIBRARY_NAME} 
        ENABLE ${ENABLE_LTO})
endif()