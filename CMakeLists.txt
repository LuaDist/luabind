# Copyright (C) 2007-2012 LuaDist.
# Modified by Peter Kapec
# Redistribution and use of this file is allowed according to the terms of the MIT license.
# For details see the COPYRIGHT file distributed with LuaDist.
# Please note that the package source code is licensed under its own license.
# Original build script by Leandro Motta Barros.

project ( luabind NONE )
cmake_minimum_required ( VERSION 2.8 )
include ( cmake/dist.cmake )
include ( lua )

# Find Boost
set ( Boost_USE_STATIC_LIBS OFF )
#~ 	FIND_PACKAGE(Boost 1.38 COMPONENTS unit_test_framework REQUIRED)
find_package ( Boost 1.38 REQUIRED )

# Include directories
include_directories ( ${Boost_INCLUDE_DIRS} ${LUA_INCLUDE_DIR} ${CMAKE_CURRENT_SOURCE_DIR} )

# Link directories
#~ 	LINK_DIRECTORIES(${BOOST_LIBRARY_DIRS})

# Build the library
file ( GLOB LUABIND_SRC "src/*.cpp" )

add_definitions ( -DLUABIND_BUILDING )

add_library ( luabind ${LUABIND_SRC} )
target_link_libraries ( luabind ${LUA_LIBRARIES} )

#~ 2TODO: Tests

# Add CTest support
#~ 	ENABLE_TESTING()

# Unit tests
#~ 	FUNCTION(AddUnitTest name)
#~ 		ADD_EXECUTABLE(${name} Tests/${name}.cpp)
#~ 		TARGET_LINK_LIBRARIES(${name} ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY} ${LUA_LIBRARIES} diluculum)
#~ 		ADD_TEST(${name} ${name})
#~ 	ENDFUNCTION(AddUnitTest)

#~ 	ADD_LIBRARY(ATestModule Tests/ATestModule.cpp)
#~ 	TARGET_LINK_LIBRARIES(ATestModule diluculum ${LUA_LIBRARIES})
#~ 	SET_TARGET_PROPERTIES(ATestModule PROPERTIES PREFIX "")

#~ 	AddUnitTest(TestLuaFunction)

# Build examples
#~ 	FUNCTION(AppExample name sources includes)
#~ 		INCLUDE_DIRECTORIES(${includes})
#~ 		ADD_EXECUTABLE(${name} ${sources})
#~ 		TARGET_LINK_LIBRARIES(${name} luabind)
#~ 	ENDFUNCTION(AppExample)

#~ 	AppExample(any_converter "examples/any_converter/any_converter.cpp" "" )
#~ 	AppExample(filesystem "examples/filesystem/filesystem.cpp" "examples/filesystem" )
#~ 	AppExample(glut "examples/glut/glut_bind.cpp" "" )
#~ 	AppExample(hello_world "examples/hello_world/hello_world.cpp" "" )
#~ 	AppExample(intrusive_ptr "examples/intrusive_ptr/intrusive_ptr.cpp" "" )
#~ 	AppExample(regexp "examples/regexp/regex_wrap.cpp" "" )

# Install
install_library ( luabind )
install_header ( luabind )
install_data ( LICENSE INSTALL )
install_doc ( doc/ )

