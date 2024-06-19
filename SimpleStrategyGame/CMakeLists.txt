#vcpkg
if(DEFINED ENV{VCPKG_HOME})
    include("$ENV{VCPKG_HOME}/scripts/buildsystems/vcpkg.cmake")
else()
    include("$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake")
endif()
#vcpkg

#exe
file(GLOB_RECURSE SOURCES "src/*.cpp"  "include/*.h")
add_executable (${CMAKE_PROJECT_NAME}  ${SOURCES})
#exe


#find packages
find_package(imgui CONFIG REQUIRED)

find_package(SDL2 CONFIG REQUIRED)
find_package(SDL2_image CONFIG REQUIRED)
find_package(SDL2_mixer CONFIG REQUIRED)
find_package(SDL2_net CONFIG REQUIRED)
find_package(SDL2_ttf CONFIG REQUIRED)
find_package(SDL2-gfx CONFIG REQUIRED)

find_package(Boost CONFIG REQUIRED)
find_package(box2d CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)
find_package(jsoncpp CONFIG REQUIRED)
find_package(unofficial-lunasvg CONFIG REQUIRED)
find_package(PugiXML CONFIG REQUIRED)
find_package(spdlog CONFIG REQUIRED)
#find packages

#linking libraries
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE imgui::imgui)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE pugixml::shared pugixml::pugixml)

target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE box2d::box2d)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE JsonCpp::JsonCpp)
#target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE tmxlite) нужно исправить
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE spdlog::spdlog_header_only)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE spdlog::spdlog)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE unofficial::lunasvg::lunasvg)

target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE SDL2::SDL2 SDL2::SDL2main)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE SDL2_image::SDL2_image)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE SDL2_mixer::SDL2_mixer)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE SDL2_ttf::SDL2_ttf)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE SDL2_net::SDL2_net)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE SDL2::SDL2_gfx)
#linking libraries


if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET ${CMAKE_PROJECT_NAME} PROPERTY CXX_STANDARD 20)
endif()

#Resources copy
set(SOURCE_DIR ${CMAKE_SOURCE_DIR}/Resources)
set(DESTINATION_DIR ${CMAKE_BINARY_DIR}/${CMAKE_PROJECT_NAME})
file(COPY ${SOURCE_DIR} DESTINATION ${DESTINATION_DIR})
#Resources copy