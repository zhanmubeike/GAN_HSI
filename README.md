# GAN_HSI
环境
#=======================================
python 版本为 2.7
tensorflow 版本为 1.8.0
keras 版本为 2.2.4
opencv 版本为 3.4.1
#=======================================

程序说明

1.半监督GAN_v1
#=============================================================================
其中GAN_train.py和GAN_test.py是两个主要程序，第一个用来训练模型，第二个用来调用训练好的模型进行测试和输出结果

vlib里包含三个文件分别为get_inputs.py， layers.py， plot.py
get_inputs.py
用于对数据库读入和预处理，包括归一化，和标签one_hot化等操作
layers.py
在tensorflow自带函数库的基础上，对卷积函数，反卷积函数，激活函数，batch_norm，池化等等进行了重写
plot.py
用于连续绘制loss曲线和acc曲线

只要安装好对应环境，只需要修改get_inputs.py里的数据集路径，代码都可以跑通，
执行时只需要先运行GAN_train.py得到模型，再运行GAN_test.py进行测试
#=============================================================================

2.半监督GAN_v2
#=============================================================================
全部文件一共有四个
get_unsupervisied_inputs.py以及GAN_train_2d+unsupervisied.py是一套，对应迁移学习方法
get_wellDistribute_inputs.py以及GAN_train_wellDistribute.py是一套，对应数据均匀分布时的方法

get_unsupervisied_inputs.py现在返回六组数据，除了原始的X_train, X_test, Y_train, Y_test
之外，新加入了无监督数据unsupervisied_X, unsupervisied_Y可以修改如下：
unsupervisied_data, _testx, unsupervisied_label, _testy = train_test_split(X_train,Y_train, test_size=0.5, random_state=0)

GAN_train_wellDistribute.py现在将训练数据和测试数据都处理成均匀分布，目前初始化为每类350个
后续改动见代码内注释;
改动仅限于训练代码和数据处理，GAN_test不做处理，用半监督GAN_v1的就可以

GAN_train_2d+unsupervisied.py在train函数里增加了无监督训练那的迭代步骤，此外需要多设置一个
无监督训练迭代步骤的参数self.unsupervised_epoch，其他部分和半监督GAN_v1相同

#=============================================================================

3.孪生稠密网络
#=============================================================================
软件包内共有五个主要py文件

conv_signal_train.py
这个py文件实现了孪生网络的训练，其中包含两种卷积神经网络结构
1dconv架构和2dconv架构，

densenet_signal_train.py
densenet.py
这两个py文件共同构成了基于稠密孪生网络的架构
densenet.py用于构建稠密网路，densenet_signal_train.py则构建
孪生网络架构并进行训练

signal_test.py
这是一个通用的“聚类”测试文件，以上三种架构一维卷
积网络孪生网络，二维卷积孪生网络和稠密孪生网络训练好模型之后都
可以用这个文件进行分类测试

get_inputs
是一个信号数据预处理文件，在弱监督模型中同样进行了使用
#=============================================================================
