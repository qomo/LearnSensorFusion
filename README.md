# LearnSensorFusion
 > 9轴传感器学习的阶段性总结  

 关于9轴传感器的融合，以及基于这些传感器的惯性导肮的原理。都来自于一门叫捷联惯性导航的学科，具体可以参考引用【1】【2】。

## Android中的9轴与姿态传感器【3】  
### 物理传感器  
- 加速度传感器（未校准）
- 陀螺仪（未校准）
- 磁力计（未校准）

### 虚拟传感器  
- 加速度传感器（校准）
- 陀螺仪（校准）
- 磁力计（校准）
- 重力传感器
- 线性加速度传感器
- 方位传感器（orientation）
- 旋转矢量（rotation vector）
- 游戏旋转矢量（game rotation vector）
- 地磁旋转矢量（geomagnetic rotation vector）

## 物理传感器与虚拟传感器的关系  
- 加速度传感器（校准）
> 六面校准  

- 陀螺仪（校准）  
> 静态自校准零偏  

- 磁力计（校准）
> 软磁：拟合椭球参数  
> 硬磁：陀螺仪辅助融合

- 重力传感器  
> 平滑滤波+陀螺仪辅助融合  

- 线性加速度传感器  
> 加速度传感器（校准） - 重力传感器

- 方位传感器（orientation）、旋转矢量
> 加速度+陀螺仪+磁力计 kalman滤波

- 游戏旋转矢量
> 加速度+陀螺仪 kalman滤波

- 地磁旋转矢量
> 磁力计+陀螺仪 kalman滤波

## 传感器融合的基础知识  
### 数学基础：旋转变换、欧拉变换  
涉及两个主要的坐标系：1）导航坐标系，即与地面关联的X-东、Y-北、Z-天坐标系；2）手机固连坐标系【4】  
【1】【2】书中有这些坐标系的详细定义。  

根据选择的坐标系的不同，同一个矢量有不同的数值表示。不同坐标系中相同矢量的表示能够通过坐标变换来转换。  
导航坐标系与手机固连坐标系间的旋转变换，实际上就是手机的姿态，即方位传感器（欧拉角）和旋转矢量（四元数）实际上就是这个旋转变换的其中两种表示形式。  
高翔博士写的《视觉SLAM十四讲》中的第三讲中有坐标变换的通俗讲解【5】  
旋转变换一般有几种表示形式：1）旋转矩阵；2）轴角；3）四元数；4）欧拉角。  
在Sensor Fusion算法中，常用旋转矩阵和四元数两种旋转变换，欧拉角通常用给人呈现旋转的图像。  

### 算法基础：卡曼滤波  
卡曼滤波是传感器融合的最主要算法，【6】【7】是我看到的这个算法比较清晰的诠释。  
如果你执着与算法的细节，【8】这本书也是不错的参考材料。  

### 物理基础：三维空间的刚体运动  

## 具体案例  
略

## 引用  
[【1】Savage, Paul G. "Strapdown analytics." (2000): 15-1.](./books/savagesins.pdf)  
[【2】Titterton, David, John L. Weston, and John Weston. Strapdown inertial navigation technology. Vol. 17. IET, 2004.](./books/StrapdownInertial_2ED.pdf)  
[【3】Android Motion Sensor](https://developer.android.com/guide/topics/sensors/sensors_motion)  
[【4】Sensor Coordinate System](https://developer.android.com/guide/topics/sensors/sensors_overview#sensors-coords)  
[【5】视觉SLAM十四讲](./books/视觉slam十四讲.pdf)  
[【6】Faragher, Ramsey. "Understanding the basis of the Kalman filter via a simple and intuitive derivation." IEEE Signal processing magazine 29.5 (2012): 128-132.](./papers/Understanding_the_Basis_of_the_Kalman_Filter_Via_a_Simple_and_Intuitive_Derivation.pdf)  
[【7】How a Kalman filter works, in pictures](https://www.bzarg.com/p/how-a-kalman-filter-works-in-pictures/)  
[【8】卡尔曼滤波理论与实践（MATLAB版）（第四版）](https://book.douban.com/subject/30425276/)