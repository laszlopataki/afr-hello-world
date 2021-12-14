# afr-hello-world
This is a base project for Amazon FreeRTOS

# Notes:
- In FreeRTOSConfig.h you can disable/enable FreeRTOS hooks.
-  

# Start a new project
- Create an empty repo on the version control provider's website 
- Clone the empty repo
- Copy the following files from `afr-hello-world`
  - .gitignore
  - .gitattributes
  - CMakeLists.txt
  - src/main.c
- Add freertos as a submodule 
  - `git submodule add -b release https://github.com/aws/amazon-freertos.git freertos`
  - `git submodule update --init --recursive`
  - `git add freertos`
  - `git commit -m "Update FreeRTOS to a new release"`
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
```

# Add shared repo with sibling project
TODO