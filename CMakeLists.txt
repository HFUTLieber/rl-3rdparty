cmake_minimum_required(VERSION 2.8.12)

project(3rdparty)

include(ExternalProject)
include(GNUInstallDirs)

option(BUILD_SHARED_LIBS "Build shared libraries" ON)

list(INSERT CMAKE_PREFIX_PATH 0 ${CMAKE_INSTALL_PREFIX})

add_subdirectory(atidaq)
add_subdirectory(boost)
add_subdirectory(bullet3)
add_subdirectory(coin)
add_subdirectory(eigen3)
add_subdirectory(gperf)
add_subdirectory(libccd)
add_subdirectory(nlopt)
add_subdirectory(ode)
add_subdirectory(pqp)
add_subdirectory(simage)
add_subdirectory(solid3)
add_subdirectory(xz)
add_subdirectory(zlib)

add_subdirectory(fcl)
add_subdirectory(libiconv)
add_subdirectory(soqt)

add_subdirectory(libxml2)

add_subdirectory(libxslt)

set(
	CPACK_INSTALL_CMAKE_PROJECTS
	"${CMAKE_CURRENT_BINARY_DIR}/atidaq/atidaq-prefix/src/atidaq-build;atidaq;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/bullet3/bullet3-prefix/src/bullet3-build;bullet3;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/coin/coin-prefix/src/coin-build;coin;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/eigen3/eigen3-prefix/src/eigen3-build;eigen3;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/fcl/fcl-prefix/src/fcl-build;fcl;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/libccd/libccd-prefix/src/libccd-build;libccd;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/libiconv/libiconv-prefix/src/libiconv-build;libiconv;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/libxml2/libxml2-prefix/src/libxml2-build;libxml2;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/libxslt/libxslt-prefix/src/libxslt-build;libxslt;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/nlopt/nlopt-prefix/src/nlopt-build;nlopt;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/ode/ode-prefix/src/ode-build;ode;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/pqp/pqp-prefix/src/pqp-build;pqp;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/simage/simage-prefix/src/simage-build;simage;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/solid3/solid3-prefix/src/solid3-build;solid3;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/soqt/soqt-prefix/src/soqt-build;soqt;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/xz/xz-prefix/src/xz-build;xz;ALL;/"
	"${CMAKE_CURRENT_BINARY_DIR}/zlib/zlib-prefix/src/zlib-build;zlib;ALL;/"
)

set(
	CPACK_INSTALLED_DIRECTORIES
	${CMAKE_CURRENT_BINARY_DIR}/boost/boost-prefix/src/boost/boost ${CMAKE_INSTALL_INCLUDEDIR}/boost
)

if(MSVC)
	if(CMAKE_CXX_COMPILER_VERSION MATCHES "^([0-9]+)\\.([0-9])([0-9]*)\\.([0-9]+)\\.")
		if(CMAKE_CXX_COMPILER_VERSION VERSION_GREATER 18)
			math(EXPR LINKER_VERSION_MAJOR "${CMAKE_MATCH_1} - 5")
		else()
			math(EXPR LINKER_VERSION_MAJOR "${CMAKE_MATCH_1} - 6")
		endif()
		set(PLATFORM_TOOLSET_MAJOR ${LINKER_VERSION_MAJOR})
		set(PLATFORM_TOOLSET_MINOR ${CMAKE_MATCH_2})
		set(LINKER_VERSION "${LINKER_VERSION_MAJOR}.${CMAKE_MATCH_2}${CMAKE_MATCH_3}.${CMAKE_MATCH_4}")
	endif()
	if(CMAKE_CL_64)
		set(CPACK_PACKAGE_FILE_NAME "rl-3rdparty-msvc-${PLATFORM_TOOLSET_MAJOR}.${PLATFORM_TOOLSET_MINOR}-x64")
		set(CPACK_PACKAGE_INSTALL_DIRECTORY "Robotics Library\\\\3rdparty\\\\MSVC\\\\${PLATFORM_TOOLSET_MAJOR}.${PLATFORM_TOOLSET_MINOR}\\\\x64")
		set(CPACK_PACKAGE_NAME "Robotics Library Third-Party Dependencies - MSVC ${PLATFORM_TOOLSET_MAJOR}.${PLATFORM_TOOLSET_MINOR} (x64)")
	else()
		set(CPACK_PACKAGE_FILE_NAME "rl-3rdparty-msvc-${PLATFORM_TOOLSET_MAJOR}.${PLATFORM_TOOLSET_MINOR}-x86")
		set(CPACK_PACKAGE_INSTALL_DIRECTORY "Robotics Library\\\\3rdparty\\\\MSVC\\\\${PLATFORM_TOOLSET_MAJOR}.${PLATFORM_TOOLSET_MINOR}\\\\x86")
		set(CPACK_PACKAGE_NAME "Robotics Library Third-Party Dependencies - MSVC ${PLATFORM_TOOLSET_MAJOR}.${PLATFORM_TOOLSET_MINOR} (x86)")
	endif()
