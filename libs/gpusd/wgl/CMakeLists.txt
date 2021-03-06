if(NOT WIN32)
  return()
endif()

set(HEADERS
  module.h
)

set(SOURCES
  module.cpp
)

set(LIBRARY gpusd_wgl)
set(INCLUDE include/gpusd/wgl)

source_group(\\ FILES CMakeLists.txt ${HEADERS} ${SOURCES})
add_library(${LIBRARY} SHARED ${HEADERS} ${SOURCES})
target_link_libraries(${LIBRARY} ${OPENGL_gl_LIBRARY} gpusd)
set_target_properties(${LIBRARY} PROPERTIES VERSION ${VERSION}
  SOVERSION ${VERSION_MAJOR} PUBLIC_HEADER "${HEADERS}"
  COMPILE_DEFINITIONS "GPUSD_SHARED")
if(CMAKE_PROJECT_NAME MATCHES "gpusd")
  install(TARGETS ${LIBRARY}
    PUBLIC_HEADER DESTINATION ${INCLUDE} COMPONENT dev
    ARCHIVE DESTINATION lib COMPONENT dev
    RUNTIME DESTINATION bin COMPONENT runtime
    LIBRARY DESTINATION lib COMPONENT runtime)
endif()