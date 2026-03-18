#----------------------------------------------------------------------------
# Re-set target output directories to ensure targets are output to per-test
# subdirectories
unset(CMAKE_RUNTIME_OUTPUT_DIRECTORY)
unset(CMAKE_LIBRARY_OUTPUT_DIRECTORY)
unset(CMAKE_ARCHIVE_OUTPUT_DIRECTORY)

foreach(_c ${CMAKE_CONFIGURATION_TYPES})
  string(TOUPPER ${_c} _c_upper)
  unset(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${_c_upper})
  unset(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${_c_upper})
  unset(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${_c_upper})
endforeach()

#----------------------------------------------------------------------------
# Add core test projects
# - Code/Library Unit Tests 
add_subdirectory(ctests_source)

