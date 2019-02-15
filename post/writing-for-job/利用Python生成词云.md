## 用到的模块
- matplotlib  用来画图
- wordcloud  生成词云
- jieba  中文分词
- numpy  图像矩阵处理
- PIL  图像读取

推荐使用jupyter-notebook玩耍

## 简单的词云
使用默认参数

```  Python

from wordcloud import WordCloud
import jieba
import matplotlib.pyplot as plt

# 设置工作目录
RUN_PATH = "./word_cloud/" 
# 设置字体
FONT = "_fonts/simhei.ttf"
# 设置文档
FILE_SOURCE = "_source/平凡的世界.txt"

# 文档读取
text_raw = open(RUN_PATH + FILE_SOURCE,'r',encoding = 'UTF-8').read()
# 分词处理
text_jieba = jieba.cut(text_raw,cut_all = True)
text_jieba_space = " ".join(text_jieba)

# 词云生成
wd_gen = WordCloud(font_path = RUN_PATH + FONT, # 字体
                   width = 800,
                   height = 600,
                   background_color = 'black').generate(text_jieba_space)
# 保存图片
plt.imsave(RUN_PATH + FILE_SOURCE[8:].replace('.txt','.png'),wd_gen)
# 图片显示
plt.imshow(wd_gen)
plt.axis("off")
plt.show()

```
效果(《平凡的世界》)
![平凡的世界.png](https://upload-images.jianshu.io/upload_images/1711028-a3502af1f4dcf9bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 带蒙版的词云

```
from wordcloud import WordCloud
import jieba
import matplotlib.pyplot as plt
import numpy as np
from PIL import Image

RUN_PATH = "./word_cloud/"
FONT = "_fonts/simhei.ttf"

FILE_SOURCE = "_source/What_I_talk_about_when_I_talk_about_running.txt"
MASK_IMG = "_mask/nike2.jpg"

text_raw = open(RUN_PATH + FILE_SOURCE,'r',encoding = 'UTF-8').read()
text_jieba = jieba.cut(text_raw,cut_all = True)
text_jieba_space = " ".join(text_jieba)
mask_img = np.array(Image.open(RUN_PATH + MASK_IMG))

wd_gen = WordCloud(font_path = RUN_PATH + FONT,
                   mask = mask_img,
                   contour_width = 3,
                   contour_color = 'steelblue',
                   max_words = 1000,
                   background_color = 'black').generate(text_jieba_space)
plt.imsave(RUN_PATH + FILE_SOURCE[8:].replace('.txt','.png'),wd_gen)
plt.imshow(wd_gen)
plt.axis("off")
plt.show()
```

效果(《当我谈跑步时我谈些什么》)

![What_I_talk_about_when_I_talk_about_running.png](https://upload-images.jianshu.io/upload_images/1711028-624e8c8db8f53b7f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 采用自定义的内容


## 美化



## 词云生成原理概览


## 一些好玩的分析
