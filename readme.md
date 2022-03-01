# Kaggle RSNA-MICCAI Brain Tumor Radiogenomic Classification Solution



## 比赛介绍

这是一场kaggle10月份的比赛，RSNA-MICCAI脑肿瘤放射基因组分类，我们被要求通过核磁共振的3D影像，来识别患者脑部肿瘤是否存在MGMT promoter，MGMT promoter是治疗脑肿瘤的一个重要的基因生物标志物。



## 解决方案思路

我们采用了monai库，来导入所有的3d-cnn模型，monai是一个免费的、开源的、基于pytorch的医疗保健图像深度学习框架。

我们从monai中尝试了DenseNet、ResNet、Efficientnet、SEResNet、ViT3D等各个版本型号的CNN并且对本次比赛提供的4类图像类型进行分别训练。最终我们我们挑选出了其中性能较好的模型，分别是（以下格式是“model_type”）：SEresnet101_T1w，ViT3D_T1wCE， efficientnet-b3_T1w， DenseNet121_T1w，SEresnet101_FLAIR2，efficientnet-b3_T2w，resnet50_T1wCE，ViT3D_T1w， SEresnet101_FLAIR。

获得以上模型后，我们直接在inference阶段导入，然后做一个简单的平均即可。



## 比赛trick

1. 本次比赛的一大挑战是数据样本非常少，模型容易过拟合，并且CV（交叉验证）和Public LB的分数都不太稳定，所以我们尝试在所有模型后面，额外加入了一些dropout层。

2. 本次比赛数据量少，所以模型本身的学习依旧困难，预测值往往趋于0.45-0.55之间，所以我们采用了一些极值化的操作，起到了不错的效果。

3. 在数据处理的时候，我们对每个患者的MRI数据，截取了正中间的64个图像，组成64×256×256的3D影像。

   

## 代码、数据集、额外lib
+ 代码

  代码文件为monai_3dcnn.ipynb ，在train和inference阶段都可以用。

+ 数据集
本次比赛没有使用外部数据集，请至kaggle官网下载相关数据。
[RSNA-MICCAI Brain Tumor Radiogenomic Classification | Kaggle](https://www.kaggle.com/c/rsna-miccai-brain-tumor-radiogenomic-classification)

+ 额外lib
请下载百度网盘中的mysitepackages.zip。

