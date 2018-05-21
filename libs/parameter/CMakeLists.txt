cmake_minimum_required(VERSION 3.5)
project(boost_parameter)

find_package(boost_core)
find_package(boost_mpl)
find_package(boost_detail)
find_package(boost_type_traits)
find_package(boost_optional)
find_package(boost_preprocessor)
find_package(boost_config)
find_package(boost_utility)


add_library(boost_parameter INTERFACE
)
add_library(boost::parameter ALIAS boost_parameter)
set_property(TARGET boost_parameter PROPERTY EXPORT_NAME parameter)

target_link_libraries(boost_parameter INTERFACE boost::core)
target_link_libraries(boost_parameter INTERFACE boost::mpl)
target_link_libraries(boost_parameter INTERFACE boost::detail)
target_link_libraries(boost_parameter INTERFACE boost::type_traits)
target_link_libraries(boost_parameter INTERFACE boost::optional)
target_link_libraries(boost_parameter INTERFACE boost::preprocessor)
target_link_libraries(boost_parameter INTERFACE boost::config)
target_link_libraries(boost_parameter INTERFACE boost::utility)

target_include_directories(boost_parameter INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)

install(DIRECTORY include/ DESTINATION include)

install(TARGETS boost_parameter EXPORT boost_parameter-targets
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    INCLUDES DESTINATION include
)

install(EXPORT boost_parameter-targets
  FILE boost_parameter-targets.cmake
  NAMESPACE boost::
  DESTINATION lib/cmake/boost_parameter
)

