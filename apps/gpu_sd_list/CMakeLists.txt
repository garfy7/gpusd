
if(NOT LUNCHBOX_USE_DNSSD)
  return()
endif()

set(HEADERS)
set(SOURCES
  gpu_sd_list.cpp
)

source_group(\\ FILES ${SOURCES} ${HEADERS})
add_executable(gpu_sd_list ${SOURCES} ${HEADERS})
target_link_libraries(gpu_sd_list gpusd_dns_sd)
if(CMAKE_PROJECT_NAME MATCHES "gpusd")
  install(TARGETS gpu_sd_list DESTINATION bin COMPONENT tools)
endif()
