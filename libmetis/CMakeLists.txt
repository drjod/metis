# Add this directory for internal users.
include_directories(BEFORE .)
# Find sources.
file(GLOB metis_sources *.c)
# Build libmetis.
add_library(metis ${GKlib_sources} ${metis_sources})
target_link_libraries(metis ${CONAN_LIBS})
if(UNIX)
  target_link_libraries(metis m)
elseif(MSVC)
  include(GenerateExportHeader)
  generate_export_header(metis)
endif()

install(TARGETS metis
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION lib
  ARCHIVE DESTINATION lib)
