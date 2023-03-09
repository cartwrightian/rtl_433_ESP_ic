Fork of rtl_443_ESP to experiment with getting current cost device working.

Works ok but not tested with any other devices, purely an experiment and no plans to add other devices etc. 

No attempt to tune sx1278 parameters as PSK worked and this device out of the box.

For openmqttgateway

platformio.ini

change rtl_433_ESP to
rtl_433_ESP = https://github.com/cartwrightian/rtl_433_ESP_ic

environments.ini

[env:lilygo-rtl_433]
;build_type = debug not helping
platform = ${com.esp32_platform}
board = ttgo-lora32-v21
; https://docs.platformio.org/en/latest/boards/espressif32/ttgo-lora32-v2.html
; ~/.platformio/packages/framework-arduinoespressif32/variants/.../pins_arduino.h
board_build.partitions = min_spiffs.csv
lib_deps =
  ${com-esp.lib_deps}
  ${libraries.wifimanager32}
  ${libraries.ssd1306}
  ${libraries.rtl_433_ESP}
build_flags =
  ${com-esp.build_flags}
; *** OpenMQTTGateway Config ***
  ;'-UZmqttDiscovery'          ; disables MQTT Discovery
  '-DvalueAsATopic=true'    ; MQTT topic includes model and device
  '-DGateway_Name="OpenMQTTGateway_lilygo_rtl_433_ESP"'
; *** OpenMQTTGateway Modules ***
  '-DZgatewayRTL_433="rtl_433"'
  '-DZradioSX127x="SX127x"'
; *** ssd1306 Display Options ***
  '-DZdisplaySSD1306="LilyGo_SSD1306"'
;  '-DLOG_TO_OLED=true'         ; Enable log to OLED
;  '-DJSON_TO_OLED=true'
;  '-DLOG_LEVEL_OLED=LOG_LEVEL_INFO'
;  '-DDISPLAY_IDLE_LOGO=false'
;  '-DDISPLAY_BRIGHTNESS=80'
;  '-DDISPLAY_METRIC=false'
;  '-DRTL_DEBUG=1'             ; rtl_433 verbose mode
;  '-DDEMOD_DEBUG'
  '-DMY_DEVICES=true'
  '-DENABLE_FSK_PULSE_PCM=true'
  ;'-DPUBLISH_UNPARSED=true'
;  '-DCURRENT_COST_DEBUG=true'
;  '-DRF_MODULE_INIT_STATUS'
