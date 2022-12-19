---
layout: post
title: cuda|ninja|pytorch|睡眠不足!
mathjax: true # false (default), true
mathjax_autoNumber: true # false (default), true
---
#  [pandas](https://geek-docs.com/pandas/pandas-tutorials/pandas-tutorial.html)
## 主要数据结构
**[dataframe](https://geek-docs.com/pandas/pandas-dataframe/python-pandas-dataframe.html)**
**[series](https://geek-docs.com/pandas/python-pandas-series/concatenate-multiindex-into-single-index-in-pandas-series.html)**
## 对数据的简单处理
### 1.读取数据
使用函数`pd.read_csv`
``` python
df = pd.read_csv([path], [header:数据的表头，不设置就是第一行，为None就是没有，给个0123作为表头], [sep:数据间间隔])
## 下为读取path下的scores.csv，含表头，间隔为,
df = pd.read_csv(path+'/scores.csv', sep=',')
```

### 2.获取数据
通过分析Dataframe的数据结构可以看出，Dataframe作为一个类的实例，数据存储其中，可以使用`df.name`来对列进行取值，也就是说：
一列数据作为一个一维的列表存储，列表的元素是元组，元组的地一个元素是该元素所在的行，第二个元素是该元素的值。
此外，Dataframe还重载了运算符`[[]]`，取列的值的时候还可以
```python
r_p = df[['recall', 'precision']]
## 也就是说通过运算符[[]]进行取列的操作
```
* * *
# [seaborn](https://huhuhang.com/post/machine-learning/seaborn-basic)

## 流程
1. sns.set()声明使用seaborn
2. plt.subplot等绘制子图、网格
3. sns.……画图
4. plt.show() 显示图片

## 声明
```python
sns.set(context='notebook', style='darkgrid', palette='deep', font='sans-serif', font_scale=1, color_codes=False, rc=None)
```
- context='' 参数控制着默认的画幅大小，分别有 {paper, notebook, talk, poster} 四个值。其中，poster > talk > notebook > paper。
- style='' 参数控制默认样式，分别有 {darkgrid, whitegrid, dark, white, ticks}，你可以自行更改查看它们之间的不同。
- palette='' 参数为预设的调色板。分别有 {deep, muted, bright, pastel, dark, colorblind} 等，你可以自行更改查看它们之间的不同。
- 剩下的 font='' 用于设置字体，font_scale= 设置字体大小，color_codes= 不使用调色板而采用先前的 'r' 等色彩缩写。

## 绘制
为了表达数据的分布情况，使用`jointplot`，其主要是用于绘制二元变量分布图，通过
```python
sns.jointplot(x='recall', y='precision', data=r_p, fill=True, levels=5, kind='kde')
```
绘图结果：
![c28bc5a7bb4ecc4f98ece762e4023e0b.png](:/assets/images/image.png)
jointplot并非figure级接口，支持 kind= 参数指定绘制出不同样式的分布图。
在kind下可以使用对应的参数。
- 可以在[这个link](https://seaborn.pydata.org/examples/index.html)找到找到想要画的样式，然后进行绘制
- 在[这个link](https://seaborn.pydata.org/generated/seaborn.color_palette.html#seaborn.color_palette)中选择想要的颜色

## 代码示例
```python
def scatter_plot(path:str):
    df = pd.read_csv(path + '/scores.csv', sep=',')
    r_p = df[['recall', 'precision']]
    sns.set(context='paper', style='darkgrid', palette='deep')
    fig = sns.jointplot(x='recall', y='precision', data=r_p, fill=True, levels=5, kind='kde')
    fig.savefig(path+'/recall_precision_kde.png',dpi=400)
    plt.suptitle('LSD recall precision distribution', y=1)
    fig.savefig(path+'/recall_precision_kde_title.png', dpi=400)
```
在该代码中，使用pandas读取数据为df，对要画图的部分取为r_p，通过sns.jointplot进行画图
一共画了两张，因为jointplot返回的不是一个图，而是由多张subplot组成的，所以在进行title时需要使用
```python
    plt.suptitle('LSD recall precision distribution', y=1)
```

## 补充: gallery
**[python_graph](https://www.python-graph-gallery.com/)**
**[各种图表的取舍](https://www.data-to-viz.com/caveats.html#page-top)**
