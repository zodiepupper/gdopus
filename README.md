# gdopus

TLDR: run this to download and build the whole thing in one go:
`git clone https://github.com/zodiepupper/gdopus --recurse-submodules && cd gdopus/src/opus/ && mkdir build && cd build && cmake -DCMAKE_POSITION_INDEPENDENT_CODE=ON .. && cmake --build . && cd ../../../ && scons`


To build, please follow the following instructions:
- `cd src/opus/` to get into the opus directory
- look at the README to find what dependencies you need to install
- `mkdir build` to create the build folder in `src/opus/`
- run `cmake -DCMAKE_POSITION_INDEPENDENT_CODE=ON ..` to setup the cmake build files to build the static library
  - the flag `-DCMAKE_POSITION_INDEPENDENT_CODE=ON` tells the opus static library to compile in a way that is usable when being embedded in a shared library like a gdextension. this is the cmake equivalent to -fPIC
- run `cmake --build .` to actually build the library file
- once you've built opus, you should have a libopus file in `src/opus/build/`, if that's true then good job!
- now you'll want to go to the project root and simply run `scons` (obviously you can also run scons with arguments, ex: apple silicon macs need to run it like this: `scons platform=macos arch=arm64`)
- that should be it. it will build the gdextension and place the resulting lib in the test project's bin directory
  - you should be able to find the resulting gdextension in `gdextensiontest/bin/` and it should start with `libgdopusencoder`

## ANDROID
- install android commandline tools for your platform using sdkmanager to get the latest version
- `cd src/opus; mkdir build-android; cd build-android`
- `cmake .. -DCMAKE_TOOLCHAIN_FILE={$ANDROID_HOME}/ndk/23.2.858313/build/cmake/android.toolchain.camke -DANDROID_ABI=arm64-v8a`
  - you can replace 23.2.8568313 with whatever version of the ndk got downloaded with the commandline tools thing
- `cmake --build . --config Release`
- cd to the root of the project (gdopus/)
- `scons platform=android`

please keep in mind this is still in early development and will change in the future.
right now this repo simply contains the most basic implementation of the opus library so I could use it for learning purposes and for a quick voip utility.
future updates will flesh out the features, stay tuned.

If you're interested in supporting development consider submitting a PR or financailly supporting the [barkvr](https://github.com/zodywoolsey/barkvr) project which this tool is being developed for: 
