# Quick Start Guide: Setting Up VSCode for Qt App Cross-Compiling

This guide provides step-by-step instructions to configure an environment for cross-compiling Qt applications for Raspberry Pi (RPi) using Visual Studio Code (VSCode). For additional tips and visuals, refer to the companion video tutorial on YouTube:  
[Video Tutorial](https://youtu.be/cfpH3ro9d80)

If you have any problems about cross-compiling Qt, refer to my another video tutorial on YouTube:  
[Video Tutorial](https://youtu.be/cfpH3ro9d80)

## 1. Create a Project Using Qt Creator
It’s strongly recommended to use **Qt Creator 11.0.3**, especially for QML debugging support.  
- Start by creating your Qt project in Qt Creator before transitioning to VSCode.

## 2. Enable X11 Forwarding for VSCode and Deploy SSH Certificate
To enable X11 forwarding and simplify SSH access:  
- For Ubuntu, edit `~/.ssh/config` and add the following at the top:  
  ```
  ForwardX11 yes
  ```
- Use `ssh-copy-id` to deploy your SSH certificate to the Raspberry Pi:  
  ```
  ssh-copy-id <username>@<rpi-hostname>
  ```

## 3. Open the Project in VSCode and Install Extensions
- Open your Qt project folder in VSCode.
- Install the following extensions:  
  - **CMake Tools** (for CMake integration)  
  - **Qt Extension** (for QML syntax highlighting)

## 4. Configure CMake Settings
- In VSCode, go to the **Project Status** section.
- Under **Configure**, click **Select a Kit**.
- Choose your cross-compiler from the list.  
  - If it’s not listed, select **Scan Recursively for Kits** and specify the folder containing your cross-compiler.

## 5. Copy Configuration Files to the `.vscode` Folder
Copy the following files from this repository into your project’s `.vscode` directory:  
- `launch.json`: [Link](https://github.com/MuyePan/pico_rtos_lvgl/blob/main/.vscode/launch.json)  
- `tasks.json`: [Link](https://github.com/MuyePan/pico_rtos_lvgl/blob/main/.vscode/tasks.json)  
- `settings.json`: [Link](https://github.com/MuyePan/pico_rtos_lvgl/blob/main/.vscode/settings.json)

## 6. Modify `CMakeLists.txt`
Add the toolchain settings before the `project()` directive in your `CMakeLists.txt`:  
```
set(CMAKE_TOOLCHAIN_FILE "/home/pmy/CrossCompile/qt6/pi/lib/cmake/Qt6/qt.toolchain.cmake")
```
Adjust the path to match your cross-compiler’s Qt toolchain file location.

## 7. Update `settings.json`
Modify `.vscode/settings.json` with the following configuration, customized for your setup:  
```json
{
    // Binary name of the application
    "APP_NAME": "appHelloVs",
    // Hostname or IP of the Raspberry Pi
    "TARGET_DEVICE": "rpi02pmy.local",
    // Files to copy to the device (space-separated)
    "RSYNC_FILES": "${workspaceFolder}/build/appHelloVs ${workspaceFolder}/Main.qml",
    // Command-line arguments for the application
    "CMD_LINE_ARGUMENTS": "",
    // Target deployment directory on the RPi
    "TARGET_FOLDER": "/usr/local/bin",
    // Path to Qt libraries on the RPi
    "TARGET_QT_LIB_FOLDER": "/usr/local/qt6/lib",
    // GDB debugging port
    "DEBUG_PORT": "12345",
    // Path to the sysroot on your host machine
    "SYS_ROOT": "/home/pmy/CrossCompile/rpi-sysroot"
}
```
Update the values (e.g., paths, hostname, app name) to match your environment.

## 8. Start Coding with AI Assistance
You’re now ready to build, deploy, and debug your Qt application on the Raspberry Pi using VSCode. Leverage AI tools like GitHub Copilot or others for enhanced productivity!

