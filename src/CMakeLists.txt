#CMake file for osc2midi

cmake_minimum_required(VERSION 2.8)

project (rbdrum2midi)

set(CMAKE_C_FLAGS "-Wall -g")

# check for our various libraries
find_package(PkgConfig)
find_package(Jack REQUIRED)
find_package(ALSA REQUIRED)
find_package(libusb-1.0 REQUIRED)

include_directories (${JACK_INCLUDE_DIRS} ${ALSA_INCLUDE_DIRS} ${LIBUSB_1_INCLUDE_DIRS})
link_directories (${JACK_LIBRARY_DIRS} ${ALSA_LIBRARY_DIRS} ${LIBUSB_1_INCLUDE_DIRS})

# config libraries

add_executable(rbdrum2midi
  jackdriver.c
  main.c
  alsadriver.c
  ghkit.c
  jackdriver.c
  rb1kit.c
  rbkit.c
  rb3keyboard.c
  rbguitar.c
)


target_link_libraries(rbdrum2midi ${JACK_LIBRARIES} ${ALSA_LIBRARIES} ${LIBUSB_1_LIBRARIES} m)

# config install
install(TARGETS rbdrum2midi
  DESTINATION bin
)

