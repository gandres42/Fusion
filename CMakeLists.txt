cmake_minimum_required(VERSION 3.15)
project(Fusion VERSION 1.0.0)

add_subdirectory("Fusion")
add_subdirectory("Examples/Advanced")
add_subdirectory("Examples/Simple")

# Include CMakePackageConfigHelpers for generating config files
include(CMakePackageConfigHelpers)

# Export the targets
install(EXPORT FusionTargets
    FILE FusionTargets.cmake
    NAMESPACE Fusion::
    DESTINATION lib/cmake/Fusion
)

# Generate the config file that includes the exports
configure_package_config_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake/FusionConfig.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/FusionConfig.cmake"
    INSTALL_DESTINATION lib/cmake/Fusion
)

# Generate the version file for the config file
write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/FusionConfigVersion.cmake"
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY AnyNewerVersion
)

# Install the generated config and version files
install(FILES
    "${CMAKE_CURRENT_BINARY_DIR}/FusionConfig.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/FusionConfigVersion.cmake"
    DESTINATION lib/cmake/Fusion
)
