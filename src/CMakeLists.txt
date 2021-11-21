

# IF ( USE_OPENCL )
# 	ADD_DEFINITIONS( -DUSE_OPENCL )
# ENDIF()

# IF( MSVC )
#     MATH(EXPR SIZEOF_VOID_P_BITS "${CMAKE_SIZEOF_VOID_P}*8")
#     ADD_DEFINITIONS( -DSIZEOF_VOID_P=8 -DMAKING_DSO -DI386 -DWIN32 -DSWAP_BITFIELDS -D_WIN32_WINNT=0x0502 -DNOMINMAX -DSTRICT -DWIN32_LEAN_AND_MEAN -D_USE_MATH_DEFINES -D_CRT_SECURE_NO_DEPRECATE -D_CRT_NONSTDC_NO_DEPRECATE -D_SCL_SECURE_NO_WARNINGS -DBOOST_ALL_NO_LIB -DSESI_LITTLE_ENDIAN -DFBX_ENABLED=1 -DOPENCL_ENABLED=1 -DOPENVDB_ENABLED=1 -DOPENEXR_DLL )

#     SET( HOUDINI_LIBRARIES
#         "${HOUDINI_LIBRARY_DIR}/hboost_system-mt-x64.lib"
#         "${HOUDINI_LIBRARY_DIR}/tbb.lib"
#         "${HOUDINI_LIBRARY_DIR}/libCH.lib"
#         "${HOUDINI_LIBRARY_DIR}/libCMD.lib"
#         "${HOUDINI_LIBRARY_DIR}/libGA.lib"
#         "${HOUDINI_LIBRARY_DIR}/libGEO.lib"
#         "${HOUDINI_LIBRARY_DIR}/libGT.lib"
#         "${HOUDINI_LIBRARY_DIR}/libGU.lib"
#         "${HOUDINI_LIBRARY_DIR}/libGUI.lib"
#         "${HOUDINI_LIBRARY_DIR}/libGSTY.lib"
#         "${HOUDINI_LIBRARY_DIR}/libUT.lib"
#         "${HOUDINI_LIBRARY_DIR}/libFS.lib"
#         "${HOUDINI_LIBRARY_DIR}/libSYS.lib"
#         "${HOUDINI_LIBRARY_DIR}/libOP.lib"
#         "${HOUDINI_LIBRARY_DIR}/libOBJ.lib"
#         "${HOUDINI_LIBRARY_DIR}/libSOP.lib"
#         "${HOUDINI_LIBRARY_DIR}/libSTY.lib"
#         "${HOUDINI_LIBRARY_DIR}/libPRM.lib"
#         "${HOUDINI_LIBRARY_DIR}/libROP.lib"
#         "${HOUDINI_LIBRARY_DIR}/libPY.lib"
#         "${HOUDINI_LIBRARY_DIR}/libPYP.lib" )
# ELSEIF( APPLE )
#     ADD_DEFINITIONS( -DMAKING_DSO
#         -DVERSION=\"15.0.416\"
#         -D_GNU_SOURCE -DMBSD
#         -DMBSD_COCOA
#         -DMBSD_INTEL
#         -arch x86_64
#         -DAMD64
#         -fPIC
#         -DSIZEOF_VOID_P=8
#         -DFBX_ENABLED=1
#         -DOPENCL_ENABLED=1
#         -DOPENVDB_ENABLED=1
#         -DSESI_LITTLE_ENDIAN
#         -DENABLE_THREADS
#         -DUSE_PTHREADS
#         -D_REENTRANT
#         -D_FILE_OFFSET_BITS=64
#         -DGCC4 -DGCC3
#         -Wno-deprecated
#         -std=c++11
#         -Wall -W -Wno-parentheses -Wno-sign-compare -Wno-reorder -Wno-uninitialized -Wunused -Wno-unused-parameter )

#     SET( HOUDINI_LIBRARIES
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniGEO.dylib"
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniOP1.dylib"
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniOP2.dylib"
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniOP3.dylib"
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniOPZ.dylib"
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniPRM.dylib"
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniUT.dylib"
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniRAY.dylib"
#         "${HOUDINI_LIBRARY_DIR}/libboost_system.dylib"
#         "${HOUDINI_LIBRARY_DIR}/libtbb.dylib" )
# ELSE()
#     ADD_DEFINITIONS( -DMAKING_DSO -DVERSION=\"15.0.416\" -D_GNU_SOURCE -DLINUX -DAMD64 -m64 -fPIC -DSIZEOF_VOID_P=8 -DFBX_ENABLED=1 -DOPENCL_ENABLED=1 -DOPENVDB_ENABLED=1 -DSESI_LITTLE_ENDIAN -DENABLE_THREADS -DUSE_PTHREADS -D_REENTRANT -D_FILE_OFFSET_BITS=64 -DGCC4 -DGCC3 -Wno-deprecated -std=c++0x -Wall -W -Wno-parentheses -Wno-sign-compare -Wno-reorder -Wno-uninitialized -Wunused -Wno-unused-parameter -fno-strict-aliasing -DBOOST_ALL_NO_LIB )
    
#     SET( HOUDINI_LIBRARIES
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniGEO.so"
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniOPZ.so"
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniPRM.so"
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniUT.so"
#         "${HOUDINI_LIBRARY_DIR}/libHoudiniRAY.so"
#         "" )
# ENDIF()

# IF (USE_OPENCL)
# 	SET( HOUDINI_LIBRARIES ${HOUDINI_LIBRARIES} ${OpenCL_LIBRARY})
# ENDIF()

# INCLUDE_DIRECTORIES( ${HOUDINI_INCLUDE_DIR} ${CMAKE_INSTALL_PREFIX}/include )
# LINK_DIRECTORIES( ${HOUDINI_LIBRARY_DIR} )

# ADD_LIBRARY( HACD SHARED HACD.cpp )
# TARGET_LINK_LIBRARIES( HACD ${HOUDINI_LIBRARIES} VHACD_LIB )

# IF(MSVC)
#     INSTALL( TARGETS HACD RUNTIME DESTINATION bin )
# ELSE()
#     SET_TARGET_PROPERTIES( HACD PROPERTIES PREFIX "" )
#     INSTALL( TARGETS HACD LIBRARY DESTINATION bin )
# ENDIF()

list( APPEND CMAKE_PREFIX_PATH "C:/Program Files/Side Effects Software/Houdini 18.5.563/toolkit/cmake" )
find_package( Houdini REQUIRED )

# Add a library
set( library_name HACD )
add_library( ${library_name} SHARED
    HACD.cpp
)

# Link against the Houdini libraries, and add required include directories and compile definitions.
target_link_libraries( ${library_name} Houdini VHACD_LIB )

# Configure several common target properties, such as its output directory.
houdini_configure_target( ${library_name} )

