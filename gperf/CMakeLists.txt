ExternalProject_Add(
	gperf
	#GIT_REPOSITORY https://github.com/roboticslibrary/gperf.git
	#GIT_TAG cmake-3.1
	URL https://github.com/roboticslibrary/gperf/archive/cmake-3.1.tar.gz
	#URL ${CMAKE_CURRENT_SOURCE_DIR}/gperf-cmake-3.1.tar.gz
	URL_MD5 ccdc42c8b534061030d49bb9cae9cfd5
	CMAKE_ARGS
		-DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
		-DCMAKE_CFG_INTDIR=${CMAKE_CFG_INTDIR}
		-DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}
		-DCMAKE_PREFIX_PATH=${CMAKE_PREFIX_PATH}
		-DCMAKE_TRY_COMPILE_CONFIGURATION=${CMAKE_TRY_COMPILE_CONFIGURATION}
	INSTALL_DIR ${CMAKE_INSTALL_PREFIX}
)

ExternalProject_Add_Step(
	gperf license
	DEPENDEES build
	COMMAND ${CMAKE_COMMAND} -E copy <SOURCE_DIR>/COPYING ${CMAKE_INSTALL_FULL_DATADIR}/gperf/COPYING
)
