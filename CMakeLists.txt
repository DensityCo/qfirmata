CMAKE_MINIMUM_REQUIRED (VERSION 3.10)

SET(CMAKE_EXECUTABLE_LIBRARY_PREFIX)
SET(CMAKE_EXECUTABLE_LIBRARY_SUFFIX)
project(qfirmata)
find_package(Qt5 REQUIRED COMPONENTS Widgets)
set(QT_QMAKE_EXECUTABLE ${INSTALL_DIR}/bin/qmake)
set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_CXX_FLAGS_RELEASE "-Werror=implicit-function-declaration -Wfatal-errors -O0 -ggdb -g3 -fpic -Wall")# -Werror")
set(CMAKE_CXX_FLAGS_DEBUG   "-Werror=implicit-function-declaration -Wfatal-errors -O0 -ggdb -g3 -fpic -Wall") # -Werror")
set(CMAKE_C_FLAGS_DEBUG     "-Werror=implicit-function-declaration -Wfatal-errors -O0 -ggdb -g3 -fpic -Wall") # -shared -Werror")
set(CMAKE_C_FLAGS_RELEASE   "-Werror=implicit-function-declaration -Wfatal-errors -O0 -fpic -shared -Wall") # -Werror")

set(LIB_QFIRMATA_SOURCES src/firmata.cpp src/backends/backend.cpp src/backends/serialinfo.cpp src/backends/serialport.cpp src/pins/analogpin.cpp src/pins/digitalpin.cpp src/pins/encoder.cpp src/pins/i2c.cpp src/pins/pin.cpp src/pins/pwmpin.cpp src/pins/servo.cpp)
set(LIB_QFIRMATA_HEADERS src/firmata.h src/backends/backend.h src/backends/serialinfo.h src/backends/serialport.h src/pins/analogpin.h src/pins/digitalpin.h src/pins/encoder.h src/pins/i2c.h src/pins/pin.h src/pins/pwmpin.h src/pins/servo.h)

set(PROJECT_SOURCE_FILES ${LIB_QFIRMATA_SOURCES})

set(QT_LIBRARIES
    Qt5Gui
    Qt5Core
    Qt5Widgets
    QtSerialPort
)

add_library(qfirmata ${LIB_QFIRMATA_SOURCES} ${LIB_QFIRMATA_HEADERS})
include_directories(qfirmata ${CMAKE_PREFIX_PATH}/include ${CMAKE_PREFIX_PATH}/include/QtWidgets ${CMAKE_PREFIX_PATH}/include/QtCore ${CMAKE_PREFIX_PATH}/include/QtSerialPort)
target_link_libraries(qfirmata ${QT_LIBRARIES})

install(TARGETS qfirmata DESTINATION lib)
install(FILES ${QFIRMATA_HEADERS} DESTINATION include/qfirmata)


