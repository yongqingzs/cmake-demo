## 关于cmake的说明
1. 使用make clean会清除生成的.exe和库文件
2. 生成的动态库必须和.exe位于同一文件夹下，.exe才能正常运行
- 因为.exe运行会调用动态库，而只有在同一文件夹下.exe才能识别到动态库
3. 生成的静态库可以删除，并不影响.exe的运行
- 因为.exe在编译过程中调用了静态库，所以即使删除生成的静态库，.exe也能正常运行

## 关于cmake中运行逻辑的说明
1. 对于.c文件，源文件名本身(可以以变量形式存在)必须传递给add_executable函数
2. 对于.h文件，只要将.h文件所在的目录传递给include_directories函数即可
3. 对于生成的bin文件，需要设置内置变量: 
set (EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
- EXECUTABLE_OUTPUT_PATH：目标二进制可执行文件的存放位置
- PROJECT_SOURCE_DIR：工程的根目录
4. TODO: 子目录CMakeLists.txt运行逻辑的说明
5. TODO: 关于动态库和静态库的编译控制
6. 链接动态库
- 尤其对于linux系统，libm.so需要手动链接(数学库相关)
- target_link_libraries(bin lib)

## 关于cmake中重要函数的说明
1. add_executable(bin source)：生成可执行文件bin
- bin是可执行文件的名字，source是源文件名（可以以变量名替代）
2. aux_source_directory(dir var): 将指定目录dir下的源文件名存入变量名var中
- dir是指定目录，var是变量名
- NOTE: 必须每个目录分别添加
3. set(var source): 将指定源文件名存入变量名var中
- var是变量名，source是源文件名
4. add_subdirectory: 用于向当前项目中添加一个子目录，并在该子目录中执行另一个CMakeLists.txt文件
5. include_directories(dir): 将指定目录dir下的头文件添加到搜索路径中
- NOTE: 无需每个目录分别添加，可一起添加

