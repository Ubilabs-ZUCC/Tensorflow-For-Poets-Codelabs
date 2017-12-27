# 2 下载训练集

## 2.1 下载花卉训练集

在开始训练前,您需要一套数据来训练您的模型,我们创建了供大家使用的花卉数据集.你可以通过下面两条命令来下载这些照片.

- 方案一 : 在GitBash中通过命令行下载花卉数据并且解压

```bash
# 请在Terminal 或者 GitBash 下进行操作
$ curl http://download.tensorflow.org/example_images/flower_photos.tgz \
    | tar xz -C tf_files
```

- 方案二 : 解压CodeLabs中的资料,放置在 tf_files/flower_photos 下

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-25/13543654.jpg)

## 2.2 检查训练集是否按照要求放置在制定文件夹下

你需要将相关的数据集放到您的工作目录中,您可以通过使用一下命令确认照片是否已经放到目录中.(请在项目文件夹下打开Gitbash)

```bash
# 请在Terminal 或者 GitBash 下进行操作
$ ls tf_files/flower_photos
# 以下为输出内容
# daisy/ dandelion/ roses/ sunflowers/  tulip/  LICENSE.txt
```

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-25/97915737.jpg)