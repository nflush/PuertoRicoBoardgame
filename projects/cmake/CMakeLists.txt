cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

# Widgets finds its own dependencies (QtGui and QtCore).
find_package(Qt5Widgets REQUIRED)
#find_package(Qt5Declarative)

project(PuertoRico)

# Call MOC when it's necessary
set(CMAKE_AUTOMOC ON)

# Les fichiers g�n�r�s par le moc sont g�n�r�s dans le dossier bin, dire � CMake de toujours 	
# inclure les ent�tes de ce dossier
SET(CMAKE_INCLUDE_CURRENT_DIR ON)

aux_source_directory(../../src)
add_executable(${PROJECT} ${SRC_LIST})


# Tell CMake to run moc when necessary:
set(CMAKE_AUTOMOC ON)

# As moc files are generated in the binary dir, tell CMake
# to always look for includes there:
set(CMAKE_INCLUDE_CURRENT_DIR ON)


find_package(Qt5Widgets REQUIRED)

# The Qt5Widgets_INCLUDES also includes the include directories for
# dependencies QtCore and QtGui
include_directories(${Qt5Widgets_INCLUDES})

# We need add -DQT_WIDGETS_LIB when using QtWidgets in Qt 5.
add_definitions(${Qt5Widgets_DEFINITIONS})

# Executables fail to build with Qt 5 in the default configuration
# without -fPIE. We add that here.
set(CMAKE_CXX_FLAGS "${Qt5Widgets_EXECUTABLE_COMPILE_FLAGS}")

add_executable(hello_world main.cpp mainwindow.cpp)

# The Qt5Widgets_LIBRARIES variable also includes QtGui and QtCore
target_link_libraries(hello_world ${Qt5Widgets_LIBRARIES})

 qt5_use_modules(hello_world Widgets)
