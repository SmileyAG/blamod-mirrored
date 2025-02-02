cmake_minimum_required(VERSION 3.1)

project(Blamod)

set(CPACK_GENERATOR "ZIP")
set(CPACK_PACKAGE_NAME "blamod")
set(CPACK_PACKAGE_VERSION "2.0-alpha14")
set(CPACK_PACKAGE_VERSION_MAJOR "0")
set(CPACK_PACKAGE_VERSION_MINOR "14")
set(CPACK_PACKAGE_VERSION_PATCH "0")
set(CPACK_INCLUDE_TOPLEVEL_DIRECTORY FALSE)

set(CMAKE_INSTALL_DEFAULT_COMPONENT_NAME "blamod")

# CPack settings
set(CPACK_BINARY_7Z OFF)
set(CPACK_BINARY_IFW OFF)
set(CPACK_BINARY_NSIS OFF)
set(CPACK_BINARY_WIX OFF)
set(CPACK_BINARY_ZIP ON)

set(CPACK_SOURCE_7Z OFF)
set(CPACK_SOURCE_ZIP OFF)

set(BLAMOD_VERSION "${CPACK_PACKAGE_VERSION}")

include(CPack)

if (MSVC)
	add_definitions("/D_WIN32")

	set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} /MANIFEST:NO")
	set(CMAKE_SHARED_LINKER_FLAGS_RELEASE "/INCREMENTAL:NO /OPT:ICF /OPT:REF")

	set(CMAKE_STATIC_LINKER_FLAGS_DEBUG "${CMAKE_STATIC_LINKER_FLAGS_DEBUG} /DEBUG")
	set(CMAKE_STATIC_LINKER_FLAGS_RELWITHDEBINFO "${CMAKE_STATIC_LINKER_FLAGS_RELWITHDEBINFO} /DEBUG")

	# compiler flags
	set(CMAKE_CXX_FLAGS "/DWIN32 /D_WINDOWS /W3 /GR /D_WIN32 /GF /arch:SSE /GS- /fp:fast")
	set(CMAKE_CXX_FLAGS_DEBUG "/D_DEBUG /MTd /Zi /Ob0 /Od")
	set(CMAKE_CXX_FLAGS_MINSIZEREL "/MT /O1 /Ob1 /D NDEBUG")
	set(CMAKE_CXX_FLAGS_RELEASE "/MT /O2 /Ob2 /D NDEBUG /Oi /Gy /Ot")
	set(CMAKE_CXX_FLAGS_RELWITHDEBINFO "/MT /Zi /O2 /Ob1 /D NDEBUG")
endif()

add_subdirectory(src)

add_subdirectory(game/blamod)
