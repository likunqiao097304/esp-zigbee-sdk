cmake_minimum_required(VERSION 3.16)

idf_component_register(
    INCLUDE_DIRS include
)

if(CONFIG_ZB_ENABLED)

    set(ESP_ZIGBEE_API_LIBS "")

    if(CONFIG_ZB_ZCZR)
    add_prebuilt_library(esp_zigbee_api_lib "${CMAKE_CURRENT_SOURCE_DIR}/lib/${idf_target}/libesp_zb_api_zczr.a" PRIV_REQUIRES espressif__esp-zboss-lib)
    elseif(CONFIG_ZB_ZED)
    add_prebuilt_library(esp_zigbee_api_lib "${CMAKE_CURRENT_SOURCE_DIR}/lib/${idf_target}/libesp_zb_api_zed.a" PRIV_REQUIRES espressif__esp-zboss-lib)
    endif()

    list(APPEND ESP_ZIGBEE_API_LIBS esp_zigbee_api_lib)

    target_link_libraries(${COMPONENT_LIB} INTERFACE ${ESP_ZIGBEE_API_LIBS})
    target_compile_options(${COMPONENT_LIB} INTERFACE "-Wno-strict-prototypes")
endif()
