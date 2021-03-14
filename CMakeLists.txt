cmake_minimum_required (VERSION 3.11) #Must allow add_library() with a single argument

project (argtable2)

option (HAVE_GETOPT_H "Have the getopt library" OFF)
option (HAVE_INTTYPES_H "Have the file inttypes.h" ON)
option (HAVE_MEMORY_H "Have the file memory.h" ON)
option (HAVE_STDLIB_H "Have the file stdlib.h" ON)
option (HAVE_STRINGS_H "Have the strings.h" OFF)
option (HAVE_STRING_H "Have the file string.h" ON)
option (HAVE_STDC_HEADERS "Have std C header files" ON)

add_library (argtable2 STATIC)

if (HAVE_GETOPT_H)
  target_compile_definitions (argtable2 PRIVATE HAVE_GETOPT_H)
endif ()
if (HAVE_INTTYPES_H)
  target_compile_definitions (argtable2 PRIVATE HAVE_INTTYPES_H )
endif ()
if (HAVE_MEMORY_H)
  target_compile_definitions (argtable2 PRIVATE HAVE_MEMORY_H)
endif ()
if (HAVE_STDLIB_H)
  target_compile_definitions (argtable2 PRIVATE HAVE_STDLIB_H)
endif ()
if (HAVE_STRINGS_H)
  target_compile_definitions (argtable2 PRIVATE HAVE_STRINGS_H)
endif ()
if (HAVE_STRING_H)
  target_compile_definitions (argtable2 PRIVATE HAVE_STRING_H)
endif ()
if (HAVE_STDC_HEADERS)
  target_compile_definitions (argtable2 PRIVATE STDC_HEADERS)
endif ()

#Allow relative paths in target_sources(). Will be converted to absolute paths
#under the assumption that they are relative to the source directory.
cmake_policy (SET CMP0076 NEW)

if (UNIX)
#Requires the TRE library 
  target_sources (argtable2
  PRIVATE
    src/arg_date.c
    src/arg_rex.c   
  )
endif (UNIX)

target_sources (argtable2 
PRIVATE
  src/arg_dbl.c
  src/arg_end.c
  src/arg_file.c
  src/arg_lit.c
  src/arg_rem.c
  src/arg_int.c
  src/arg_str.c
  src/argtable2.c
  src/getopt.c
  src/getopt1.c
  src/getopt.h
PUBLIC
  src/argtable2.h
)

target_include_directories (argtable2 PUBLIC src)

install (TARGETS argtable2 RUNTIME DESTINATION bin LIBRARY DESTINATION lib ARCHIVE DESTINATION lib)
install (FILES src/argtable2.h DESTINATION include)
