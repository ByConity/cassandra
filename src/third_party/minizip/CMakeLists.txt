file(GLOB SOURCES ioapi.c unzip.c crypt.h ioapi.h unzip.h)

source_group("Source Files\\" REGULAR_EXPRESSION ".*\\.c(pp)?")
source_group("Header Files\\" REGULAR_EXPRESSION ".*\\.h(pp)?")

# Add suffix for both kinds of name to distiguish from contrib/minizip
if(CASS_BUILD_SHARED)
  add_library(minizip_share OBJECT ${SOURCES})
  target_include_directories(minizip_share PRIVATE ${ZLIB_INCLUDE_DIRS})
  set_target_properties(minizip_share PROPERTIES
    POSITION_INDEPENDENT_CODE ON
    FOLDER "Driver/Dependencies")
endif()

if(CASS_BUILD_STATIC)
  add_library(minizip_static OBJECT ${SOURCES})
  target_include_directories(minizip_static PRIVATE ${ZLIB_INCLUDE_DIRS})
  set_target_properties(minizip_static PROPERTIES 
    FOLDER "Driver/Dependencies")
endif()
