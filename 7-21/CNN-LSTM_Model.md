# CNNs

> 卷积神经网络是最初为图片任务创建的网络，可以学习捕捉特定的特征而不管局部特征。
举一个更具体的例子，假设我们使用CNN来区分Cars和Dogs的照片。由于CNN学习捕捉特征而不管这些特征在哪里，CNN将会知道车有轮子，并且每次看到车轮时，无论它在图片的那个位置，该特征将会被激活。
在我们特定的情况下，CNN可以捕捉一个消极的短语，例如“不喜欢”而不管它在文中的什么位置。

 - 我不喜欢这些类型的电影
 - 那一件事情我真的不喜欢
 - 我看过这个电影，但是不喜欢它的结局。

![Figure 1](https://github.com/Text-sentiment-analysis-bjfu/work_log/raw/master/7-21/images/1.png)

----------

# LSTMs

> 长短期记忆(LSTM) 是一种网络，具有记忆来自输入的先前数据并基于该知识作出决定的存储器。
这些网络更直接适用于书面数据的输入。
因为在句子中的每一个单词都有基于周围的单词的含义（先前和即将出现的单词）。
在我们的具体情况中，LSTM有可能让我们能够在文中捕捉到不断变化的情绪。
例如，一个句子，`“At first I loved it, but then I ended up hating it.”`
有相矛盾的观点，最终会导致简单的前馈网络混淆。
另一方面，LSTM可以得知，在句子结尾处表达的意思比一开始表达的意思更重要。

![Figure 2](https://github.com/Text-sentiment-analysis-bjfu/work_log/raw/master/7-21/images/2.jpeg)

----------

# CNN-LSTM 模型

> CNN-LSTM 模型结合由初始的卷积层组成，这将接收word embedding（对文档中每个不同的单词都得到一个对应的向量）作为输入。然后将其输出汇集到一个较小的尺寸，然后输入到LSTM层。隐藏在这个模型后面的直觉是卷积层将提取局部特征，然后LSTM层将能够使用所述特征的排序来了解输入的文本排序。

![Figure 3](https://github.com/Text-sentiment-analysis-bjfu/work_log/raw/master/7-21/images/3.png)

----------


