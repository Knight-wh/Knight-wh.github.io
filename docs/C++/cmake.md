# Cmake操作

## command line

```cmd
mkdir build
cd build
cmake .. //windows下默认是MSVC，可使用-G指定编译器cmake -G"MinGW Makefiles" ..
cmake --build . //--build用来指定编译生成文件的目录，可使用mingw32-make
```

## Cmake-gui

使用界面进行配置和生成，然后在编译目录里，调用编译器来实际编译和链接项目
```
cmake --build .
```

## Tips

首先要通过cmake进行配置和生成，在不改变`CMakeLists.txt`的情况下，修改源码后，可以直接进行编译，不用再重复`cmake ..`

cmake编译的项目，cpp文件中打开的文件设置绝对路径（还没找到相对路径的方法）