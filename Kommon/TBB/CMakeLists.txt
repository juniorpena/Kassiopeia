find_package( TBB REQUIRED )

# headers
set( KOMMON_TBB_HEADER_FILES
    Utility/KMathIntegratorThreaded.h
)

# source
#set( KOMMON_TBB_SOURCE_FILES
#    Utility/KMathIntegratorThreaded.cxx
#)


# get header paths from collected header files
foreach(HEADER ${KOMMON_BOOST_HEADER_FILES})
    get_filename_component(DIRNAME ${CMAKE_CURRENT_SOURCE_DIR}/${HEADER} DIRECTORY)
    target_include_directories(KommonCore PUBLIC $<BUILD_INTERFACE:${DIRNAME}>)
endforeach(HEADER)
target_include_directories(KommonCore PUBLIC $<INSTALL_INTERFACE:include>)

target_include_directories(KommonCore PRIVATE ${TBB_INCLUDE_DIRS})
target_compile_definitions(KommonCore PUBLIC KASPER_USE_TBB)
target_link_libraries(KommonCore
    PRIVATE
        ${TBB_LIBRARIES}
)

#kasper_install_libraries( KommonCore )
kasper_install_headers( ${KOMMON_TBB_HEADER_FILES} )
