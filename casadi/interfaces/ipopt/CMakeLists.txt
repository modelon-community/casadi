cmake_minimum_required(VERSION 3.10.2)

set(NLPSOL_IPOPT_SRCS
  ipopt_interface.hpp
  ipopt_interface.cpp
  ipopt_nlp.hpp
  ipopt_nlp.cpp
  ipopt_interface_meta.cpp)

if(WITH_IPOPT_CALLBACK)
  add_definitions(-DWITH_IPOPT_CALLBACK)
endif()

casadi_plugin(Nlpsol ipopt ${NLPSOL_IPOPT_SRCS})
if(MSVC)
  set(IPOPT_LIBRARIES ${IPOPT_LIBRARIES} mkl_intel_lp64 mkl_sequential mkl_core netapi32 comctl32 Ws2_32 Dhcpcsvc Userenv Shlwapi Comdlg32 OleAut32 Ole32 Wbemuuid legacy_stdio_definitions)
endif()
casadi_plugin_link_libraries(Nlpsol ipopt ${IPOPT_LIBRARIES})

#set_property(TARGET casadi_nlpsol_ipopt PROPERTY PKG_CONFIG_REQUIRES ipopt)
