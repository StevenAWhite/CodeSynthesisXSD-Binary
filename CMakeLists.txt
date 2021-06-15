cmake_minimum_required(VERSION 3.10)

# set the project name
project(Code_Synthesis_XSD CXX )

if(XSD_CROSS_INSTALL)
  set(BINARY_DESTINATION  ${CMAKE_HOST_SYSTEM_NAME}/bin/)
  set(HEADER_DESTINATION include/)
else()
  set(BINARY_DESTINATION  bin/)
  set(HEADER_DESTINATION include/)
endif()
message(STATUS "CMAKE_HOST_SYSTEM_NAME=${CMAKE_HOST_SYSTEM_NAME} OR WIN32=${WIN32}")
if(CMAKE_HOST_SYSTEM_NAME STREQUAL "Windows" OR WIN32)
install(PROGRAMS x86_64-windows-msvc/bin/xsd.exe
        DESTINATION  ${BINARY_DESTINATION}
        PERMISSIONS  OWNER_EXECUTE OWNER_WRITE OWNER_READ
                     GROUP_EXECUTE             GROUP_READ
                     WORLD_EXECUTE             WORLD_READ
       )
install(DIRECTORY x86_64-windows-msvc/libxsd/
        DESTINATION ${HEADER_DESTINATION}
        FILE_PERMISSIONS  OWNER_WRITE OWNER_READ
                          GROUP_READ
                          WORLD_READ
        DIRECTORY_PERMISSIONS 
                          OWNER_EXECUTE OWNER_WRITE OWNER_READ
                          GROUP_EXECUTE GROUP_READ
                          WORLD_EXECUTE WORLD_READ
        FILES_MATCHING
                        PATTERN "*.?xx"
        )
elseif ( UNIX AND NOT APPLE)
install(PROGRAMS x86_64-linux-gnu/bin/xsd
        DESTINATION ${BINARY_DESTINATION}
        PERMISSIONS  OWNER_EXECUTE OWNER_WRITE OWNER_READ
                     GROUP_EXECUTE             GROUP_READ
                     WORLD_EXECUTE             WORLD_READ
       )
install(DIRECTORY x86_64-linux-gnu/libxsd/
        DESTINATION ${HEADER_DESTINATION}
        FILE_PERMISSIONS  OWNER_WRITE OWNER_READ
                          GROUP_READ
                          WORLD_READ
        DIRECTORY_PERMISSIONS 
                          OWNER_EXECUTE OWNER_WRITE OWNER_READ
                          GROUP_EXECUTE GROUP_READ
                          WORLD_EXECUTE WORLD_READ
        FILES_MATCHING
        PATTERN "*.?xx"
        ) 
else()
 message(WARNING "This repositroy does not support APPLE installations use brew")
 message(INFO "The previous message is not an ERROR to allow drop through of this package in meta installations")
endif()


