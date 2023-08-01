add_custom_target(build_lef ALL
        COMMAND ${CMAKE_MAKE_PROGRAM}
        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/lef
        COMMENT "Original lef makefile target")
add_custom_target(build_def ALL
        COMMAND ${CMAKE_MAKE_PROGRAM}
        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/def
        COMMENT "Original def makefile target")

add_library(lef STATIC IMPORTED)
add_library(def STATIC IMPORTED)

set_property(TARGET lef APPEND PROPERTY IMPORTED_CONFIGURATIONS NOCONFIG)
set_target_properties(lef PROPERTIES IMPORTED_LOCATION_NOCONFIG "${METIS_LIBRARY}")

set_property(TARGET def APPEND PROPERTY IMPORTED_CONFIGURATIONS NOCONFIG)
set_target_properties(def PROPERTIES IMPORTED_LOCATION_NOCONFIG "${PARMETIS_LIBRARY}")

add_dependencies(lef build_lef)
add_dependencies(def build_def)