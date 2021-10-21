project(obs-ndi VERSION 4.9.0)

if(MSVC)
	set(obs-ndi_PLATFORM_DEPS
		w32-pthreads)
endif()

set(obs-ndi_SOURCES
	src/obs-ndi.cpp
	src/obs-ndi-source.cpp
	src/obs-ndi-output.cpp
	src/obs-ndi-filter.cpp
	src/premultiplied-alpha-filter.cpp
	src/main-output.cpp
	src/preview-output.cpp
	src/Config.cpp
	src/forms/output-settings.cpp)

set(obs-ndi_HEADERS
	src/obs-ndi.h
	src/main-output.h
	src/preview-output.h
	src/Config.h
	src/forms/output-settings.h)

qt5_wrap_ui(obs-ndi_UI_HEADERS "src/forms/output-settings.ui")

add_library(obs-ndi MODULE
	${obs-ndi_SOURCES}
	${obs-ndi_HEADERS}
	${obs-ndi_UI_HEADERS})

include_directories("lib/ndi")

target_link_libraries(obs-ndi
	libobs
	obs-frontend-api
	Qt5::Core
	Qt5::Widgets
	${obs-ndi_PLATFORM_DEPS})

set_target_properties(obs-ndi PROPERTIES FOLDER "plugins/exeldro")
install_obs_plugin_with_data(obs-ndi data)