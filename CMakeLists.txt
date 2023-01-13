cmake_minimum_required(VERSION 3.16.3)

# CMake options.
set(CMAKE_ERROR_DEPRECATED TRUE)
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")
# Añadir PATH para cmake que sepa donde tengo instalado QT6
set(CMAKE_PREFIX_PATH "C:/Qt/6.4.2/msvc2019_64")
# Esa libreria esta compilada en c:/vcpkg! como la añado?
set(LibArchive_INCLUDE_DIR "C:/git/libarchive/include")
set(LibArchive_LIBRARY "C:/git/libarchive/lib/archive.lib")
# Ahora lo mismo con SQLIte_LIBRARY e INCLUDE
set(SQLite_INCLUDE_DIR "C:/vcpkg/installed/x64-windows/include")

set(SQLite_LIBRARY "C:/vcpkg/installed/x64-windows/lib/sqlite3.lib")

set(QT6_INCLUDE_DIR "C:/Qt/6.4.2/msvc2019_64/include")
set(QT6_LIBRARY "C:/Qt/6.4.2/msvc2019_64/lib")

project(Zeal VERSION 0.6.2)

# Set to TRUE for a tagged release.
# NOTE: Don't forget to add a new release entry in the AppStream metadata!
set(RELEASE_VERSION FALSE)

# Project information.
if(APPLE)
    set(PROJECT_OUTPUT_NAME "Foxtrot-Zeal by peseoane")
else()
    set(PROJECT_OUTPUT_NAME "Foxtrot-Zeal by peseoane")
endif()

set(PROJECT_COMPANY_NAME "ZealDocs")
set(PROJECT_COPYRIGHT "2023 Pedro Seoane, Oleg Shparber and other contributors")
set(PROJECT_DESCRIPTION "A simple documentation browser!.")
set(PROJECT_URL "https://github.com/peseoane/zeal")

# Find available major Qt version. It will be stored in QT_VERSION_MAJOR.
find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Core)
if(QT_VERSION_MAJOR EQUAL 6)
    set(QT_MINIMUM_VERSION 6.2.0)
endif()

# Determine version for dev builds.
if(NOT RELEASE_VERSION)
    message(NOTICE "Building unreleased code. Proceed at your own risk!")

    # TODO: Add support for metadata passed from env, e.g. aur, appimage, etc.
    if(Zeal_GIT_VERSION_SHA)
        set(ZEAL_VERSION_SUFFIX "-dev")
    endif()
endif()

set(ZEAL_VERSION_FULL "Foxtrot-Zeal V1R")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /O2")

# For development builds insert an extra release in the AppStream metadata.
if(NOT RELEASE_VERSION)
    string(TIMESTAMP ZEAL_APPSTREAM_DEV_RELEASE "\n    <release date=\"%Y-%m-%d\" version=\"${ZEAL_VERSION_FULL}\" type=\"development\" />")
endif()

# A custom target to print the full version.
# Usage: cmake --build build --target zeal_version
add_custom_target(zeal_version
    COMMAND ${CMAKE_COMMAND} -E echo "Zeal version: ${ZEAL_VERSION_FULL}"
    VERBATIM
)

if(${CMAKE_VERSION} VERSION_GREATER_EQUAL "3.24.0")
    set(CMAKE_COMPILE_WARNING_AS_ERROR ON)
endif()
file(GLOB_RECURSE SRC_FILES "src/*.cpp")
add_subdirectory(assets)
add_subdirectory(src)

add_executable(zeal ${SRC_FILES} ${QM_FILES})

target_include_directories(zeal PRIVATE ${QT6_INCLUDE_DIR} ${LibArchive_INCLUDE_DIR} ${SQLite_INCLUDE_DIR})

target_link_libraries(zeal PRIVATE
${LibArchive_LIBRARY}
${SQLite_LIBRARY}
${QT_LIBRARIES}
)

target_include_directories(zeal PRIVATE
${LibArchive_INCLUDE_DIR}
${SQLite_INCLUDE_DIR}
${QT_INCLUDE_DIR}
)

install(TARGETS zeal DESTINATION bin)




set(CPACK_GENERATOR "NSIS")
set(CPACK_PACKAGE_NAME "Foxtrot-Zeal")
set(CPACK_PACKAGE_VERSION ${ZEAL_VERSION_FULL})
set(CPACK_PACKAGE_VENDOR "ZealDocs")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "A simple documentation browser!.")
set(CPACK_PACKAGE_EXECUTABLES "zeal" "Foxtrot-Zeal")
set(CPACK_NSIS_DISPLAY_NAME "Foxtrot-Zeal")
set(CPACK_NSIS_URL_INFO_ABOUT "https://github.com/peseoane/zeal")
set(CPACK_NSIS_CONTACT "info@pedroseoaneprado.es")
set(CPACK_NSIS_MODIFY_PATH ON)


include(CPack)
set(CPACK_GENERATOR "NSIS")
