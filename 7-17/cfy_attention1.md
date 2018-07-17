> [参考链接](https://blog.csdn.net/malefactor/article/details/50550211)

----------
# Encoder-Decoder框架

> 本文暂且只谈**NLP领域的Attention Model**，其实在图片处理或者（图片-图片标题）生成等任务中也有很多场景会应用**Attention Model**，机制也是相同的。


要提**NLP领域的Attention Model**，就不得不先谈**Encoder-Decoder**框架，因为目前绝大多数文献中出现的**Attention Model**是附着在**Encoder-Decoder**框架下的，当然，其实**Attention Model**可以看作一种通用的思想，本身并不依赖于**Encoder-Decoder**模型。

下图是NLP领域里常用的**Encoder-Decoder**框架最抽象的一种表示：

![1](https://leanote.com/api/file/getImage?fileId=5b4de432ab6441529f00348d)
<p align="center">图1. 抽象的Encoder-Decoder框架</p>


**Encoder-Decoder**框架可以这么直观地去理解：
可以把它看作适合处理由一个句子（或篇章）生成另外一个句子（或篇章）的通用处理模型。
对于句子对$<X,Y>$，我们的目标是给定输入句子$X$，期待通过**Encoder-Decoder**框架来生成目标句子$Y$。
$X$和$Y$可以是同一种语言，也可以是两种不同的语言。
而$X$和$Y$分别由各自的单词序列构成：

$$
X=<x_1,x_2...x_m>
$$
$$
Y=<y_1,y_2...y_n>
$$

**Encoder**顾名思义就是对输入句子$X$进行编码，将输入句子通过非线性变换转化为中间语义表示$C$：

$$C=\Gamma(x_1,x_2...x_m)$$

对于解码器**Decoder**来说，其任务是根据句子$X$的中间语义表示$C$和之前已经生成的历史信息$y_1,y_2...y_{i-1}$来生成$i$时刻要生成的单词$y_i$：

$$y_i=\Upsilon(C,y_1,y_2...y_{i-1})$$

每个$y_i$都依次这么产生，那么看起来就是整个系统根据输入句子$X$生成了目标句子$Y$.

----------
# Attention Model

> 图$1$中展示的**Encoder-Decoder**模型是没有体现出“注意力模型”的，所以可以把它看作是注意力不集中的分心模型。为什么说它注意力不集中呢？请观察以下目标句子$Y$中每个单词的生成过程如下：

$$
\begin{align}
y_1=& \quad f(C) \\
y_2=& \quad f(C,y_1) \\
y_3=& \quad f(C,y_1,y_2)
\end{align}
$$

> 其中$f$是**decoder**的非线性变换函数。
从这里可以看出，在生成目标句子的单词时，不论生成哪个单词，是$y_1$,$y_2$也好，还是$y_3$也好，他们使用的句子$X$的语义编码$C$都是一样的，没有任何区别。
而语义编码$C$是由句子$X$的每个单词经过**Encoder** 编码产生的，这意味着不论是生成哪个单词，$y_1$,$y_2$还是$y_3$，其实句子$X$中任意单词对生成某个目标单词$y_i$来说影响力都是相同的，没有任何区别。
这就是为何说这个模型没有体现出注意力的缘由。
这类似于你看到眼前的画面，但是没有注意焦点一样。
如果拿机器翻译来解释这个分心模型的**Encoder-Decoder**框架更好理解。
比如输入的是英文句子：
`Tom chase Jerry`，
**Encoder-Decoder**框架逐步生成中文单词：
`“汤姆”，“追逐”，“杰瑞”`。
在翻译“杰瑞”这个中文单词的时候，
分心模型里面的每个英文单词对于翻译目标单词“杰瑞”贡献是相同的，很明显这里不太合理，显然“Jerry”对于翻译成“杰瑞”更重要，但是分心模型是无法体现这一点的，这就是为何说它没有引入注意力的原因。
没有引入注意力的模型在输入句子比较短的时候估计问题不大，但是如果输入句子比较长，此时所有语义完全通过一个中间语义向量来表示，单词自身的信息已经消失，可想而知会丢失很多细节信息，这也是为何要引入注意力模型的重要原因。

上面的例子中，如果引入**Attention Model**的话，应该在翻译“杰瑞”的时候，体现出英文单词对于翻译当前中文单词不同的影响程度，比如给出类似下面一个概率分布值：

    (Tom,0.3) (chase,0.2) (Jerry,0.5)
    
每个英文单词的概率代表了翻译当前单词“杰瑞”时，注意力分配模型分配给不同英文单词的注意力大小。
这对于正确翻译目标语单词肯定是有帮助的，因为引入了新的信息。
同理，目标句子中的每个单词都应该学会其对应的源语句子中单词的注意力分配概率信息。
这意味着在生成每个单词$y_i$的时候，原先都是相同的中间语义表示$C$会替换成根据当前生成单词而不断变化的$C_i$.
理解**Attention Model**的关键就是这里，即由固定的中间语义表示$C$换成了根据当前输出单词来调整成加入注意力模型的变化的$C_i$.
增加了**Attention Model**的**Encoder-Decoder**框架理解起来如图$2$所示。

![2](https://leanote.com/api/file/getImage?fileId=5b4de476ab6441529f003497)
<p align="center">图2.引入Attention Model的Encoder-Decoder框架</p>


即生成目标句子单词的过程成了下面的形式：

$$
\begin{align}
y_1=& \quad f(C_1) \\
y_2=& \quad f(C_2,y_1) \\
y_3=& \quad f(C_3,y_1,y_2)
\end{align}
$$

而每个$C_i$可能对应着不同的源语句子单词的注意力分配概率分布，
比如对于上面的英汉翻译来说，其对应的信息可能如下：

![3](https://leanote.com/api/file/getImage?fileId=5b4de51bab6441529f0034aa)

其中，$f_2$函数代表**Encoder**对输入英文单词的某种变换函数，
比如如果**Encoder**是用的**RNN模型**的话，
这个$f_2$函数的结果往往是某个时刻输入$x_i$后隐层节点的状态值；
$g$代表**Encoder**根据单词的中间表示合成整个句子中间语义表示的变换函数，
一般的做法中，$g$函数就是对构成元素加权求和，也就是常常在论文里看到的下列公式：

$$C_i=\sum_{j=1}^{T_x}\alpha_{ij}h_j$$

假设$C_i$中那个$i$就是上面的“汤姆”，
那么$T_x$就是3，代表输入句子的长度，
$h_1=f(“Tom”)$，
$h_2=f(“Chase”)$,
$h_3=f(“Jerry”)$，
对应的注意力模型权值分别是$0.6,0.2,0.2$，
所以$g$函数就是个加权求和函数。
如果形象表示的话，翻译中文单词“汤姆”的时候，数学公式对应的中间语义表示$C_i$的形成过程类似下图：

![4](https://leanote.com/api/file/getImage?fileId=5b4de662ab6441548c002d01)
<p align="center">图3.$C_i$的形成过程</p>


这里还有一个问题：生成目标句子某个单词，比如“汤姆”的时候，是怎么知道Attention Model所需要的输入句子单词注意力分配概率分布值呢？
就是说“汤姆”对应的概率分布：

    (Tom,0.6) (Chase,0.2) (Jerry,0.2)
    
是如何得到的呢？

> 为了便于说明，我们假设对图$1$的**非Attention Model**的**Encoder-Decoder**框架进行细化，
**Encoder**采用**RNN模型**，
**Decoder**也采用**RNN模型**，
这是比较常见的一种模型配置，则图$1$的图转换为下图：

![5](https://leanote.com/api/file/getImage?fileId=5b4de72aab6441529f0034de)
<p align="center">图4.RNN作为具体模型的Encoder-Decoder框架</p>


> 那么用下图可以较为便捷地说明注意力分配概率分布值的通用计算过程：

![6](https://leanote.com/api/file/getImage?fileId=5b4de773ab6441548c002d38)
<p align="center">图5.Attention分配概率计算</p>


> 对于采用**RNN**的**Decoder**来说，
如果要生成$y_i$单词，在时刻$i$，我们是可以知道在生成$y_i$之前的隐层节点$i$时刻的输出值$H_i$的，
而我们的目的是要计算生成$y_i$时的输入句子单词`“Tom”、“Chase”、“Jerry”`对$y_i$来说的注意力分配概率分布，
那么可以用$i$时刻的隐层节点状态$H_i$去一一和输入句子中每个单词对应的**RNN**隐层节点状态$h_j$进行对比，
即通过函数$F(h_j,H_i)$来获得目标单词$y_i$和每个输入单词对应的对齐可能性，
这个$F$函数在不同论文里可能会采取不同的方法，
然后函数$F$的输出经过**Softmax**进行归一化就得到了符合概率分布取值区间的注意力分配概率分布数值。
图$5$显示的是当输出单词为“汤姆”时刻对应的输入句子单词的对齐概率。
绝大多数**Attention Model**都是采取上述的计算框架来计算注意力分配概率分布信息，区别只是在$F$的定义上可能有所不同。
<br>
上述内容就是论文里面常常提到的**Soft Attention Model**的基本思想，在文献里看到的大多数**Attention Model**基本就是这个模型，区别很可能只是把这个模型用来解决不同的应用问题。

那么怎么理解**Attention Model**的物理含义呢？
一般文献里会把**Attention Model**看作是单词对齐模型，这是非常有道理的。
目标句子生成的每个单词对应输入句子单词的概率分布可以理解为输入句子单词和这个目标生成单词的对齐概率，
这在机器翻译语境下是非常直观的：传统的统计机器翻译一般在做的过程中会专门有一个短语对齐的步骤，而注意力模型其实起的是相同的作用。
在其他应用里面把**Attention Model**理解成输入句子和目标句子单词之间的对齐概率也是很顺畅的想法。

当然，从概念上理解的话，把**Attention Model**理解成影响力模型也是合理的，就是说生成目标单词的时候，输入句子每个单词对于生成这个单词有多大的影响程度。
这种想法也是比较好理解**Attention Model**物理意义的一种思维方式。

图$6$是论文**“A Neural Attention Model for Sentence Summarization”**中，**Rush**用**Attention Model**来做生成式摘要给出的一个非常直观的例子。

![7](https://leanote.com/api/file/getImage?fileId=5b4dea81ab6441548c002d92)
<p align="center">图6.句子生成式摘要例子</p>


这个例子中，**Encoder-Decoder**框架的输入句子是：
`“russian defense minister ivanov called sunday for the creation of a joint front for combating global terrorism”`。
对应图中纵坐标的句子。

系统生成的摘要句子是：
`“russia calls for joint front against terrorism”`，
对应图中横坐标的句子。

可以看出模型已经把句子主体部分正确地抽出来了。
矩阵中每一列代表生成的目标单词对应输入句子每个单词的**Attention Model**分配概率，颜色越深代表分配到的概率越大。
这个例子对于直观理解**Attention Model**也是很有帮助的。        

----------


