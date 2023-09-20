# Simulator project for LVGL embedded GUI Library

The [LVGL](https://github.com/lvgl/lvgl) is written mainly for microcontrollers and embedded systems however you can run the library **on your PC** as well without any embedded hardware. The code written on PC can be simply copied when your are using an embedded system.

Using a PC simulator instead of an embedded hardware has several advantages:
* **Costs $0** because you don't have to buy or design PCB
* **Fast** because you don't have to design and manufacture PCB
* **Collaborative** because any number of developers can work in the same environment
* **Developer friendly** because much easier and faster to debug on PC

## Requirements
This project is configured for VSCode and only tested on Linux, although this may work on OSx or WSL. It requires a working version of GCC, GDB and make in your path.

To allow debugging inside VSCode you will also require a GDB [extension](https://marketplace.visualstudio.com/items?itemName=webfreak.debug) or other suitable debugger.

* **SDL** a low level driver library to use graphics, handle mouse, keyboard etc.

## Usage

### Get the PC project

Clone the PC project and the related sub modules:

```
git clone --recursive https://github.com/lvgl/lv_sim_vscode_sdl
```

### Install SDL
You can download SDL from https://www.libsdl.org/

On Linux you can install it via terminal:
```
sudo apt-get update && sudo apt-get install -y build-essential libsdl2-dev
```
On Windows copy "SDL2.dll" to your "Windows\System32" directory and the "ui\simulator\dlls" directory. Copy the SDL2 source code "include" directory to "ui\simulator\inc" name it "SDL2", the final paths look like this:
```
C:\Windows\System32\SDL2.dll
C:\(lv_sim_vscode_sdl source directory)\ui\simulator\dlls\SDL2.dll
C:\(lv_sim_vscode_sdl source directory)\ui\simulator\inc\SDL2\*.h
```

### Build
On Linux use the default make target. Select "g++ build and debug active file" from the VS Code "RUN AND DEBUG" drop down, or via the command line:
```
make
```

On Windows install Cygwin from https://www.cygwin.com. Select the appropriate compiler and debugger during installation (x86_64-w64-mingw32-gcc, gdb). Add the Cygwin binaries directory path ( C:\cygwin64\bin for example ) to the "Path" "System Environment Variable" via Windows Settings. Use the win64 target to build. Select "win64 build and debug active file" from the VS Code "RUN AND DEBUG" drop down, or via the command line:
```
make win64
```

### Setup
To allow custom UI code an `lv_conf.h` file placed at `ui/simulator/inc` will automatically override this projects lv_conf.h file. By default code under `ui` is ignored so you can reuse this repository for multiple projects. You will need to place a call from `main.c` to your UI's entry function.

To build and debug, press F5. You should now have your UI displayed in a new window and can access all the debug features of VSCode through GDB.

To allow temporary modification between simulator and device code, a SIMULATOR=1 define is added globally.
