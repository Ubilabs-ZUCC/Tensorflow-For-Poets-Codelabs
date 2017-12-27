# 3 (Re)训练神经网络

## 3.1 模型的选择与配置

我们提供了一个训练脚本,用来重新训练Inception V3模型或MobileNet模型.在这个联系中,我们将会使用MobileNet模型.主要区别在于Inception V3模型针对精度做了优化,而MobileNet模型则是更为小巧和高效.

初始版本的V3在ImageNet上的初始精度为78%,但是他的模型有85MB这么大,这笔最大的MobileNet模型还要大,识别精度为70.5%的MobileNet模型仅有19MB大.

选择训练神经网络的配置

- 输入图像的分辨率 : 128 , 160 , 192 or 224px (高分辨率的图像识别需要更多的处理时间,但是准确度会更高,在这里我们推荐使用224px)

- 该模型与MobileNet模型的压缩比 : 1.0 , 0.75 , 0.5 or 0.25 (压缩的越多,识别速度越快,但是越不准确,在这里我们推荐使用0.5作为压缩比例)

Topic1 : 使用推荐配置,通常只需要几分钟来重新训练笔记本电脑,你可以通过shell来设置这些变量

```bash
# 请在Terminal 或者 GitBash 下进行操作
$ IMAGE_SIZE=224
$ ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}"
```

Topic2 : 下图的y轴为**精度**,x轴为所需**计算数**,圆圈的面积为**模型的大小**,园的左下角是128px的图片,右上角是224px

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-20/35059624.jpg)

## 3.2 开启TensorBoard可视化训练平台

在开始训练之前,我们需要先启动TensorBoard(Tensorflow配套的监督和检查工具).您可以用它来监督培训进度.

```bash
# 请在Terminal 或者 GitBash 下进行操作
$ tensorboard --logdir tf_files/training_summaries &
```

输出如下图所示

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-25/76176260.jpg)

并且你可以通过浏览器访问 http://localhost:6006 查看到TensorBoard的页面,在进行training的时候网页会自动显示训练进度

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-25/77143530.jpg)



Topic1 : 如果已经开启了TensorBoard请先关闭其他的TensorBoard或者6006端口的进程

```bash
# Error信息: tensorflow:TensorBoard attempted to bind to port 6006, but it was already in use
$ pkill -f "tensorboard"
```

## 3.3 训练前的额外准备

为什么说是额外的准备呢,这是因为学校网络不好带来的额外步骤.在训练的过程中他会自动搜索下载所需的模型,并进行reTraining.

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-25/63738526.jpg)

这个时候我们需要自行下载训练用的模型,放在/tf_files/models下

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-25/20745447.jpg)

## 3.4 加载处理后的图片数据集(可选)

在进行机器学习前,我们的Python程序会先将我们的图片转换成机器看的数组,这一步大约要话费3~4分钟左右,等不及的同学可以从桌面CodeLabs资料中解压bottlenecks压缩包,讲文件放置在/tf_files/bottlenecks/

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-25/91081799.jpg)

## 3.5 开始训练

如同引言所属,ImageNet模型是具有百万个参数的网络,可以用来区分大量的物品,我们只是训练该神经网络的最后一次,所以训练将会在比较短的时间内结束.

使用一下命令开始训练(注意--summaries_dir选项,该选项是用来将训练进度报告发送到TensorBoard用来显示训练进度的)

如果遇到错误可以查看下文Topic的内容,如果觉得数据加载的过程太慢,可以考虑按4.4可选步骤直接使用处理好的数据

```bash
# 请在Terminal 或者 GitBash 下进行操作
$ python -m scripts.retrain \
  --bottleneck_dir=tf_files/bottlenecks \
  --how_many_training_steps=500 \
  --model_dir=tf_files/models/ \
  --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
  --output_graph=tf_files/retrained_graph.pb \
  --output_labels=tf_files/retrained_labels.txt \
  --architecture="${ARCHITECTURE}" \
  --image_dir=tf_files/flower_photos
```

该脚本将会下载预训练的模型,并在添加一个新的最后一层,训练您下载的花卉照片.

数据处理

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-25/75367974.jpg)

开始训练

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-25/11049357.jpg)

这个时候TensorBoard已经可以看到训练的过程了

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-25/62969073.jpg)

Topic1 : 如果您使用命令后出现下列错误信息,请重新输入IMAGE_SIZE和ARCHITECTURE,在不关闭Gitbash的基础上重新运行

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-25/33071831.jpg)

```bash
# 请在Terminal 或者 GitBash 下进行操作
$ IMAGE_SIZE=224
$ ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}"
```