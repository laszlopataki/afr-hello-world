# afr-hello-world
This is an example project for Amazon FreeRTOS as a submodule

## Install environment
Follow AWS guide at https://docs.aws.amazon.com/freertos/latest/userguide/getting_started_espressif.html

## Create shortcut to `freertos/vendors/espressif/esp-idf` 
1. Open `C:\Users\John\.espressif\esp_idf.json`  
2. Add a new item to `idfInstalled` list as below  
  
  ```
    "esp-idf-7f645c11ccc057733dd6247d1da48a39": {
    "version": "4.2",
    "python": "C:/Users/John/.espressif/python_env/idf4.2_py3.8_env/Scripts/python.exe",
    "path": "C:/work/afr-hello-world/freertos/vendors/espressif/esp-idf/"
}
  ```  

3. Create a copy of the `ESP-IDF 4.2 PS.lnk` and fill the properties as  

3.1 Target
```
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Bypass -NoExit -File "C:\Users\Laszlo\.espressif/Initialize-Idf.ps1" -IdfId esp-idf-7f645c11ccc057733dd6247d1da48a38
```

3.2 Start in       
```
c:\work\embedded_workspace\afr-hello-world
```  

## Compile
- run `ESP-IDF 4.2 PS.lnk` 
- `cmake -S . -B build -DCMAKE_TOOLCHAIN_FILE="freertos/tools/cmake/toolchains/xtensa-esp32.cmake" -GNinja`
- `idf.py build`

### One liner clean build with tracealyzer
```
rm -r .\build;cmake -S . -B build -DCONFIG_FREERTOS_UNICORE=1 -DCMAKE_TOOLCHAIN_FILE="freertos/tools/cmake/toolchains/xtensa-esp32.cmake" -GNinja;idf.py build
```