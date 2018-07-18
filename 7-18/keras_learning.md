# Keras: 基于 Python 的深度学习库
[官方文档](https://keras.io)

> **Keras** 是一个用 **Python** 编写的高级神经网络 **API**，它能够以[TensorFlow](https://github.com/tensorflow/tensorflow), [CNTK](https://github.com/Microsoft/cntk), 或者 [Theano](https://github.com/Theano/Theano) 作为后端运行。
**Keras** 的开发重点是支持快速的实验。
能够以最小的时延把你的想法转换为实验结果，是做好研究的关键。

 - 允许简单而快速的原型设计（由于用户友好，高度模块化，可扩展性）
 - 同时支持卷积神经网络和循环神经网络，以及两者的组合
 - 在 **CPU** 和 **GPU** 上无缝运行


 
> **Keras** 兼容的 **Python** 版本: __Python 2.7-3.6__.

------------------
# 指导原则

 - 用户友好。 Keras 是为人类而不是为机器设计的 API。它把用户体验放在首要和中心位置。Keras 遵循减少认知困难的最佳实践：它提供一致且简单的 API，将常见用例所需的用户操作数量降至最低，并且在用户错误时提供清晰和可操作的反馈。
 - 模块化。 模型被理解为由独立的、完全可配置的模块构成的序列或图。这些模块可以以尽可能少的限制组装在一起 。特别是神经网络层、损失函数、优化器、初始化方法、激活函数、正则化方法，它们都是可以结合起来构建新模型的模块。
 - 易扩展性。 新的模块是很容易添加的（作为新的类和函数），现有的模块已经提供了充足的示例。由于能够轻松地 创建可以提高表现力的新模块，Keras 更加适合高级研究。
 - 基于 Python 实现。 Keras 没有特定格式的单独配置文件。模型定义在 Python 代码中，这些代码紧凑，易于调试，并且易于扩展。

------------------
# 快速开始：30 秒上手 Keras

> __Keras__ 的核心数据结构是 __model__，一种组织网络层的方式。
最简单的模型是 [`Sequential`](https://keras.io/getting-started/sequential-model-guide)  顺序模型，它是由多个网络层线性堆叠的栈。
对于更复杂的结构，你应该使用 [Keras 函数式 API](https://keras.io/getting-started/functional-api-guide)，它允许构建任意的神经网络图。

`Sequential`顺序模型如下所示：
```python
from keras.models import Sequential

model = Sequential()
```

可以简单地使用`.add()` 来堆叠模型：
```python
from keras.layers import Dense

model.add(Dense(units=64, activation='relu', input_dim=100))
model.add(Dense(units=10, activation='softmax'))
```

在完成了模型的构建后, 可以使用 `.compile()` 来配置学习过程：

```python
model.compile(loss='categorical_crossentropy',
              optimizer='sgd',
              metrics=['accuracy'])
```

如果需要，你还可以进一步地配置你的优化器。
**Keras** 的核心原则是使事情变得相当简单，
同时又允许用户在需要的时候能够进行完全的控制（终极的控制是源代码的易扩展性）。

```python
model.compile(loss=keras.losses.categorical_crossentropy,
              optimizer=keras.optimizers.SGD(lr=0.01, momentum=0.9, nesterov=True))
```

现在，你可以批量地在训练数据上进行迭代了：

```python
# x_train and y_train are Numpy arrays --just like in the Scikit-Learn API.
model.fit(x_train, y_train, epochs=5, batch_size=32)
```

或者，你可以手动地将批次的数据提供给模型：

```python
model.train_on_batch(x_batch, y_batch)
```

只需一行代码就能评估模型性能：

```python
loss_and_metrics = model.evaluate(x_test, y_test, batch_size=128)
```

或者对新的数据生成预测：

```python
classes = model.predict(x_test, batch_size=128)
```

构建一个问答系统，一个图像分类模型，一个神经图灵机，或者其他的任何模型，就是这么的快。深度学习背后的思想很简单，那么它们的实现又何必要那么痛苦呢？

有关 **Keras** 更深入的教程，请查看：

- [开始使用 Sequential 顺序模型](https://keras.io/getting-started/sequential-model-guide)
- [开始使用函数式 API](https://keras.io/getting-started/functional-api-guide)

------------------

> 在代码仓库的 [examples 目录](https://github.com/keras-team/keras/tree/master/examples)中，
能找到更多高级模型：
**基于记忆网络的问答系统**、
**基于栈式LSTM 的文本生成**
等等。

------------------

[My Keras_Learning](https://github.com/Eurus-Holmes/keras_learning)

------------------




