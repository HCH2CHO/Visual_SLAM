### 熟悉Linux

1. ` sudo apt-get install packagename`

   一般安装在 /usr/local 目录下

2. 环境变量是指操作系统运行环境的一些参数。
   系统环境变量在/etc/profile中定义，通常又会转到/etc/bash.bashrc文件；用户的环境变量在~/.bash_profile中定义，通常又会转到~/.bashrc文件。

3. 根目录为/，下面有/bin，/etc，/home，/lib，/root，/mnt，/opt，/usr等目录

   root为root用户文件夹，home为普通用户文件夹，mnt为挂载文件系统

4. `chmod +x a.sh`

5. `chown xiang:xiang a.sh `

### SLAM 综述文献阅读

1. 自动驾驶的定位避障导航、机器人的定位避障导航、AR

2. 定位与建图是相互关联的，准确的定位需要精确的地图，精确的地图构建又需要准确的位置信息。两者的精度相互关联依赖，所以需要同时定位建图。

3. ①古典年代，引入了SLAM概率论推导方法，包括基于拓展卡尔曼滤波、粒子滤波、最大似然估计

   ②算法分析年代，包括可观测性、收敛性、一致性

   ③鲁棒性时代，更强调算法的鲁棒性、高层次理解力、计算资源、自适应性

4. *FastSLAM: a factored solution to the simultaneous localization*
   *and mapping problem.*

   *ORB-SLAM:ORB-SLAM: a Versatile and Accurate Monocular SLAM System*

   *VINS-Mono: A Robust and Versatile Monocular Visual Inertial State Estimator*

### CMake练习

编写顶层CMakeLists.txt文件如下：

```
project(hello)

add_subdirectory(src)
add_subdirectory(libhello)
set(CMAKE_BUILD_TYPE "Release")
```

src中的CMakeLists.txt文件如下：

```
include_directories(${PROJECT_SOURCE_DIR}/libhello)
set(APP_SRC useHello.cpp)
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
add_executable(sayHello ${APP_SRC})
target_link_libraries(sayHello libhello)
```

libhello中的CMakeLists.txt文件如下：

```
set(LIB_SRC hello.cpp)
add_definitions("-DLIBHELLO_BUILD")
add_library(libhello SHARED ${LIB_SRC})
set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)
set_target_properties(libhello PROPERTIES OUTPUT_NAME "sayHello")
```

### 理解ORB-SLAM2 框架

1.

![image-20200524181746698](C:\Users\HCHO\AppData\Roaming\Typora\typora-user-images\image-20200524181746698.png)



2.(a)将编译出可执行文件和库文件：可执行文件6个和1个库文件

​	(b)include目录下是程序头文件

​		src目录下为源代码

​		Examples目录下有Monocular、Stereo、RGB-D模式的数据文件，及一个ROS节点来读取数据。

​	(c)链接到libDBoW2.so和libg2o.so这两个库

```
${PROJECT_SOURCE_DIR}/Thirdparty/DBoW2/lib/libDBoW2.so
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/lib/libg2o.so
```

