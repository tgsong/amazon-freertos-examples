# Amazon FreeRTOS Examples

This repo shows how to set up a CMake project for ESP32 and use amazon freertos as an external library.

See the official document for software prerequisite, https://docs.aws.amazon.com/freertos/latest/userguide/getting_started_espressif.html

Build instruction,

```sh
cmake -S . -B build -DCMAKE_TOOLCHAIN_FILE=amazon-freertos/tools/cmake/toolchains/xtensa-esp32.cmake -GNinja
```

To flash,

```sh
cmake --build build --target flash
```

To monitor the output,

```sh
export ESPPORT <replace-with-serial-port-of-ESP32>
amazon-freertos/vendors/espressif/esp-idf/tools/idf.py monitor
```
