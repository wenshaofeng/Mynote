#### 8-10  width和min-width的区别和差异性比较
1、正常情况下：
   -  width :给块级元素/行内块 元素设置固定的宽度，或者固定百分比的宽度。

  -  min-width:  当盒子内部元素宽度小于 min-width的值时，盒子宽度为 min-width的值，**当盒子内容宽度大于 min-width的值时，盒子随着内容的增加而被撑大，没有上上限**，但是 盒子宽度的最小值是 设置的 min-width 的值。
![](https://upload-images.jianshu.io/upload_images/9249356-5504a069e9dba9df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


 ###总结：
一般情况下，width设置盒子宽度的固定值。 min-width设置盒子宽度的最小值。

**在父元素设置为flex弹性布局的情况下**：

 >   a、 子元素宽度和小于父元素时，同上，width设置盒子宽度的固定值。 min-width设置盒子宽度的最小值。
>
  >  b、子元素宽度和大于父元素时，width设置的盒子宽度会被压缩，具体宽度计算公式：  
>
   >  子元素 宽度 = （该子元素宽度 / 所有子元素宽度和） * 父元素宽度
>
  >  而此时min-width设置的盒子宽度不会被压缩，盒子的最小宽度为 设置的min-width的值。
--------------------- 
作者：ITzhongzi 
来源：CSDN 
原文：https://blog.csdn.net/ITzhongzi/article/details/80434508 

#### 9-10banner布局
![](https://upload-images.jianshu.io/upload_images/9249356-270d7dfa34ba20f4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
