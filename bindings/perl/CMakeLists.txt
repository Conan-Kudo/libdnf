find_package(SWIG REQUIRED)
include(UseSWIG)


message("Building for perl")
find_package(Perl REQUIRED)
find_package(PerlLibs REQUIRED)


include_directories(${CMAKE_SOURCE_DIR})
include_directories(${PERL_INCLUDE_PATH})
include(UseSWIG)

if(CMAKE_SIZEOF_VOID_P EQUAL 8)
    # using 64bit architecture
    set(CMAKE_SWIG_FLAGS "-DSWIGWORDSIZE64")
endif()

# The libdnf API is under development now. This enables it for internal usage.
set(CMAKE_SWIG_FLAGS ${CMAKE_SWIG_FLAGS} "-DLIBDNF_UNSTABLE_API")

set(COMMON_TYPES_NAME "common_types")
set_source_files_properties(../swig/${COMMON_TYPES_NAME}.i PROPERTIES CPLUSPLUS ON)
swig_add_module(${COMMON_TYPES_NAME} perl ../swig/${COMMON_TYPES_NAME}.i)
swig_link_libraries(${COMMON_TYPES_NAME} libdnf)
swig_link_libraries(${COMMON_TYPES_NAME} ${PERL_LIBRARY})

set(CONFIG_NAME "conf")
set_source_files_properties(../swig/${CONFIG_NAME}.i PROPERTIES CPLUSPLUS ON)
swig_add_module(${CONFIG_NAME} perl ../swig/${CONFIG_NAME}.i)
swig_link_libraries(${CONFIG_NAME} libdnf)
swig_link_libraries(${CONFIG_NAME} ${PERL_LIBRARY})

set(REPO_NAME "repo")
set_source_files_properties(../swig/${REPO_NAME}.i PROPERTIES CPLUSPLUS ON)
swig_add_module(${REPO_NAME} perl ../swig/${REPO_NAME}.i)
swig_link_libraries(${REPO_NAME} libdnf)
swig_link_libraries(${REPO_NAME} ${PERL_LIBRARY})

set(SMARTCOLS_NAME "smartcols")
set_source_files_properties(../swig/${SMARTCOLS_NAME}.i PROPERTIES CPLUSPLUS ON)
swig_add_module(${SMARTCOLS_NAME} perl ../swig/${SMARTCOLS_NAME}.i)
swig_link_libraries(${SMARTCOLS_NAME} libdnf)
swig_link_libraries(${SMARTCOLS_NAME} ${PERL_LIBRARY})

set_source_files_properties(../swig/utils.i PROPERTIES CPLUSPLUS ON)
swig_add_module(utils perl ../swig/utils.i)
swig_link_libraries(utils libdnf)
swig_link_libraries(utils ${PERL_LIBRARY})
swig_link_libraries(utils ${SQLite3_LIBRARIES})

set_source_files_properties(../swig/transaction.i PROPERTIES CPLUSPLUS ON)
swig_add_module(transaction perl ../swig/transaction.i)
swig_link_libraries(transaction libdnf)
swig_link_libraries(transaction ${PERL_LIBRARY})

set(MODULE_NAME "module")
set_source_files_properties(../swig/${MODULE_NAME}.i PROPERTIES CPLUSPLUS ON)
swig_add_module(${MODULE_NAME} perl ../swig/${MODULE_NAME}.i)
swig_link_libraries(${MODULE_NAME} libdnf)
swig_link_libraries(${MODULE_NAME} ${PERL_LIBRARY})
