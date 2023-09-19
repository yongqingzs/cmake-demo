## 关于makefile的说明
1. 在msys2中安装make: pacman -S make，安装cmake: pacman -S cmake
- 注意：这些均会安装在msys64/usr/bin下，而不是msys64/mingw64/bin下
2. 关于makefile中Tab键的错误:
- 在设置中Editor:Detect Indentation和Editor:Insert Spaces取消打勾
- 如果重新打勾，Detect Indentation的功能将恢复正常
3. 在make_template_linux中，提供了一个简单并通用的makefile模板(基于Ubuntu)