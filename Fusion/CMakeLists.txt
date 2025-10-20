file(GLOB_RECURSE files "*.c")

add_library(Fusion ${files})

target_include_directories(Fusion PUBLIC 
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include/Fusion>
)

if(UNIX AND NOT APPLE)
    target_link_libraries(Fusion m) # link math library for Linux
endif()

# Install the library
install(TARGETS Fusion
    EXPORT FusionTargets
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include/Fusion
)

# Install header files
file(GLOB headers "*.h")
install(FILES ${headers} DESTINATION include/Fusion)
