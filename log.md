## 关于VSCode中c开发环境的说明
1. 关于编译器
- VSCode官方: pacman -S --needed base-devel mingw-w64-x86_64-toolchain
- tan: pacman -S mingw-w64-ucrt-x86_64-toolchain
- 当前采用VSCode官方的编译器环境
- 当期添加环境变量: I:\msys64\mingw64\bin
2. 预设置(for vscode)
- 需要手动生成launch.json
- 为了改变.exe生成路径，tasks.json-args修改如下
```json
"${fileDirname}\\..\\bin\\${fileBasenameNoExtension}.exe" 
```
- 为了改变.exe运行路径，将launch.json-program修改如下
```json
"${fileDirname}\\..\\bin\\${fileBasenameNoExtension}.exe"
```
3. 为了识别 /include 头文件:
- 在c_cpp_properties.json中的includePath添加
```json
"${workspaceFolder}/include"
```
- 在tasks.json中的args添加
```json
"-I", 
"${workspaceFolder}\\include"
```
4. 为了多文件运行:
- 在tasks.json中修改args
```json
// "${file}"  // 单文件运行，方便调试
"${fileDirname}\\*.c"  // 修改之后该文件夹只能存在一个main()函数
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

