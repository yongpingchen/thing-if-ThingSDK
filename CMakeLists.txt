CMAKE_MINIMUM_REQUIRED(VERSION 3.5)
PROJECT(kiithingifsdk C)
SET(CMAKE_C_FLAGS "-Wall")
SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DKII_PUSH_KEEP_ALIVE_INTERVAL_SECONDS=300")
SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DKII_JSON_FIXED_TOKEN_NUM=128")
# Uncomment it if you need to use unsecure connection.
#SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DKII_MQTT_USE_PORT_TCP=1")
SET(CMAKE_C_FLAGS_RELEASE "-O2")
SET(CMAKE_C_FLAGS_DEBUG "-g -DDEBUG")

FILE(GLOB srcs ./*.c kii/kii-core/*.c kii/kii/*.c kii/kii_json/src/*.c kii/lib/jsmn/jsmn.c)
ADD_LIBRARY(kiithingifsdk SHARED ${srcs})
TARGET_INCLUDE_DIRECTORIES(kiithingifsdk PRIVATE ${PROJECT_SOURCE_DIR} kii/kii kii/kii-core kii/kii_json/include kii/lib/jsmn)
TARGET_INCLUDE_DIRECTORIES(kiithingifsdk PUBLIC ${PROJECT_SOURCE_DIR}/include)
SET(version "1.0.1")
SET(soversion "1.0.0")
SET_TARGET_PROPERTIES(kiithingifsdk PROPERTIES VERSION ${version} SOVERSION ${soversion})
INSTALL(FILES include/kii_thing_if.h kii/kii/kii.h kii/kii/kii_task_callback.h kii/kii-core/kii_socket_callback.h kii/kii-core/kii_core.h kii/kii_json/include/kii_json.h kii/kii_json/libs/jsmn/jsmn.h DESTINATION include)
INSTALL(TARGETS kiithingifsdk LIBRARY DESTINATION lib)
