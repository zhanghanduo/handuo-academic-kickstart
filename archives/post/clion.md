+++
title = "CLion for catkin projects"
date = 2018-05-03T10:07:29+08:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Handuo"]

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["Tips", "Tools", "ROS"]
categories = []

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = "clion1.png"
image_preview = "clion1.png"
caption = ""
preview = true

+++

## Why use CLion?
---
- Better indexing and intelligence hints for C++ than Eclipse and QtCreator-desktop.
- Free for students.
- Also integrate PyCharm already.
- Good Git integration (although I am still used to commandline git).
- I really like the `code inspection clang-tidy` function which makes the code style more modern.

## Initial set-up
---

Highly recommend you to add `source <CATKIN_WORKSPACE_DIR>/devel/setup.bash` to the end of `~/.bashrc` or `~/.zshrc` (Depends you use bash or zsh). So when you type

```bash
echo $ROS_PACKAGE_PATH
```
you can find both `<CATKIN_WORKSPACE_DIR>/src` and `/opt/ros/<ROS_DIST>/share`. So next time you open any terminal, your cmakelist can find the package of `catkin`. 

### Method 1: Launch CLion via terminal

```bash
sh <CLION_INSTALL_DIR>/bin/clion.sh
```
Recommend you to make alias for this command in `~/.bashrc`.

### Method 2: Launch CLion via app icon on sidebar

Just edit `/usr/share/applications/jetbrains-clion.desktop`. If it does not exist, open up Clion and hit `Tools > Create Desktop Entry` first. Here I give an example and if you are using `zsh`, just change `bash` to `zsh`.

```bash
[Desktop Entry]
Version=1.0
Type=Application
Name=CLion
Icon=XXX/clion-2017.2.3/bin/clion.svg
Exec=bash -i -c "XXX/clion-2017.2.3/bin/clion.sh" %f
Comment=The Drive to Develop
Categories=Development;IDE;
Terminal=false
StartupWMClass=jetbrains-clion
```

## Settings

In CLion, you can set the `Toolchain` dialog (including CMake, C++ compiler, gdb) so it can be consistent with your current system-level toolchain.

Also you can set the pass any envrionment variables and parameters to CMake in CLion by using the `CMake` dialog.

<table>
    <tbody>
        <tr>
            <td>
                <img src="https://gitlab.com/handuo/msc_storage/uploads/8dfc0acb4cc40bf7ded20489f98086d2/toolchain.png" alt="tool chain setting" width="100%">
            </td>
            <td>
                <img src="https://gitlab.com/handuo/msc_storage/uploads/c190b9f472836b6993821df80cd27af6/cmake.png" alt="Cmake setting" width="100%">
            </td>
        </tr>
        <tr align="center">
            <td>C++ tool chain settings</td>
            <td>Cmake settings</td>
        </tr>
    </tbody>
</table>

CLion builds your project in `cmake-build-debug` by default. If you want to change that, you could easily set:
```CMake
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "my_dir")
```
Or change the build output directory in the `CMake` dialog as well.

In addition, the `Run/Debug` Configurations dialog in the right up corner allows you to set program execution arguments, working directory, and environment variables.

<table>
    <tbody>
        <tr>
            <td>
                <img src="https://gitlab.com/handuo/msc_storage/uploads/a51009514844b403224fee6e25f056ea/menu_setting.png" alt="open debug & run setting" width="60%">
            </td>
            <td>
                <img src="https://gitlab.com/handuo/msc_storage/uploads/843d191d2e1d8fdef1a15b6aa0b11059/debug_setting.png" alt="modify execution argument" width="100%">
            </td>
        </tr>
        <tr align="center">
            <td>open debug & run setting</td>
            <td>modify execution arguments</td>
        </tr>
    </tbody>
</table>

Now try to build & run your ROS project! I hope this could provide you with better experience on project development.