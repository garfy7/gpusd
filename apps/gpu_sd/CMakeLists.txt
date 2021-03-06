
if(NOT LUNCHBOX_USE_DNSSD)
  return()
endif()

set(HEADERS)
set(SOURCES gpu_sd.cpp)

include_directories(${LUNCHBOX_INCLUDE_DIRS})
set(LINK_LIBRARIES ${LUNCHBOX_LIBRARIES} gpusd)

if(APPLE)
  add_definitions(-DGPUSD_CGL)
  list(APPEND LINK_LIBRARIES gpusd_cgl)
endif()
if(X11_FOUND)
  add_definitions(-DGPUSD_GLX)
  list(APPEND LINK_LIBRARIES gpusd_glx)
endif()
if(WIN32)
  add_definitions(-DGPUSD_WGL)
  list(APPEND LINK_LIBRARIES gpusd_wgl ws2_32)
endif()

if(Boost_FOUND)
  list(APPEND LINK_LIBRARIES ${Boost_PROGRAM_OPTIONS_LIBRARY})
else()
  message(STATUS
    "boost::program_options missing, command line options not available")
endif()

source_group(\\ FILES ${SOURCES} ${HEADERS})
add_executable(gpu_sd ${SOURCES} ${HEADERS})
target_link_libraries(gpu_sd ${LINK_LIBRARIES})
if(CMAKE_PROJECT_NAME MATCHES "gpusd")
  install(TARGETS gpu_sd DESTINATION bin COMPONENT daemon)
endif()
