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

source ~/.zsh_profile

3) Download the WebRTC source

Back in your working directory, in the next few commands to download the massive source repository:

gclient config http://webrtc.googlecode.com/svn/trunk

 
.gclient file should contain a line like:
target_os = ['ios', 'mac']

gclient sync --force
 
cd /path/to/webrtc/trunk

export GYP_DEFINES="build_with_libjingle=1 build_with_chromium=0 libjingle_objc=1"
export GYP_GENERATORS="xcode"
gclient runhooks
