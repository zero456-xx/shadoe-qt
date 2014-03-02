# Minimum cmake version required to build
cmake_minimum_required(VERSION 2.8)

# Define shadoe-qt's name
project(shadoe-qt)

# Version number
set(shadoe-qt_version "0.1")

# This takes the file version.h.in and replaces it with version.h.  This allows
# the version name and number defined above to be used by shadoe-qt.  See the file
# version.h.in for more info.

configure_file("${shadoe-qt_SOURCE_DIR}/version.h.in" "${shadoe-qt_BINARY_DIR}/version.h")

find_package(PkgConfig)
pkg_check_modules(GTK REQUIRED gtk+-3.0>=3.0) 
pkg_check_modules(VTE3 REQUIRED vte-2.90>=0.32)

add_definitions(${GTK_CFLAGS} ${GTK_CFLAGS_OTHER} 
                ${VTE3_CFLAGS} ${VTE3_CFLAGS_OTHER})

# Note that we add the shadoe-qt_BINARY_DIR in the include_directories section.
# This is necessary so we can pick up version.h once it's created from
# version.h.in.                                                              

include_directories(${GTK_INCLUDE_DIRS}  
                    ${VTE3_INCLUDE_DIRS} 
                    ${shadoe-qt_BINARY_DIR})
                    
link_libraries(${GTK_LIBRARIES}  
               ${VTE3_LIBRARIES})
               
link_directories(${GTK_LIBRARY_DIRS}  
                 ${VTE3_LIBRARY_DIRS})
                
add_subdirectory(src) #Move to the src directory and run the CMakeLists.txt there  
add_subdirectory(doc) #Move to the doc directory and run the CMakeLists.txt there            

# Set CPack variables for shadoe-qt.  This allows us to build a tarball for shadoe-qt
# with cmake.

set(CPACK_SOURCE_GENERATOR "TBZ2")
set(CPACK_PACKAGE_NAME ${PROJECT_NAME})
set(CPACK_VERSION_MAJOR ${shadoe-qt_version})
set(CPACK_SOURCE_PACKAGE_FILE_NAME "${CPACK_PACKAGE_NAME}-${CPACK_VERSION_MAJOR}")

INCLUDE(CPack)