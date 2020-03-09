# ROS Setting (including some useful shortcuts)

Copy the following into your `~\.bashrc`

    # ROS Setting
    source  /opt/ros/kinetic/setup.bash
    source  ~/catkin_ws/devel/setup.bash

    export  ROS_MASTER_URI=http://localhost:11311
    export  ROS_HOSTNAME=localhost
    export PYTHONPATH=/home/{USER-NAME}/catkin_ws/devel/lib/python2.7/dist-packages:/opt/ros/kinetic/lib/python2.7/dist-packages:
    export DISTRO=kinetic

    # Useful Shortcuts
    alias  eb='nano  ~/.bashrc'
    alias  sb='source  ~/.bashrc'
    alias  cw='cd  ~/catkin_ws'
    alias  cs='cd  ~/catkin_ws/src'
    alias  cm='cd  ~/catkin_ws&&  catkin_make'


Modify `{USER_NAME}` to your user name according to your local computer. 

Here, `cw`,`cs`, etc. are useful shortcuts. 


# Some Useful ROS Commmands

`rosdep check {package_name}`: To check if a certain package was installed

`rosdep install --from-paths src --ignore-src -r -y`: To install any necessary dependancy. If you encounter any catkin_make error, then it is recommended to execute this command. 

# Useful applications

- "VS Code" as a development editor: https://code.visualstudio.com/
    * Using this, you can debug a rospy-based node. How to do this is described below. 
- "Terminator" as a terminal: https://terminator-gtk3.readthedocs.io
    * Particularly, I recommend to modify shortcuts such as "Copy" and "Paste" so that they can be executed without pressing "Shift" as the same in Windows. Otherwise, it may be confusing to use Windows and Ubuntu both. It can be done from "Right Click from any window" -> "Preferences" -> "Keybindings".
- "Double Commander" as a file explorer: https://doublecmd.sourceforge.io/
    * I recommend to link "F4" shortcut to open VS Code. It can be done from "Options" -> "Tools/Editor" -> Modify "Path to program to execute" with `code`. 

# How to debug a ROS node

Using VS Code, you can debug a ROS node based on rospy. 

## Setting

Step 1) Open VS Code, do "File" -> "Open Folder", and choose `src` folder in `catkin_ws`.

Step 2) Do "Debug" -> "Open Configurations", then you will see `launch.json`. 

Step 3) Copy the content of `launch.json` in this repo as additional debug setting. The content looks like

  
    {
      "version": "0.2.0",
      "configurations": [
          {
            "name": "ROS-Python",
            "type": "python",
            "request": "launch",
            "stopOnEntry": true,
            "pythonPath": "/usr/bin/python",
            "program": "${file}",            
            "cwd": "${workspaceRoot}",
            "env": {
                      "PYTHONPATH":"/home/{USER_NAME}/catkin_ws/devel/lib/python2.7/dist-packages:/opt/ros/kinetic/lib/python2.7/dist-packages", 
                   },            
          }      
      ]
    }

 Step 4) Modify `{USER_NAME}` to your user name according to your local computer. 
 
 ## Debugging
 
 Once you finish the setting, you can put breakpoints on any rospy-based ROS node, and you can debug it by pressing "F5" or "Debug" -> "Start Debugging". You should make sure that `roscore` is running before debugging. Also, you should make sure that `ROS-Python` is chosen as a debugging setting in VS Code. Otherwise, by default, the first debug setting would be used. 
  
  
