# **Hikari-Linux-Builds**
Having problems with hikari not compiling or Linux? Don’t want to waste your time pouring in hours for defeat? Hikari too outdated? Don’t worry, for an idiot (me) has gone through that just to make it public for you!

# **What the fuck is Hikari?**
-> Hikari from [Zangh](https://github.com/HikariObfuscator) is an old toy llvm based obfuscator.

-> This works cross-platform, but targets mainly ios and macOS.

-> You can uss this for linux and windows too!

-> It's a pain to set up though, which is why alot of people get deterred.

-> it took me 11 hours for a single build even with past experience. I bet it takes less than half an hour on a mac, but.... *linux supremacy*

-> It's a pain to get ios/macos stuff to get working on linux, but people manage i guess if you're determined enough.

# **Where do I get them?**
-> Above (github)

-> Google drive (releases)

(They might be compressed over and over, so it'll take a while to deflate. mine is over a giga-byte...)

# **Which toolchains are compiled?**
-> LLVM18.1+

-> More coming soon

# **How Do I use them?**
-> You can use them with [theos](https://theos.dev/docs)

-> on your host machine too! just set ‘‘ld‘‘ to your linux's linker (you get this by running:)
‘‘‘
which ld
‘‘‘

# **How to set it up with theos?**
 **You're going to have to follow each of these steps. It's not hard to do it properly if you listen.**
 1. Download it and unzip it, until you reach a ‘‘my-toolchain‘‘ named folder or similar.
 3. Download an old IOS sdk (example 13.7) from [theos/sdks](https://github.com/theos/sdks/releases)
 4. Move/Copy this toolchain to your $THEOS/toolchain path. There will be a ‘‘linux‘‘ folder here by default (should be, atleast...)
 5. Move/Copy this sdk folder after un-compressing it to $THEOS/sdks
 6. Now open any theos project you have. By default there is a Makefile.
 7. you will set the following variables:
‘‘‘
TARGET := iphone:clang:13.7 # depends on which old sdk you used
ARCHS = arm64 # only system level apps/binaries use arm64e. but linux doesn't support it so we will set it explicitly to arm64
BASE_HIKARI_PATH = $THEOS/toolchain/<name-of-toolchain-folder>/bin
TARGET_CC = $(BASE_HIKARI_PATH)/clang
TARGET_CXX = $(BASE_HIKARI_PATH)/clang++
TARGET_LD =  $(BASE_HIKARI_PATH)/ld
SYSROOT = $THEOS/sdks/<iphonesdkfolder>.sdk
‘‘‘
8. Now, do a quick compile test and see if all goes well. you may get errors regarding a 'module map' deprecation, so just listen to the error and rename that file from .map to .modulemap.
9. Now compile again and this time it should suceed.
10. Now, you can add flags for Obfuscation.

‘‘‘
OBFUSCATED_Flags = -mllvm -enable-cffobf -mllvm -enable-strcry -mllvm -enable-subobf -mllvm -enable-fco -mllvm -ah_objcruntime -mllvm -enable-antihook -mllvm -ah_inline -mllvm -enable-indibran -mllvm -indibran-enc-jump-target -mllvm -ah_antirebind -enable-constenc -mllvm -constenc_times=1 -mllvm -constenc_togv=1 -mllvm -constenc_togv_prob=50 -mllvm -constenc_subxor=1 -mllvm -constenc_subxor_prob=40
‘‘‘

10. **BE CAREFUL THIS CAN STRAIN AND CRASH EVEN FUCKING NASA COMPUTERS!**
11. experiment around with the flags, find fhe one that is just right.
12. Pro tip: constenc ususally hogs resources and is the main crash causing culprit.
13. You can add these flags in ‘‘CFFlags‘‘ and ‘‘CCFlags‘‘ and compile.

# **Compile info?**
-> Proudly compiled on manjaro linux (i use arch, btw)

-> llvm18+

-> compiled with system llvm, do not use gcc or g++ on linux to compile this.

# ** OPEN FOR BUG REPORTS!!! **
-> Disclaimer: This will have to do with runtime issues, not llvm or clang bugs. you report that to @llvm in llvm-project, not here

# **License**
none really. just dont't do stupid stuff i guess. im not responsible blah blah blah blah i went fucking insane it took me 9 hours for one build and 2 extra hours for after build bug bullshit and don't want someone else to go through it.
