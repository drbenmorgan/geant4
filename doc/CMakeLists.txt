# - Test of building Doxygen docs for Geant4 toolkit code
find_package(Doxygen QUIET)
if(NOT Doxygen_FOUND)
  message(WARNING "Doxygen not found, disabling doc generation")
  return()
endif()

# Should be done at a higher level (we currently have to maintain versions
# outside of project() due to nested calls)
set(PROJECT_VERSION ${${PROJECT_NAME}_VERSION})

# - Organised as per https://www.doxygen.nl/manual/config.html
# Project related options
set(DOXYGEN_FULL_PATH_NAMES NO)
#set(DOXYGEN_PROJECT_LOGO "the current geant4 logo in suitable form")

# Build related configuration options
set(DOXYGEN_SHOW_USED_FILES NO)

# Configuration options related to the input files
set(DOXYGEN_FILE_PATTERNS
  "*.hh"
  "*.icc"
  "*.md"
)
set(DOXYGEN_EXTENSION_MAPPING "icc=C++")
set(DOXYGEN_EXCLUDE_PATTERNS "*/test/*")
#set(DOXYGEN_USE_MDFILE_AS_MAINPAGE "${PROJECT_SOURCE_DIR}/README.md")

# Configuration options related to the HTML output
# - DOXYGEN_HTML_... options
# - Can use for things like MathJax, custom stylesheet, search engines etc

# Turn off all other LaTeX generator, all others are NO by default
# - May want to investigate XML generator for Breathe use
set(DOXYGEN_GENERATE_LATEX NO)

# These are for testing gross structure even if not everything is documented yet
# - Will generate all correct files/info etc
set(DOXYGEN_EXTRACT_ALL NO)
set(DOXYGEN_SOURCE_BROWSER YES)

set(DOXYGEN_ALIASES
    [[check="@xrefitem check \"CHECK\" \"To be checked\""]]
)
set(DOXYGEN_VERBATIM_VARS DOXYGEN_ALIASES)

# Call CMake function from FindDoxygen to generate
doxygen_add_docs(doc
  "${PROJECT_SOURCE_DIR}/source/global/management"
  "${PROJECT_SOURCE_DIR}/source/geometry/management"
  WORKING_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}"
  COMMENT "Processing C++ documentation with Doxygen"
)





