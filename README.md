# nrf5sdk-createproject
guideline to make new project on NRF5-SDK

## Prerequisite:
### 1.a. Install gnu-mcu-eclipse winddows-build-tools
Download from https://github.com/gnu-mcu-eclipse/windows-build-tools/releases, extract "GNU MCU ECLIPSE" anywhere, remember the path. 
### 1.b.  Add gnu-mcu-eclipse winddows-build-tools to path
Add (your windows-build-tools extraction path)\GNU MCU Eclipse\Build Tools\2.12-20190422-1053\bin to your path environment variable. 
Verify the installation with cmd or powersheell: 
```
make.exe --version 
```
if the installation is OK, will output something like: 
```
GNU Make 4.2.1
Built for x86_64-w64-mingw32
Copyright (C) 1988-2016 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```

### 2. Install GNU Arm Embedded Toolchain
Download from https://github.com/gnu-mcu-eclipse/windows-build-tools/releases, install the toolchain, dont forget to select "add to path" option at the end of the installation. Verify the installation with cmd or powershell: 
 ```
 arm-none-eabi-gcc.exe --version
 ```
 if the installation is OK, will output something like: 
 ```
 arm-none-eabi-gcc.exe (GNU Tools for Arm Embedded Processors 9-2019-q4-major) 9.2.1 20191025 (release) [ARM/arm-9-branch revision 277599]
Copyright (C) 2019 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
 ```
 
 ### 3. Install NRF5-SDK
 Download the zip file from https://www.nordicsemi.com/Software-and-tools/Software/nRF5-SDK/Download#infotabs, extract the SDK anywhere, remember the path. 
 
## How to create a project
1. Copy related from NRF5-sdk example to your workspace
2. Move all content from $(project_dir)/PCA10040/s132/armgcc to $(project_dir)
3. Delete unused .eww file 
4. Make new dir in $(project_dir), name it "src", move main.c to "src" dir
5. Make new dir in $(project_dir), name it "linker", move *_gcc_nrf52.ld to "linker" dir
4. Edit makefile, 
	a. Add these line after OUTPUT_DIRECTORY, overwrite the existing lines
    ```
    	#change according to your NRF5-SDK directory 
	SDK_ROOT := D:/Nordic/nRF5SDK16-0098a08e2
	PROJ_DIR := .
	SDK_CONFIG_DIR := $(PROJ_DIR)/config/
	SDK_CONFIG_FILE := $(PROJ_DIR)/sdk_config.h

	$(OUTPUT_DIRECTORY)/nrf52832_xxaa.out: \
  	  LINKER_SCRIPT  := $(PROJ_DIR)/linker/blinky_gcc_nrf52.ld
	#LINKER_SCRIPT has to be added with white-spaces in the begining, rule of makefile
    ```

	b. edit SRC_FOLDERS, change:
	```
	$(PROJ_DIR)/main.c
	```
		to
	```
	$(PROJ_DIR)/src/main.c
	```
	c. edit INC_FOLDERS, change: 
	```
	../config 
	```
		to
	```
	SDK_CONFIG_DIR
	```
	d. delete this line at bottom of the makefile:
	```
	SDK_CONFIG_FILE := ../config/sdk_config.h
	```


