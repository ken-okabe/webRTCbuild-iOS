webRTCbuild-iOS
===============
1) Create a working directory

Make a new directory somewhere,  and get ready because you’re going to need in the ballpark of 1.7 GB of free space
2) Download the Chromium depot tools

Switch into your working directory and grab the Chromium depot_tools repository with git:

git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git

These are a bunch of tools used during the build process, and they will need to be in your path so you will need to modify your .bash_profile (or other shell file) and modify the PATH line like so:

export PATH=/a_bunch_of_stuff:/working_directory/depot_tools:$PATH

Next you will need to restart your terminal or re-run your bash profile so that the changes take effect:

 ~/.zshrc

3) Download the WebRTC source
 
gclient config http://webrtc.googlecode.com/svn/trunk

(edit generated .gclient)  
target_os = ['ios', 'mac']

gclient sync --force
 
4) set up projects 
cd trunk

export GYP_DEFINES="build_with_libjingle=1 build_with_chromium=0 libjingle_objc=1"

export GYP_GENERATORS="ninja"
export GYP_GENERATORS="xcode"

export GYP_DEFINES="$GYP_DEFINES OS=ios target_arch=ia32"
 
export GYP_GENERATOR_FLAGS="$GYP_GENERATOR_FLAGS output_dir=out_sim"

export GYP_CROSSCOMPILE=1

gclient runhooks






create a Xcode project from scratch that works with WebRTC libraries.

1. Build WebRTC libraries following the steps from talk/app/webrtc/objc/README
2. Add the webrtc source directory into header search path in [build settings]->[search paths]
3. Choose libstdc++ for C++ standard library under [build settings] -> [Apple LLVM compiler language]
4. In [build phases]->[link binary with libraries], add AudioToolbox.framework, CodeMedia.framework, CoreVideo.framework, AVFoundation.framework, libsqlites3.dylib, UIKit.framework, Foundation.framework, CoreGraphics.framework, OpenGLES.framework, and QuartzCore.framework
5. Drag the WebRTC static libraries built by ninja (libxxxx.a) into the project as references (no need to copy them, so that when the libraries are updated, your project can link against the newest ones)
6. Select all of the WebRTC libraries, in file inspector change their file type to Mach-O Object Code
7. 
(scott)
