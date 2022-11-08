# ResNet_Challenge

## Dataset(CIFAR10)

a relatively small dataset. 50000 images, 10 labels

CIFAR: 32 x 32

Imagenet: 300 x 300 at least

## ResNet Intro

![image-20221105002015179](C:\Users\92333\AppData\Roaming\Typora\typora-user-images\image-20221105002015179.png)

基本架构，如果模型深度变高，所对应处理的图片大小也会较大，为了降低运算量，会对图片先进性降维的操作，做完卷积后，在进行升维

![image-20221104233724484](C:\Users\92333\AppData\Roaming\Typora\typora-user-images\image-20221104233724484.png)

There is overfitting when the depth reaches 1202.（所以为什么transformer一千亿的参数能保持不过拟合呢=3=）

![image-20221104234155586](C:\Users\92333\AppData\Roaming\Typora\typora-user-images\image-20221104234155586.png)

在residul connection中，如果新加的层不能让你的模型变好，那训练出来的下一个结果$H(x) = F(x) - x$应该等于0，所以1000层的网络可能只有前几百层有用，后面的网络基本上没有什么东西可以学的



plain network求梯度:

$\frac{\part{f(g(x))}}{\part{x}} = \frac{\part{f(g(x))}}{\part{g(x)}}.\frac{\part g(x)}{\part x}$

Resnet求梯度：

$\frac{\part{f(g(x))}}{\part{x}} = \frac{\part{f(g(x)}}{\part{g(x)}}.\frac{\part g(x)}{\part x} + \frac{\part g(x)}{x}$

浅层网络梯度相对来说会比深层的大，$g(x)$层所队对应的梯度都是不会太小，从误差反传的角度来看训练比较快，训练的动。

反过来看文章开头部分，为什么网络深度增加，SGD收敛，但是模型效果不好的原因也显而易见了，因为梯度太小，训练不动。如蓝线（不加residual block）

![image-20221105001020322](D:\NYU\NYU\classes\22fall\dsp lab\week9\image-20221105001020322.png)

## Data Augmentation Policy
We apply random data augmentation techniques to train data only. 
### 1. Random Cropping
Use `transforms.RandomCrop()` from PyTorch to cut random image patches from the original image. Patch size (24\*24) out of (32\*32) with a padding of 4.\n
![image-1](https://pytorch.org/vision/stable/_images/sphx_glr_plot_transforms_012.png)

### 2. Random Rotation
Use `transforms.RandomRotation()` from PyTorch to rotate images by a random degree. Degrees ranges from 0 to 180.\n
![image-2](https://pytorch.org/vision/stable/_images/sphx_glr_plot_transforms_009.png)

### 3. Random Horizontal flipping
Use `transforms.RandomHorizontalFlip()` from PyTorch to randomly flip images.\n
![image-3](https://pytorch.org/vision/stable/_images/sphx_glr_plot_transforms_024.png)
