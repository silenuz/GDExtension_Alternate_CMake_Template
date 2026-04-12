Note the content of this repository is basically the same as the [official template](https://github.com/godotengine/godot-cpp-template) .

Even most of this readme is their hard work, and credit for this template belongs to the maintainers of that repository, as I have only made small changes.

# godot-cpp template
This repository serves as a quickstart template for GDExtension development with Godot 4.0+.

## Contents
* Preconfigured source files for C++ development of the GDExtension ([src/](./src/))
* An empty Godot project in [project/](./project), to test the GDExtension
* godot-cpp as CMake fetched content placed in build folder /_deps


## Usage - Template

To use this template, log in to GitHub and click the green "Use this template" button at the top of the repository page. This will let you create a copy of this repository with a clean git history.

To get started with your new GDExtension, do the following:

* clone your repository to your local computer
* change the name of the compiled library file inside the [CmakeLists.txt](./CMakeLists.txt) file by modifying the `libname` string.
  * change the paths of the to be loaded library name inside the [project/bin/example.gdextension](./project/bin/example.gdextension) file, by replacing `EXTENSION-NAME` with the name you chose for `libname`.
* change the `entry_symbol` string inside [project/bin/example.gdextension](./project/bin/example.gdextension) file.
  * rename the `example_library_init` function in [src/register_types.cpp](./src/register_types.cpp) to the same name you chose for `entry_symbol`.


Now, you can configure the project which will download the godot-cpp bindings:

```shell
cmake -G Ninja -S . -B cmake-build-debug
```
Once it is configured you can build it by specifying the target as the cmake-build-debug folder:

```shell
cmake --build cmake-build-debug
```

If the build command worked, you should have a new library file for the target system in project [bin](./project/bin).
You can test it with the [project](./project) project. Import it into Godot, open it, and launch the main scene. You should see it print the following line in the console:

```
Type: 24
```

### Configuring an IDE

Comming Soon....

