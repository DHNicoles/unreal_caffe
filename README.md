# Unreal Caffe

[![Travis Build Status](https://travis-ci.org/uglide/RedisDesktopManager.svg?branch=0.9)](https://travis-ci.org/uglide/RedisDesktopManager) 
[![Appveyor Build status](https://ci.appveyor.com/api/projects/status/91mj2ge0lxjf693c/branch/0.9?svg=true)](https://ci.appveyor.com/project/uglide/redisdesktopmanager/branch/0.9)
[![Coverage Status](https://coveralls.io/repos/uglide/RedisDesktopManager/badge.svg?branch=0.9)](https://coveralls.io/r/uglide/RedisDesktopManager?branch=0.9)
[![Coverity Scan Build](https://scan.coverity.com/projects/3548/badge.svg)](https://scan.coverity.com/projects/3548)
[![Documentation Status](https://readthedocs.org/projects/redisdesktopmanager/badge/?version=latest)](http://docs.redisdesktop.com/en/latest/?badge=latest)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/uglide/RedisDesktopManager)





unreal_caffe 是由Unreal Vision维护的一个caffe版本，在使用它完成一些任务的过程中，我们发现很多任务都有重复性，如果每个任务都去编译一个自己的caffe版本非常麻烦，因此我们新建了这么一个自己维护的版本，这里面很多层是官方没有的，至少在未来五年，caffe的一些应用会在这个基础上演化开来，caffe本身只是一个反向传播的计算工具。这里面的附加层才是核心！

这里简单列举一下我们这个版本的一些改变，可以说是非常的前沿了，官方丝毫没有支持。

- cudnn 7 support, add to cudnn7;
- `roi_pooling_layer` needed in Fast-RCNN series task;
- `smooth_l1_loss_ohem_layer` needed in RFCN task;
- `deformalable_conv_layer` which is the most advanced conv (still under test.);




# Contribute

非常欢迎大家来贡献你们的层，基本上能在官方caffe上通过编译的层在unreal_caffe 都没有问题。我们目前还有这些工作没有解决：

-[ ] cmake 安装整合, under testing;


-[ ] PSPNet， ICNet等分割网络层希望得到融合进来;


-[ ] 更多的实例，如RFCN， PSPNet等检测分割模型

如果你希望加入贡献，可以添加微信：`jintianiloveu` ， 一起来 深入做开源的计算机视觉工程，我们还有很多有意思的技术含量的想法期待你的参与！



## 安装

你编译过caffe吗？你觉得蛋疼吗？没有错，是很蛋疼，但是在**unreal_caffe**这个版本里面，你不需要再忍受蛋疼。你只需要克隆，然后make，不用鸡巴的改各种乱七八糟的文件。直接make。当然前提是你得安装一些依赖。不过你不是从一个新的机器来编译，依赖应该都有。

```shell
git clone https://github.com/UnrealVision/unreal_caffe.git
cd unreal_caffe
./generatepb.sh
make -j32
```

你应该可以看到这个:

![](https://i.loli.net/2017/12/28/5a446e4ec8f9a.png)

编译完了之后你应该看到这个:

![](https://i.loli.net/2017/12/28/5a446e8ff3c22.png)

然后编译pycaffe：

```
makepycaffe
```

One last thing:

Add `/path/to/unreal_caffe/python` to your `~/.bashrc` or `~/.zshrc` file. You will using caffe through python. **unreal_caffe default using Python2.7, you can open python3 support but not open them at same time!**



## 视觉任务



后面我们会把一些使用unreal_caffe的目标检测，路面分割等的demo放上来。欢迎大家来贡献feature！



## 在C++项目中使用

由于我们之前安装用的是make，因此直接用CMake来查找caffe是失败的。但是我们可以在cmake中手动去找到它，具体写法也很简单：

```
link_directories("/home/jintian/Documents/unreal_caffe/include/")
include_directories("/home/jintian/Documents/unreal_caffe/include/")
find_library(caffe_LIBRARY
        NAMES  caffe
        HINTS "/home/jintian/Documents/unreal_caffe/build/lib/"
        PATHS "/home/jintian/Documents/unreal_caffe/build/lib/")
```

大家注意，这里其还是得手动把include和lib添加进来，最后一步，在target link的时候link一下库即可：

```
target_link_libraries(rfcn_caffe ${caffe_LIBRARY})
```



# Copyright

caffe来自与BVLC，欢迎大家cite：

```
@article{dai16rfcn,
    Author = {Jifeng Dai, Yi Li, Kaiming He, Jian Sun},
    Title = {{R-FCN}: Object Detection via Region-based Fully Convolutional Networks},
    Journal = {arXiv preprint arXiv:1605.06409},
    Year = {2016}
}
```