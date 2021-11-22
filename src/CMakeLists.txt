
# Run your CMAKE as "cmake -DCMAKE_PREFIX_PATH=/your/path ."
# or uncomment this line
# list( APPEND CMAKE_PREFIX_PATH "C:/Program Files/Side Effects Software/Houdini 18.5.563/toolkit/cmake" )

find_package( Houdini REQUIRED )

# Add a library
set( library_name HACD )
add_library( ${library_name} SHARED
    HACD.cpp
)

# Link against the Houdini libraries, and add required include directories and compile definitions.
target_link_libraries( ${library_name} Houdini vhacd )

# Configure several common target properties, such as its output directory.
houdini_configure_target( ${library_name} )

