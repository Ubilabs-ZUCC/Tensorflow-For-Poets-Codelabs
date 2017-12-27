# 4 使用再培训模型

在培训模型将会写入一下两个文件

- tf_files/retrained_graph.pb (从网络上下载的模型,以及刚才我们重新训练的花卉层)

- tf_files/retrained_labels.txt (它是一个包含标签的文本文件)

你可以使用我们提供的 label_image.py , 您可以用他来测试你训练好的模型

```bash
# 请在Terminal 或者 GitBash 下进行操作
# graph的参数是模型所在的位置,image的参数是图片所在的位置
$ python -m scripts.label_image \
    --graph=tf_files/retrained_graph.pb  \
    --image=tf_files/flower_photos/daisy/21652746_cc379e0eea_m.jpg
```

你可能会得到如下结果,该结果表示,该图片为雏菊的可能性最高

```bash
# 输出结果
daisy (score = 0.99071)
sunflowers (score = 0.00595)
dandelion (score = 0.00252)
roses (score = 0.00049)
tulips (score = 0.00032)
```

![](http://ox0sjjwt5.bkt.clouddn.com/17-10-25/78200521.jpg)