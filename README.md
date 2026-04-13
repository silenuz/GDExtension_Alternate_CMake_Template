Note the content of this repository is basically the same as the [official template](https://github.com/godotengine/godot-cpp-template) .

Even most of this readme is their hard work, and credit for this template belongs to the maintainers of that repository, as I have only made small changes, mainly
omiting the godot-cpp bindings as a git submodule, due to the fact that a submodule points to a specific branch/tag/commit in the repository.

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

The default branch of the godot-cpp bindings that is downloaded by cmake is the current master branch. 
It is likely that you will wish to change this to target a specific stable version of the GDExtension api.
To do so, change the tag property of the godot-cpp fetch configuration in [CMakeLists.txt](./CMakeLists.txt)
to the git tag of the version of the  [godot-cpp](https://github.com/godotengine/godot-cpp) bindings you wish to target.

For example if you wish to specifically target 4.5, you would change it from this:
```cmake
FetchContent_Declare(
        godot-cpp
        GIT_REPOSITORY https://github.com/godotengine/godot-cpp.git
        GIT_TAG master
        SYSTEM
)
```
To This:

```cmake
FetchContent_Declare(
        godot-cpp
        GIT_REPOSITORY https://github.com/godotengine/godot-cpp.git
        GIT_TAG godot-4.5-stable
        SYSTEM
)
```
By default, Cmake will place the fetched content in the 

```cmake
"${CMAKE_BINARY_DIR}/_deps"
```
which in this case is the [cmake-build-debug](./cmake-build-debug) folder.

If you wish to change the folder where external source code will be stored and built, you can set the
`FETCHCONTENT_BASE_DIR` variable in the [CMakeLists.txt](./CMakeLists.txt) to change the download/build folder.

For example if you wish to have your external source downloaded and built in a folder called `_external_bin`, you would add the following line near the top of the [CMakeLists.txt](./CMakeLists.txt) file like so:

```cmake
set (FETCHCONTENT_BASE_DIR "${CMAKE_SOURCE_DIR}/_external_bin" CACHE PATH "Custom fetch content root")
```

Note this will create three folders in the base directory for each external source, the source code itself, a sub build folder, and a build folder.  

In most cases it might be desirable to have the source code separate from its build folders, or perhaps you want your project to have the godot-cpp source code in the main project folder like the default template.

To change the folder where the source code for the godot-cpp bindings is placed, add a `SOURCE_DIR` to the fetch content declaration like so:
```cmake

FetchContent_Declare(
        godot-cpp
        GIT_REPOSITORY https://github.com/godotengine/godot-cpp.git
        GIT_TAG godot-4.5-stable
        SOURCE_DIR "${CMAKE_SOURCE_DIR}/godot-cpp"
        SYSTEM
)
```

This will result in the source code being placed in the project's top level, in a folder called godot-cpp. 

If you changed the base directory for fetching content, then that directory will contain the `godot-cpp-build` and `godot-cpp-subbuild` folders, otherwise they will be found in default `_deps` folder.

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

