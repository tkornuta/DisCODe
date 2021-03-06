
#
ADD_EXECUTABLE(xmltree xmltree.cpp)
MESSAGE(STATUS "\txmltree")
SET(BUILT_TOOLS ${BUILT_TOOLS} xmltree)

#
ADD_EXECUTABLE(regexfind regexfind.cpp)
target_link_libraries(regexfind ${Boost_SYSTEM_LIBRARY} ${Boost_FILESYSTEM_LIBRARY} ${Boost_REGEX_LIBRARY})
MESSAGE(STATUS "\tregexfind")
SET(BUILT_TOOLS ${BUILT_TOOLS} regexfind)


SET_TARGET_PROPERTIES(${BUILT_TOOLS} PROPERTIES
   BUILD_WITH_INSTALL_RPATH ON
   INSTALL_RPATH_USE_LINK_PATH 1
   INSTALL_RPATH ${CMAKE_INSTALL_PREFIX}/lib
)

INSTALL(
  TARGETS ${BUILT_TOOLS}
  RUNTIME DESTINATION bin COMPONENT applications
)



configure_file("${CMAKE_CURRENT_SOURCE_DIR}/create_dcl.py" "${CMAKE_BINARY_DIR}/create_dcl" IMMEDIATE @ONLY)
configure_file("${CMAKE_CURRENT_SOURCE_DIR}/create_component.py" "${CMAKE_BINARY_DIR}/create_component" IMMEDIATE @ONLY)
configure_file("${CMAKE_CURRENT_SOURCE_DIR}/diswizard.py" "${CMAKE_BINARY_DIR}/diswizard" IMMEDIATE @ONLY)
configure_file("${CMAKE_CURRENT_SOURCE_DIR}/diswizard_library.py" "${CMAKE_BINARY_DIR}/diswizard_library.py" IMMEDIATE @ONLY)
configure_file("${CMAKE_CURRENT_SOURCE_DIR}/discode_helper.py" "${CMAKE_BINARY_DIR}/discode_helper.py" IMMEDIATE @ONLY)

INSTALL(
  PROGRAMS 
	${CMAKE_BINARY_DIR}/create_dcl 
	${CMAKE_BINARY_DIR}/create_component 
	${CMAKE_BINARY_DIR}/diswizard 
	${CMAKE_BINARY_DIR}/discode_helper.py
  DESTINATION bin COMPONENT applications
) 

install(
  FILES ${CMAKE_CURRENT_SOURCE_DIR}/diswizard.ui
	${CMAKE_CURRENT_SOURCE_DIR}/diswizard_library.ui
	${CMAKE_CURRENT_SOURCE_DIR}/Library.py
	${CMAKE_BINARY_DIR}/diswizard_library.py
  DESTINATION bin
)
