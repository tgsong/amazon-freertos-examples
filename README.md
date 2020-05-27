# Amazon FreeRTOS Examples

This repo shows how to set up a CMake project for ESP32 and use amazon freertos as an external library.

See the official document for software prerequisite, https://docs.aws.amazon.com/freertos/latest/userguide/getting_started_espressif.html

Build instruction,

```sh
cmake -S . -B build -DCMAKE_TOOLCHAIN_FILE=freertos/tools/cmake/toolchains/xtensa-esp32.cmake -GNinja
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

## Troubleshooting

### Linker Error: undefined reference to <some_function>

If you changed some configuartion and run into this, usually it's  because of missing dependent libraries/demos. To fix it, first find out which CMake target the missing functions belong to, normally it should be in the `CMakeLists.txt` closest to the source file where the functions are defined. Then add the CMake target to your application dependency list using the `target_link_libraries` command in the root level `CMakeLists.txt`. For example,

1. Linker complains about `undefined reference to NumericComparisonInit`.
1. `NumericComparisonInit` is defined in `amazon-freertos/demos/ble/iot_ble_numericComparison.c`.
1. `amazon-freertos/demos/ble/CMakeLists.txt` defines the target `ble_numeric_comparison` which has this source file.
1. Link `AFR::demo_ble_numeric_comparison` target with `target_link_libraries` to your application target. (`demo_` prefix is added because it's a demo module, all target names can be found in the summary of CMake output)