else()
	set(CPACK_PACKAGE_FILE_NAME "rl-3rdparty-${CMAKE_SYSTEM_NAME}")
	set(CPACK_PACKAGE_INSTALL_DIRECTORY "rl-3rdparty")
	set(CPACK_PACKAGE_NAME "Robotics Library Third-Party Dependencies")
endif()

set(CPACK_DEBIAN_PACKAGE_HOMEPAGE "https://www.roboticslibrary.org/contact")
set(CPACK_DEBIAN_PACKAGE_NAME "librl-3rdparty")
set(CPACK_DEBIAN_PACKAGE_SECTION "devel")
set(CPACK_NSIS_DISPLAY_NAME ${CPACK_PACKAGE_NAME})
set(CPACK_NSIS_EXECUTABLES_DIRECTORY ${CMAKE_INSTALL_BINDIR})
set(CPACK_NSIS_HELP_LINK "https://www.roboticslibrary.org/contact")
set(CPACK_NSIS_INSTALLED_ICON_NAME Uninstall.exe)
set(CPACK_NSIS_MODIFY_PATH ON)
set(CPACK_NSIS_MUI_ICON ${CMAKE_CURRENT_SOURCE_DIR}/robotics-library.ico)
set(CPACK_NSIS_MUI_UNIICON ${CMAKE_CURRENT_SOURCE_DIR}/robotics-library.ico)
set(CPACK_NSIS_PACKAGE_NAME ${CPACK_PACKAGE_NAME})
set(CPACK_NSIS_URL_INFO_ABOUT "https://www.roboticslibrary.org/contact")
set(CPACK_PACKAGE_CONTACT "Robotics Library Team <roblib-developers@lists.sourceforge.net>")
set(CPACK_PACKAGE_VENDOR "Robotics Library")
set(CPACK_PROJECT_CONFIG_FILE ${CMAKE_CURRENT_SOURCE_DIR}/CPackProjectConfig.cmake)
set(CPACK_RPM_PACKAGE_GROUP "Development/Libraries")
set(CPACK_RPM_PACKAGE_NAME "rl-3rdparty")
set(CPACK_RPM_PACKAGE_SUMMARY "Robotics Library Third-Party Dependencies")
set(CPACK_RPM_PACKAGE_URL "https://www.roboticslibrary.org/contact")
set(CPACK_WIX_EXTENSIONS "WiXUtilExtension")
set(
	CPACK_WIX_EXTRA_SOURCES
	${CMAKE_CURRENT_BINARY_DIR}/WixExtra.wxs
	${CMAKE_CURRENT_SOURCE_DIR}/WixUI_FeatureTreeNoLicense.wxs
)
set(CPACK_WIX_PATCH_FILE ${CMAKE_CURRENT_BINARY_DIR}/WixPatch.xml)
set(CPACK_WIX_PRODUCT_ICON ${CMAKE_CURRENT_SOURCE_DIR}/robotics-library.ico)
set(CPACK_WIX_PROGRAM_MENU_FOLDER ${CPACK_PACKAGE_NAME})
set(CPACK_WIX_PROPERTY_ARPHELPLINK "https://www.roboticslibrary.org/contact")
set(CPACK_WIX_PROPERTY_ARPURLINFOABOUT "https://www.roboticslibrary.org/")
set(CPACK_WIX_ROOT_FEATURE_TITLE "Robotics Library Third-Party Dependencies")
set(CPACK_WIX_UI_BANNER ${CMAKE_CURRENT_SOURCE_DIR}/WixUIBanner.bmp)
set(CPACK_WIX_UI_DIALOG ${CMAKE_CURRENT_SOURCE_DIR}/WixUIDialog.bmp)
set(CPACK_WIX_UI_REF "WixUI_FeatureTreeNoLicense")
set(CPACK_WIX_UPGRADE_GUID D604D1B7-3760-447A-A275-A78CAEA8B5D9)

configure_file(WixExtra.wxs.in ${CMAKE_CURRENT_BINARY_DIR}/WixExtra.wxs)
configure_file(WixPatch.xml.in ${CMAKE_CURRENT_BINARY_DIR}/WixPatch.xml)

set(CMAKE_INSTALL_SYSTEM_RUNTIME_COMPONENT system)
include(InstallRequiredSystemLibraries)

include(CPack)
