## 关于VSCode中c开发环境的说明
1. 关于编译器
- VSCode官方: pacman -S --needed base-devel mingw-w64-x86_64-toolchain
- tan: pacman -S mingw-w64-ucrt-x86_64-toolchain
- 当前采用VSCode官方的编译器环境
- 当期添加环境变量: I:\msys64\mingw64\bin
2. 生成json文件
- 需要手动生成launch.json、tasks.json(通过运行旁边的小齿轮)
- 生成c_cpp_properties.json(ctrl + shift + p -> C/C++:Edit Configurations(UI))
3. 改变.exe生成路径
- 为了改变.exe生成路径，tasks.json-args修改如下
```json
"${fileDirname}\\..\\bin\\${fileBasenameNoExtension}.exe" 
```
- 为了改变.exe运行路径，将launch.json-program修改如下
```json
"${fileDirname}\\..\\bin\\${fileBasenameNoExtension}.exe"
```
4. 为了识别 /include 头文件:
- 在c_cpp_properties.json中的includePath添加
```json
"${workspaceFolder}/include"
```
- 在tasks.json中的args添加
```json
"-I", 
"${workspaceFolder}\\include"
```
5. 为了多文件运行:
- 在tasks.json中修改args
```json
// "${file}"  // 单文件运行，方便调试
"${fileDirname}\\*.c"  // 修改之后该文件夹只能存在一个main()函数
```

## 关于Ubuntu-VSCode的c开发环境的说明
1. 关于编译器(通过apt命令安装)
- gcc
- gcc 11(gcc 11使用的c标准和gcc并不相同，由于合并的要求，以gcc 11作为默认编译器，以下设置均针对gcc 11)
2. 生成json文件
- 需要手动生成launch.json、tasks.json(通过运行旁边的小齿轮)
- 生成c_cpp_properties.json(ctrl + shift + p -> C/C++:Edit Configurations(UI))
3. 改变.exe生成路径
- 为了改变.exe生成路径，tasks.json-args修改如下
(注意在windows-dos下，路径分隔符为\\，而在linux下，路径分隔符为/)
```json
"-o",
"${fileDirname}/../bin/${fileBasenameNoExtension}" 
```
- 为了改变.exe运行路径，将launch.json-program修改如下
```json
"${fileDirname}/../bin/${fileBasenameNoExtension}"
```
4. 为了识别 /include 头文件:
- 在c_cpp_properties.json中的includePath添加
（因为在后面的开发中，将include和scr下建立新的子文件夹，所以设置做了调整）
```json
"${workspaceFolder}/include"
```
- 在tasks.json中的args添加
```json
"-I", 
"${workspaceFolder}/include",
"${workspaceFolder}/include/子文件夹",
```
5. 为了多文件运行:
- 在tasks.json中修改args
```json
"-g",
// "${file}"  // 单文件运行，方便调试
"${fileDirname}/*.c",  // 修改之后该文件夹只能存在一个main()函数
"${fileDirname}/子文件夹/*.c",
```
6. 在linux下，不会自动链接动态库，需要手动链接动态库
```json
"-lm",
```



## 关于makefile的说明
1. 在msys2中安装make: pacman -S make，安装cmake: pacman -S cmake
- 注意：这些均会安装在msys64/usr/bin下，而不是msys64/mingw64/bin下
2. 关于makefile中Tab键的错误:
- 在设置中Editor:Detect Indentation和Editor:Insert Spaces取消打勾
- 如果重新打勾，Detect Indentation的功能将恢复正常

## 关于cmake的说明
1. 使用make clean会清除生成的.exe和库文件
2. 生成的动态库必须和.exe位于同一文件夹下，.exe才能正常运行
- 因为.exe运行会调用动态库，而只有在同一文件夹下.exe才能识别到动态库
3. 生成的静态库可以删除，并不影响.exe的运行
- 因为.exe在编译过程中调用了静态库，所以即使删除生成的静态库，.exe也能正常运行
