## VS Code Debugging Configuration for HTML & JavaScript Projects

This repository provides a comprehensive configuration for debugging your HTML & JavaScript projects within VS Code. It leverages the built-in debugging features of VS Code and enhances the debugging experience with the help of a simple HTTP server. 

**Configuration Breakdown:**

### `launch.json`

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch Chrome",
            "request": "launch",
            "type": "chrome",
            "url": "http://localhost:8080",
            "webRoot": "${workspaceFolder}",
            "preLaunchTask": "Run HTTP Server",
            "serverReadyAction": {
                "pattern": "Serving HTTP on.*:(\\d+)",
                "uriFormat": "http://localhost:%s",
                "webRoot": "${workspaceFolder}"
            }
        },
        {
            "type": "msedge",
            "request": "launch",
            "name": "Launch Edge against localhost",
            "url": "http://localhost:8080",
            "webRoot": "${workspaceFolder}",
            "preLaunchTask": "Run HTTP Server",
            "serverReadyAction": {
                "pattern": "Serving HTTP on.*:(\\d+)",
                "uriFormat": "http://localhost:%s",
                "webRoot": "${workspaceFolder}"
            }
        }
    ]
}
```

* **Version:** This file specifies the version of the debugging configuration.
* **Configurations:** This array holds the different debugging configurations for your project.
    * **Launch Chrome:**
        * **Name:** A user-friendly name for the configuration, "Launch Chrome" in this case.
        * **Request:** Specifies the type of debugging action, "launch" in this case, meaning to start a debugging session.
        * **Type:** The debugger type, "chrome" is used for debugging with the Chrome browser.
        * **Url:** The URL to launch the browser with, in this case, it points to "http://localhost:8080".
        * **WebRoot:** The root directory of your project, represented by `${workspaceFolder}` which maps to the current VS Code workspace folder.
        * **PreLaunchTask:**  Specifies that the "Run HTTP Server" task should be executed before launching the browser.
        * **ServerReadyAction:** 
            * **Pattern:** A regular expression used to capture the server's port from the console output of the "Run HTTP Server" task. 
            * **UriFormat:** The format of the URL to launch the browser with, utilizing the captured port number.
            * **WebRoot:**  Specifies the web root directory again.
    * **Launch Edge against localhost:** 
        * This configuration mirrors the "Launch Chrome" configuration, but uses the "msedge" debugger type instead, allowing you to debug your project in Microsoft Edge.

### `tasks.json`

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Run HTTP Server",
            "type": "shell",
            "command": "python -m http.server 8080",
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "problemMatcher": [],
            "isBackground": true
        }
    ]
}
```

* **Version:** This file specifies the version of the tasks configuration.
* **Tasks:** An array of tasks to be executed.
    * **Run HTTP Server:**
        * **Label:** A user-friendly name for the task.
        * **Type:** The type of task, "shell" in this case, indicating a command-line task.
        * **Command:** The command to be executed, "python -m http.server 8080" starts a Python HTTP server on port 8080.
        * **Group:**  
            * **Kind:** Specifies the task's group, "build" in this case, indicating that it is a build-related task.
            * **isDefault:**  Marks this task as the default task in the build group.
        * **ProblemMatcher:** Specifies how to handle errors, "[]" indicates that no specific error handling is required.
        * **isBackground:**  Indicates that the task should run in the background.

### `readme.md` (This file)

This file provides an overview of the configuration files and explains their purpose.

**Getting Started:**

1. **Install VS Code:** Download and install VS Code from [https://code.visualstudio.com/](https://code.visualstudio.com/).
2. **Create a Project Folder:** Create a new folder for your project.
3. **Initialize VS Code:** Open the project folder in VS Code.
4. **Create the Configuration Files:**
    * Create a `.vscode` folder within your project.
    * Create `launch.json` and `tasks.json` files in the `.vscode` folder with the content provided above.
5. **Start Debugging:**
    * Open the Debug view in VS Code (Ctrl+Shift+D).
    * Select the desired debugging configuration from the "Select a Configuration" dropdown menu.
    * Press F5 or click the "Start Debugging" button to start the debugging session.

**Customization:**

* **Port Number:**  You can change the port number used by the HTTP server in `tasks.json`.
* **Debugger:**  You can choose to debug with Chrome, Edge, or another supported browser by modifying the `type` attribute in `launch.json`.
* **Server Command:** You can change the command used to start the HTTP server in `tasks.json`.

**Enjoy debugging your HTML & JavaScript projects efficiently with VS Code!** 
