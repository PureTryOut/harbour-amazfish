cmake_minimum_required(VERSION 3.13.0)

project(harbour-amazfish
	VERSION 1.7.2
	DESCRIPTION "Companion application for various smartwatches")

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

include(FeatureSummary)
include(GNUInstallDirs)

option(FLAVOR "Supported platforms: kirigami, silica, qtcontrols, ubports" silica)

set(QT_MIN_VERSION "5.6.0")
set(KF5_MIN_VERSION "5.75.0")
find_package(Qt5 ${QT_MIN_VERSION} COMPONENTS Qml Bluetooth Location REQUIRED)
find_package(PkgConfig REQUIRED)
find_package(KF5Contacts ${KF5_MIN_VERSION} CONFIG REQUIRED)
find_package(KDb CONFIG REQUIRED)
find_package(DBus1 CONFIG REQUIRED)

pkg_check_modules(MPRIS-QT mpris-qt5 REQUIRED IMPORTED_TARGET)

if(MPRIS-QT_FOUND)
	set_property(GLOBAL APPEND PROPERTY PACKAGES_FOUND mpris-qt5)
else()
	set_property(GLOBAL APPEND PROPERTY PACKAGES_NOT_FOUND mpris-qt5)
endif()

add_subdirectory(lib)
add_subdirectory(daemon)
#add_subdirectory(ui)

feature_summary(WHAT ALL FATAL_ON_MISSING_REQUIRED_PACKAGES)
