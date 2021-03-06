add_library(emcrk-lib SHARED
	r40.c
	cfg.c
	kfind.c
	names.c
	process.c
	exl.c
	obj.c
)

set_target_properties(emcrk-lib PROPERTIES
	OUTPUT_NAME "emcrk"
	SOVERSION ${APP_VERSION_MAJOR}.${APP_VERSION_MINOR}
)

install(TARGETS emcrk-lib
	LIBRARY DESTINATION lib
	ARCHIVE DESTINATION lib
	PUBLIC_HEADER DESTINATION include
)

install(FILES
	${CMAKE_SOURCE_DIR}/include/r40.h
	${CMAKE_SOURCE_DIR}/include/process.h
	${CMAKE_SOURCE_DIR}/include/kfind.h
	${CMAKE_SOURCE_DIR}/include/cfg.h
	${CMAKE_SOURCE_DIR}/include/obj.h
	${CMAKE_SOURCE_DIR}/include/exl.h
	DESTINATION include/emcrk
)

add_executable(crkfind
	crkfind.c
)

add_executable(r40
	r40tool.c
)

target_link_libraries(crkfind emcrk-lib)
target_link_libraries(r40 emcrk-lib)

install(TARGETS crkfind
	RUNTIME DESTINATION bin
)

install(TARGETS r40
	RUNTIME DESTINATION bin
)

# vim: tabstop=4
