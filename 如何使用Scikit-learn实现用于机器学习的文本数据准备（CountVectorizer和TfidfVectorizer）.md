## 如何使用Scikit-learn实现用于机器学习的文本数据准备（CountVectorizer和TfidfVectorizer）



* 词条化：通过解析来提取单词
* 特征化（量化）：单词编码为整数或者浮点数

文章目的

* 如何使用CounterVectorizer将文本转化成单词频数向量
* 如何使用TfidfVectorizer提取文本的单词权重向量
* HashingVectorizer???

### 词袋（Bag-of-words）模型，简称BOW

* 舍弃单词的顺序信息，关注单词的出现频率
* 然后给单词一个固定的数字编码。
* 主要关心编码方法和出现频率



### CountVectorizer---量化单词数量

* 文本文档的数据集转化成此条，并建立一个已知单词的词汇表，可以应用该词汇表对新文本进行编码
* 使用方法
  * 创建CountVectorizer类实例
  * 调用fit()函数，通过学习从一个或者多个文档中得出一个词汇表
  * 对一个或者多个文档应用transfrom()函数，将每个文档编码成一个向量。
* 关于文档编码成的向量：
  * 可以返回整个词汇表的长度，以及每个单词在该文档中出现的次数
  * 向量是稀疏的，我们可以使用。**scipy.sparse **库中有处理稀疏向量的有效方法。
  * 可以通过调用toarray()函数来把向量转化为numpy数组，得到更直观的表现。
* 下面是一个实例
* 重点来了：当给出了一个新文档text1时，假设text1里面出现了词汇表text里面没有出现的新单词怎么办？答案是**新单词**会被忽略掉，然后在得到的向量结果中不会给出新单词的出现次数。

### TfidfVectorizer—计算单词权重

* 首先简单的单词频数统计会出现问题，有些单词比如'the'会出现很多次，但是他们的出现对语意并没有太多的参考作用。
  * 有一个解决办法就是统计单词权重—TF-IDF(词频-逆文档频率，Term Frequency-Inverse Document Frequency),代表一个词对于一个文档的重要程度。
  * 词频：指的是某一个给定的词语在一篇文档中出现的次数
  * 逆文档频率：单词在文档中出现的频率越高，IDF值越低？？？（万一是个有用的词呢？？？）
  * TF_IDF给出的是单词权重，譬如在某篇文档中频率很高但是不会在所有文档中都频繁出现的单词。
* TidfVectorizer可以词条化文档，学习词汇表以及逆文档频率权重，还可以编码新文档。如果我们已经使用了ConuntVectorizer学习得到了向量，你可以对它使用Tfidftransformer函数，计算逆文档频率并且开始编码文件。

### 使用方法

* 创建实例
* fit学习
* transform

使用实例：

### 问题：

* Vector.idf  是怎么计算和使用的？
* transform()后得到的编码向量有什么意义？？？

### 参考

*  [如何使用Scikit-learn实现用于机器学习的文本数据准备（CountVectorizer和TfidfVectorizer）](http://www.infoq.com/cn/articles/prepare-text-data-machine-learning-scikit-learn) 
*  实例详见[**Logistic-regression-with-words-and-char-n-grams**](https://github.com/xjwsfgcs/Logistic-regression-with-words-and-char-n-grams)

