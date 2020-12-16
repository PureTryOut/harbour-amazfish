set(SRC
	src/amazfishconfig.cpp
	src/weather/city.cpp
	src/weather/citymanager.cpp
	src/weather/citysearchmodel.cpp
	src/weather/currentweather.cpp)
set(HEADERS
	src/amazfishconfig.h
	src/weather/apikey.h
	src/weather/city.h
	src/weather/citymanager.h
	src/weather/citysearchmodel.h
	src/weather/currentweather.h)

add_library(amazfish SHARED ${SRC} ${HEADERS})

target_link_libraries(amazfish
	Qt5::Core
	Qt5::Network)
