Formats de fichiers
===================

该章节展示了由Unitex读取或生成文件的不同格式。DELAS和DEKLAF字典的格式都在[section-DELAF-format]和
[section-DELAS-format].中表示。

注意：在这一章节中， ¶
符号表示换行。除非另有说明，所有的在该章节中的文本文件都是由Unicode
Little-Endian进行编码的。

Codage Unicode
--------------

默认由Unitex操作的文本文件由Unicode Little-Endian编码。
Unitex也接受Unicode
Big-Endian格式或UTF-8格式文件。这个编码可以表示65536个字符，每两个字节构成一个字符。Little-Endian代码中，字节是以由低到高的顺序排列。而Big-Endian的顺序则是相反。一个由
Little-Endian, Big-Endian或UTF-8变码的文件由16进制特殊字符
``FF``\ ``FE``\ (Little-Endian)、``FE``\ ``FF``
(Big-Endian)或``EF``\ ``BB``\ ``BF`` (UTF-8)开始（Unicode Byte Order
Mark - BOM）。因为UTF-8没有字节顺序，在BOM
UTF-8添加是可选的；对于UTF-16来说是必须的。跨行符号应由\ ``0D``\ ``00``
和\ ``0A``\ ``00``
(Little-Endian)，``00``\ ``0D``\ 和\ ``00``\ ``0A``\ (Big-Endian)或``0D``\ 和\ ``0A``\ (UTF-8)两个字符构成。

参考以下文本：

``Unitex¶``

``\beta-version¶``

这里是由Unicode Little-Endian编码文本：

+------------------+------------------+------------------+------------------+------------------+------------------+------------------+----------------------------------+----------------------------------+
| BOM header       | U                | n                | i                | t                | e                | x                | ¶                                | :math:`\beta`                    |
+==================+==================+==================+==================+==================+==================+==================+==================================+==================================+
| ``FF``\ ``FE``   | ``55``\ ``00``   | ``6E``\ ``00``   | ``69``\ ``00``   | ``74``\ ``00``   | ``65``\ ``00``   | ``78``\ ``00``   | ``0D``\ ``00``\ ``0A``\ ``00``   | ``B2``\ ``03``                   |
+------------------+------------------+------------------+------------------+------------------+------------------+------------------+----------------------------------+----------------------------------+
| -                | v                | e                | r                | s                | i                | o                | n                                | ¶                                |
+------------------+------------------+------------------+------------------+------------------+------------------+------------------+----------------------------------+----------------------------------+
| ``2D``\ ``00``   | ``76``\ ``00``   | ``65``\ ``00``   | ``72``\ ``00``   | ``73``\ ``00``   | ``69``\ ``00``   | ``6F``\ ``00``   | ``6E``\ ``00``                   | ``0D``\ ``00``\ ``0A``\ ``00``   |
+------------------+------------------+------------------+------------------+------------------+------------------+------------------+----------------------------------+----------------------------------+

Table: 16进制表示由Unicode Little-Endian编码的文本

这里是由Unicode Big-Endian表示的：

+------------------+------------------+------------------+------------------+------------------+------------------+------------------+----------------------------------+----------------------------------+
| BOM header       | U                | n                | i                | t                | e                | x                | ¶                                | :math:`\beta`                    |
+==================+==================+==================+==================+==================+==================+==================+==================================+==================================+
| ``FE``\ ``FF``   | ``00``\ ``55``   | ``00``\ ``6E``   | ``00``\ ``69``   | ``00``\ ``74``   | ``00``\ ``65``   | ``00``\ ``78``   | ``00``\ ``0D``\ ``00``\ ``0A``   | ``03``\ ``B2``                   |
+------------------+------------------+------------------+------------------+------------------+------------------+------------------+----------------------------------+----------------------------------+
| -                | v                | e                | r                | s                | i                | o                | n                                | ¶                                |
+------------------+------------------+------------------+------------------+------------------+------------------+------------------+----------------------------------+----------------------------------+
| ``00``\ ``2D``   | ``00``\ ``76``   | ``00``\ ``65``   | ``00``\ ``72``   | ``00``\ ``73``   | ``00``\ ``69``   | ``00``\ ``6F``   | ``00``\ ``6E``                   | ``00``\ ``0D``\ ``00``\ ``0A``   |
+------------------+------------------+------------------+------------------+------------------+------------------+------------------+----------------------------------+----------------------------------+

Table: 16进制表示由Unicode Big-Endian编码的文本

这里是由UTF-8表示的：

+--------------------------+----------+----------+----------+----------+----------+----------+------------------+------------------+
| BOM header               | U        | n        | i        | t        | e        | x        | ¶                | :math:`\beta`    |
+==========================+==========+==========+==========+==========+==========+==========+==================+==================+
| ``EF``\ ``BB``\ ``BF``   | ``55``   | ``6E``   | ``69``   | ``74``   | ``65``   | ``78``   | ``0D``\ ``0A``   | ``CE``\ ``B2``   |
+--------------------------+----------+----------+----------+----------+----------+----------+------------------+------------------+
| -                        | v        | e        | r        | s        | i        | o        | n                | ¶                |
+--------------------------+----------+----------+----------+----------+----------+----------+------------------+------------------+
| ``2D``                   | ``76``   | ``65``   | ``72``   | ``73``   | ``69``   | ``6F``   | ``6E``           | ``0D``\ ``0A``   |
+--------------------------+----------+----------+----------+----------+----------+----------+------------------+------------------+

Table: 16进制表示由UTF-8编码的文本

Unicode
Little-Endian编码中，高位字节和低位字节是倒过来的，这说明开始的字符是由
``FF``\ ``FE``\ 编码，而不是\ ``FE``\ ``FF``\ ，同上，\ ``00``\ ``0D``
和 ``00``\ ``0A``\ 分别变成\ ``0D``\ ``00``\ 和\ ``0A``\ ``00``\ 。

字母文件
--------

有两种字母文件输出格式：一个是定义一种语言的字符，还有一种是显示了字符的排序。第一个被称为\ *alphabet*\ ，第二个被称为\ *alphabet
de tri*\ 。

字母
~~~~

字母文件是记录一种语言中所有字符与小写和大写字母之间的对应关系的文本文件。该文件被称为\ ``Alphabet.txt``
，可以在相关语言根目录中被找到。Unitex能够运行必须要它的存在。

举例～：英文字母文件可以在\ ``.../English/``\ 目录里找到。

字母文件的每一行都应该有三种以下形式之一，然后另起一行：

-  |image| :
   在\ :math:`X`\ 和\ :math:`Y`\ 两个字符后的升号表示所有在\ :math:`X`\ 和\ :math:`Y`\ 字符中包含的所有字符都是字母。
   所有字符都同时被认为是大写或小写。这种模式被用来定义亚洲语言的字，比如韩语，中文，日语，不区分大小写或返回的字符数太繁琐，枚举出来太多

-  ``Aa`` :
   :math:`X`\ 和\ :math:`Y`\ 两个字符表示\ :math:`X`\ 和\ :math:`Y`\ 是两个字母并且\ :math:`X`\ 等效于大小字母\ :math:`Y`\ 。

-  |image|: 单独的字符\ :math:`X`\ 表示\ :math:`X`\ 同时作为大小写字母。
   这种模式适用于及时处理亚洲语言。

对于某些类似于法语的语言，会有一个小写字母对应大写字母的情况。比如\ ``é``\ ，大写字母可以是\ ``E或\texttt{\'E}。为了表示它，只要使用多线操作。反过来也是一样：一个大写字母可以对应多个小写字母。因此\verb``\ E+
可以是\ ``e``, ``é``, ``è``,
``ë``\ 或\ ``ê``\ 的大写字母。这里是法语字母文件处理定义不同的字母

``e``:

``Ee``\ ¶

``Eé``\ ¶

``Éé``\ ¶

``Eè``\ ¶

``Èè``\ ¶

``Eë``\ ¶

``Ëë``\ ¶

``Eê``\ ¶

``Êê``\ ¶

顺序字母表
~~~~~~~~~~

顺序字母表是一个文本文件，它在\ ``SortTxt``\ 程序的帮助下定义了一种语言的字母排序
文件中的每一行定义一组字母。如果\ :math:`A`\ 组的字母在\ :math:`B`\ 之前就定义好，\ :math:`A`\ 中的任何字母都比\ :math:`B`\ 中的任何字母高级。

同一组的字母非必要的情况下不需要区分。比如，如果我们定义一组字母\ ``eéèëê``\ ，\ ``ébahi``
就会被看作比\ ``estuaire``\ 更小，而它本身比\ ``été``\ 更小。\ ``e``\ 和
``é``
后的字母可以用于分类这些单词，我们没有找来比较\ ``e``\ 和\ ``é``\ ，因为它们在同一个组。
另一方面，如果我们比较\ ``chantés``\ 和\ ``chantes``\ ，\ ``chantes``
更小。实际上，应该比较\ ``e``\ 和\ ``é`` 来区分这两个单词。
``e``\ 出现在字母组\ ``eéèëê``\ 的第一个，它在\ ``é``\ 前面。因此\ ``chantes``
被看作比 ``chantés``\ 更小的单词。

顺序字母表文件可以定义等效字符。因此我们能忽视发音的不同。比如如果我们要给字母\ ``b``,
``c``, 和\ ``d``\ 排序，不区分大小写和变音符号，我们可以写出如下几行：

``Bb``\ ¶

``CcÇç``\ ¶

``Dd``\ ¶

这个文件是可选的，当在给Unicode编码字符排序的\ ``SortTxt``\ 程序中没有顺序字母表时。

图形
----

本节介绍图的两种格式：图形格式 ``.grf``\ 和编译格式 ``.fst2``\ 。

Format .grf
~~~~~~~~~~~

``.grf``\ 文件是含有除了信息表示的框和图表的转换内容的提示信息的文本文件。\ ``.grf``\ 文件由下面的内容开始：

``#Unigraph``\ ¶

``SIZE 1313 950``\ ¶

``FONT Times New Roman:  12``\ ¶

``OFONT Times New Roman:B 12``\ ¶

``BCOLOR 16777215``\ ¶

``FCOLOR 0``\ ¶

``ACOLOR 12632256``\ ¶

``SCOLOR 16711680``\ ¶

``CCOLOR 255``\ ¶

``DBOXES y``\ ¶

``DFRAME y``\ ¶

``DDATE y``\ ¶

``DFILE y``\ ¶

``DDIR y``\ ¶

``DRIG n``\ ¶

``DRST n``\ ¶

``FITS 100``\ ¶

``PORIENT L``\ ¶

``#``\ ¶

第一行\ ``#Unigraph`` 是评论行。下面的几行定义图形演示设置的值：

-  ``SIZE x y`` : 定义以像素为单位的图的宽度 ``x`` 和高度verb+y+ d；

-  ``FONT name:xyz`` : 设置用于显示框的内容的字体。 ``name``
   是字体的名字. ``x`` 定义字体是否加粗. 如果 ``x`` 是 ``B``,
   表示字体加粗. 对于正常的字体来说, ``x``\ 是一个空格. 同样, ``y`` 是
   ``I`` 如果字体是斜的，否则就是一个空格。 ``z`` 表示字体的大小;

-  ``OFONT name:xyz`` : 设置用于显示转导的字体。 参数\ ``name``, ``x``,
   ``y``, 和 ``z`` 同样定义 ``FONT``;

-  ``BCOLOR x`` : 设置图形的背景的色彩。 ``x`` 表示RGB格式颜色;

-  ``FCOLOR x`` : 定义图形绘制颜色。 ``x`` 表示RGB格式的颜色;

-  ``ACOLOR x`` :
   定义用于对应子图的框的颜色。\ ``x``\ 表示表示RGB格式的颜色。

-  ``SCOLOR x`` : 定义用来写的评论框的内容的颜色 (i.e.
   未链接到任何其他的框)。\ ``x``\ 表示RGB格式的颜色。

-  ``CCOLOR x`` : 设置用于绘制选择框的颜色。 ``x``
   表示表示RGB格式的颜色;

-  ``DBOXES x`` : 这一行语句被Unitex忽视。它是为了保存图索引的兼容性；

-  ``DFRAME x`` :
   根据\ ``x``\ 的值为\ ``y``\ 或\ ``n``\ 来决定为图的框架作图或不作图；

-  ``DDATE x`` :
   根据\ ``x``\ 的值为\ ``y``\ 或\ ``n``\ 来决定是不是在图的底部显示时间；

-  ``DFILE x`` :
   根据\ ``x``\ 的值为\ ``y``\ 或\ ``n``\ 来决定图的底部是否显示文件的名字；

-  ``DDIR x`` : 根据\ ``x``\ 的值为
   ``y``\ 或\ ``n``\ 来决定是否在图的底部显示打开文件的完整路径；
   这个操作只在\ ``DFILE``\ 参数的值为\ ``y``\ 的时候考虑；

-  ``DRIG x`` : 根据\ ``x``\ 的值为\ ``y``\ ，或
   ``n``\ 来决定图是从左向右还是从右向左；

-  ``DRST x`` : 这一行语句被Unitex忽视。它是为了保存图索引的兼容性；

-  ``FITS x`` : 这一行语句被Unitex忽视。它是为了保存图索引的兼容性；

-  ``PORIENT x`` : 这一行语句被Unitex忽视。它是为了保存图索引的兼容性；

-  ``#`` : 这一行语句被Unitex忽视。它从信息的开始指向结尾。

下面的几行语句表示内容和图的位置。之后的几行对应于图形识别图：

``3``\ ¶

``"<E>" 84 248 1 2 ``\ ¶

``"" 272 248 0 ``\ ¶

``s"1+2+3+4+5+6+7+8+9+0" 172 248 1 1 ``\ ¶

第一行语句表示图的编号，随后另起一行。这个数字不能小于二，因为一个图形总是
被认为至少拥有一个初始状态和最终状态

下面的语句表示图形框。这些框从\ :math:`0`\ 开始编号，\ :math:`0`\ 是初始状态，\ :math:`1`\ 是最终状态。最终状态的内容总是空的。

每一个图的框都被有如下格式的语句定义

*contenu X Y N transitions ¶*

*内容*\ 是用引号括起来的字符串，它代表了框的内容。这个字符串可任意由在倒入图形索引\ ``s``\ 的情况下形成；该字符被Unitex忽视。字符串的内容是在图形编辑器的文本控制其中的文本。[table10-2]给出未在文件\ ``.grf``:编码为这样的两个特殊序列的编码

+--------------------------------------------+------------+
| ``.grf``\ 文件中序列和图片编辑器中的序列   |            |
+============================================+============+
| ``"``                                      | ``\"``     |
+--------------------------------------------+------------+
| ``\"``                                     | ``\\\"``   |
+--------------------------------------------+------------+

Table: 特殊的编码序列[table10-2]

注意：\ ``<``\ 与\ ``>``\ 中的或\ ``{``\ 和\ ``}`` 的字符不是注释。因此
``+``\ 符号在\ ``"le <A+Conc>"``
字符串中不是分隔符的意思，因为\ ``<A+Conc>``\ 优先解释。

*X* and *Y*\ 表示像素框的坐标. 图 [fig-box-coordinates]
显示这些坐标是如何被Unitex解释。

.. figure:: resources/img/repere.pdf
   :alt: Interprétation des coordonnées des boîtes[fig-box-coordinates]
   :width: 7.00000cm

   Interprétation des coordonnées des boîtes[fig-box-coordinates]

*N* 表示从框中转换的次数。该数字在最终状态下总为\ :math:`0`\ 。

这些转换由它们所指向的框的号码定义。

每一行定义箱必须用一个空格，接着一个换行符结束。

Format .fst2
~~~~~~~~~~~~

``.fst2``\ 文件是一个文本文件描述图的集合。这里是\ ``.fst2``
file文件的例子：

``0000000002``\ ¶

``-1 NP``\ ¶

``: 1 1 ``\ ¶

``: 2 2 -2 2 ``\ ¶

``: 3 3 ``\ ¶

``t ``\ ¶

``f ``\ ¶

``-2 Adj``\ ¶

``: 6 1 5 1 4 1 ``\ ¶

``t ``\ ¶

``f ``\ ¶

``%<E>``\ ¶

``%the/DET``\ ¶

``%<A>/ADJ``\ ¶

``%<N>``\ ¶

``%nice``\ ¶

``@pretty``\ ¶

``%small``\ ¶

``f``\ ¶

第一行表示文件里已经编码的图片号码。每个图的开头由指向号码和图的名称的语句定义。
( (``-1 NP`` et ``-2 Adj`` dans le fichier ci-dessus)。

之后的语句描述图的状态。如果状态为结束，语句由\ ``t``\ 开始，否则由\ ``:``\ 开始
``:``\ 。对于每一种状态，转换列表可能是一系列可能为空的整数对：

-  第一个整数表示标签号码或与转换相对应的子图的号码。
   标签从0开始编号。子图由负整数表示，图的编号都为负数；

-  第二个整数表示转换到达时的状态。在每一个图中，状态都从0开始标记，按照惯例，0状态时初始状态。

每个状态定义行必须以空格结尾。
每一幅图的结尾都要被包含一个空格和换行后的\ ``f``\ 符号的语句标记。

标签在最后一个图之后被定义。如果语句由\ ``@``\ 开始，表示标签的内容应在没有变化的条件下查找。这个信息之外标签是一个单词的时候被使用。如果语句由
``%`` 开始，变化的情况已经被授权。如果一个标签支持转换，输入和输出序列被
``/``\ (比如 : ``the/DET``)分开。按惯例来说，第一个标签总是空的
(``<E>``)，即使标签未在任何转换中使用。

文件的末尾由换行后包含f的字符的语句指出。

Textes
------

这个章节表示用来表示文本的不同文件。

文件 .txt
~~~~~~~~~

[section-texts] ``.txt``\ 文件应该是由 Unicode
Little-Endian编码的文本文件。这些文件不应包含闭合或开启的大括号，除非它们被用来写一个句子分离器
(``{S}``)
或一个有效的词汇标签(\ ``{aujourd'hui,.ADV}``)，回车必须由两个特殊字符十六进制值编码\ ``000D``\ 和\ ``000A``\ 。

文件.snt
~~~~~~~~

``.snt``\ 是Unitex处理过的\ ``.txt``\ 文件。这些文件不包含标签。在连续的语句中不包含多个空格或回车。\ ``.snt``\ 文件中只有用来分开句子\ ``{S}``
的大括号和词汇标 (``{aujourd'hui,.ADV}``)签的大括号才会被授权。

文本文件.cod
~~~~~~~~~~~~

``text.cod``
文件是一个二进制文件包含一系列整数来表示文档。每一个整数\ ``i``\ 在\ ``tokens.txt``\ 文件中返回标记索引\ ``i``\ 。这些整数占用4个字节。

注意：这些令牌从0开始标记。

令牌文件.txt
~~~~~~~~~~~~

[fichier-tokens-txt] ``tokens.txt``
文件是一个文本文件包含所有词汇文本单元列表的文件。文件的第一行语句表示包含在文件中的单元的数目。每一个单元通过换行隔开。当文档中的一个系列随着变化的情况找到时，每一个变体子都被一个独立的单元编码。

注意：\ ``.snt``
文件中可能出现的回车是和空格一样被编码的。因此从来没有回车的编码单元。

Fichier tok\_by\_alph.txt et tok\_by\_freq.txt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

这两个文件是按字母顺序或字幕出现频率包含排序词汇单元列表的文本文件。

``tok_by_alph.txt``\ 文件中，每一行语句包含一个单元，接着是制表符和这个单元在文本中出现的次数
``tok_by_freq.txt``\ 文件中的语句是因相同的原理形成的，但是制表符和单元前面会显示出现次数。

Fichier enter.pos
~~~~~~~~~~~~~~~~~

这个文件是包含fichier
``.snt``\ 文件中的换行符位置列表的二进制文件。每个位置都是text.cod
文件中用空格代替回车键的指数。这些位置是由4位二进制表示的整数。

文本自动机
----------

Fichier text.tfst
~~~~~~~~~~~~~~~~~

``text.tfst``\ 文件表示文本自动机。这是与十位指示中包含的控制器句子的数目的行开始的文本文件。接着对于每一个句子，它具有以下标题：

-  ``$XXX``\ ¶: ``XXX`` = numéro de la phrase;

-  ``foo foo foo...``\ ¶: 句子文本;

-  ``a/b c/d e/f g/h...``\ ¶: 对于每个句子的令牌, 有一个 ``x/y``\ 部分:
   ``x`` 是该文件中的标记索引\ ``tokens.txt``, ``y`` 是它的字符长度;

-  ``X_Y``\ ¶: ``X``
   是从文本开始的第一个句子令牌的偏移量；\ ``Y``\ 是相同的但是偏移量表示的是字符数。

然后，所有自动机的状态都被逐行编码。如果状态是最终状态，语句由\ ``t``.开始。否则，由\ ``:``\ 开始。所有的转变都由\ ``x y``,
``x``\ 部分的形式来描述作为数字标签，\ ``y``\ 是目的状态数。注意与\ ``.fst2``\ 格式不同，语句要由空格来结束。状态列表的最后一行语句包含\ ``f``\ 。

最后，所有的标签进行编码。按照惯例，第一个标签总是是最小值： ``@<E>``\ ¶

``.``\ ¶

其他标签应该要么是词汇单元或大括号里DELAF格式的入口。它的编码如下：

``@STD``\ ¶

``@``\ *content*\ ¶

``@``\ *a*\ ``.``\ *b*\ ``.``\ *c*\ ``-`` *x*\ ``.``\ *y*\ ``.``\ *z*\ ¶

``.``\ ¶

*内容* 是标签内容.信息 *a.b.c-x.y.z* 描述由标签所覆盖的文本区:

-  *a*: 通过自句子的开头令牌起始偏移;

-  *b*: 在从第一开头字符，令牌标签;开始偏移; token du tag;

-  *c*:
   从标签的第一个字符的逻辑字母开头偏移。这个信息对于韩语有用的，因为一个标记代表
   Jamo符号出现在朝鲜语内的字符序列。因此字符偏移量不够准确；

-  *x*: 从句头开始，结尾用令牌抵消；

-  *y*: 从标签的最后一个令牌的开头字符结束偏移;

-  *z*:
   因为标签的最后一个字符的字母逻辑结束。在韩语的句子自动机中，空表面的形成能对应空的文本。在这种情况下，\ *z*\ 得值为\ :math:`-1`\ 。

标签的定义由包含\ ``f``\ 的语句结束。

举例 : 这是与文本 *He is drinking orange juice.*\ 对应的文件

``0000000001``\ ¶

``$1``\ ¶

``He is drinking orange juice. ``\ ¶

``0/2 1/1 2/2 1/1 3/8 1/1 4/6 1/1 5/5 6/1 1/1``\ ¶

``0_0``\ ¶

``: 2 1 1 1``\ ¶

``: 4 2 3 2``\ ¶

``: 7 3 6 3 5 3``\ ¶

``: 10 5 9 4 8 4``\ ¶

``: 12 5 11 5``\ ¶

``: 13 6``\ ¶

``t``\ ¶

``f``\ ¶

``@<E>``\ ¶

``.``\ ¶

``@STD``\ ¶

``@{He,he.N:s:p}``\ ¶

``@0.0.0-0.1.0``\ ¶

``.``\ ¶

``@STD``\ ¶

``@{He,he.PRO+Nomin:3ms}``\ ¶

``@0.0.0-0.1.0``\ ¶

``.``\ ¶

``@STD``\ ¶

``@{is,be.V:P3s}``\ ¶

``@2.0.0-2.1.0``\ ¶

``.``\ ¶

``@STD``\ ¶

``@{is,i.N:p}``\ ¶

``@2.0.0-2.1.0``\ ¶

``.``\ ¶

``@STD``\ ¶

``@{drinking,drinking.A}``\ ¶

``@4.0.0-4.7.0``\ ¶

``.``\ ¶

``@STD``\ ¶

``@{drinking,drinking.N:s}``\ ¶

``@4.0.0-4.7.0``\ ¶

``.``\ ¶

``@STD``\ ¶

``@{drinking,drink.V:G}``\ ¶

``@4.0.0-4.7.0``\ ¶

``.``\ ¶

``@STD``\ ¶

``@{orange,orange.A}``\ ¶

``@6.0.0-6.5.0``\ ¶

``.``\ ¶

``@STD``\ ¶

``@{orange,orange.N:s}``\ ¶

``@6.0.0-6.5.0``\ ¶

``.``\ ¶

``@STD``\ ¶

``@{orange juice,orange juice.N+XN+z1:s}``\ ¶

``@6.0.0-8.4.0``\ ¶

``.``\ ¶

``@STD``\ ¶

``@{juice,juice.N+Conc:s}``\ ¶

``@8.0.0-8.4.0``\ ¶

``.``\ ¶

``@STD``\ ¶

``@{juice,juice.V:W:P1s:P2s:P1p:P2p:P3p}``\ ¶

``@8.0.0-8.4.0``\ ¶

``.``\ ¶

``@STD``\ ¶

``@.``\ ¶

``@9.0.0-9.0.0``\ ¶

``.``\ ¶

``f``\ ¶

Fichier text.tind
~~~~~~~~~~~~~~~~~

``text.tind``
文件用来当你想加载一个给定的句子时，跳转到\ ``text.tfst``\ 文件的正确偏移量。这是一个二进制文件包含\ :math:`4
\times N`
字节，\ :math:`N`\ 是句子的数量。它给每个句子起始偏移量小于little-endian的四个字节。

Fichier cursentence.grf
~~~~~~~~~~~~~~~~~~~~~~~

``cursentence.grf``\ 文件是显示一个句子时自动时。由Unitex管理。
``Fst2Grf``\ 程序建立一个\ ``.grf``\ 文件表示从\ ``text.fst2``\ 文件开始的句子自动机。

注意：框的出口用来标记偏移量，在\ ``.tfst``\ 中定义。偏移量由空格分开。这里是几行表示\ *Ivanhoe*\ 的第一句话的语句。

``"Ivanhoe/0 0 0 0 6 0" 100 200 2 3 4 ``\ ¶

``"{by,by.PART}/2 0 0 2 1 0" 220 150 2 5 6 ``\ ¶

``"{by,by.PREP}/2 0 0 2 1 0" 220 50 2 5 6 ``\ ¶

``"{Sir,sir.N+Hum:s}/4 0 0 4 2 0" 310 200 1 7``\ ¶

句子文件.grf
~~~~~~~~~~~~

当用户修改了句子自动机，这个自动机就会保存为\ ``sentenceN.grf``\ ，
``N``\ 表示句子号码。

一个这样的图形在图形框里包含偏移量（见 [section-cursentence\_grf]）

Fichier cursentence.txt
~~~~~~~~~~~~~~~~~~~~~~~

当提取句子自动机时，句子文本保存在名为\ ``cursentence.txt``\ 的文件中。这个文件被Unitex使用来在自动机上显示句子文本。这个文件包含句子文本，其次是一个换行符。

The cursentence.tok file
~~~~~~~~~~~~~~~~~~~~~~~~

当提取句子自动机时，组成句子的令牌号码保存在\ ``cursentence.tok``\ 文件中。这个文件每个令牌包含一行语句，每个语句包含两个整形\ ``x y``\ ；\ ``x``\ 是令牌的号码，\ ``y``\ 是字符长度。

这里是\ *Ivanhoe*\ 的第一句内容。 ``0 7``\ ¶\ ``         ``\ *Ivanhoe*

``1 1``\ ¶\ ``         ``\ ``‘ ``

``2 2``\ ¶\ ``         ``\ *by*

``1 1``\ ¶\ ``         ``\ ``‘ ``

``3 3``\ ¶\ ``         ``\ *Sir*

``1 1``\ ¶\ ``         ``\ ``‘ ``

``4 6``\ ¶\ ``         ``\ *Walter*

``1 1``\ ¶\ ``         ``\ ``‘ ``

``5 5``\ ¶\ ``         ``\ *Scott*

``1 1``\ ¶\ ``         ``\ ``‘ ``

Fichiers tfst\_tags\_by\_freq.txt et tfst\_tags\_by\_alph.txt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

这些文件包含所有出现在由频率和字母排序的文本自动机中的令牌。

Concordances
------------

Fichier concord.ind
~~~~~~~~~~~~~~~~~~~

``concord.ind``\ 文件是在应用一个语法的时候由\ ``Locate``\ 或\ ``LocateTfst``\ 找到的指数索引。这是一个文本文件包含每一个事件的初始位置和结束位置，如果考虑到可能的语法转换已经被匹配时，用字符串任选。这里是文件的例子：

``#M``\ ¶

``59.0.0 63.3.0 the[ADJ= greater] part``\ ¶

``67.0.0 71.4.0 the beautiful hills``\ ¶

``87.0.0 91.3.0 the pleasant town``\ ¶

``123.0.0 127.4.0 the noble seats``\ ¶

``157.0.0 161.5.0 the fabulous Dragon``\ ¶

``189.0.0 193.3.0 the Civil Wars``\ ¶

``455.0.0 459.11.0 the feeble interference``\ ¶

``463.0.0 467.6.0 the English Council``\ ¶

``566.0.0 570.10.0 the national convulsions``\ ¶

``590.0.0 594.5.0 the inferior gentry``\ ¶

``626.0.0 630.11.0 the English constitution``\ ¶

``696.0.0 700.4.0 the petty kings``\ ¶

``813.0.0 817.5.0 the certain hazard``\ ¶

``896.0.0 900.5.0 the great Barons``\ ¶

``938.0.0 942.3.0 the very edge``\ ¶

第一行表示模式转导一致性计算。 可能的三个值是:

-  ``#I`` : 这些转换被忽视;

-  ``#M`` : 转换被列入可识别的序列 ( MERGE模式);

-  ``#R`` : 转换已经取代了可识别的序列 ( REPLACE 模式).

每个事件由一个语句描述。这些语句从事件开始或结束的位置开始。这些位置对应于标签文件\ ``.tfst``\ 中定义的偏移量(见
[section-tfst-format])。 如果文件中包含标题语句
``#I``\ ，每个事件的的结束位置后面紧跟着一个换行符。否则，它后跟一个空格和一个字符串。在REPLACE模式中，这个字符串对应公认的序列产生的转换。在MERGE模式中，它代表其中插入转换的识别序列。在MERGE模式或REPLACE模式中，相应的显示字符串。如果转换被忽视了，事件的内容是由文本文件处理的。

Fichier concord.txt
~~~~~~~~~~~~~~~~~~~

``concord.txt``\ 文件是表示索引的文本文件。每个事件由包括由制表符分隔的三个字符串行编码，并表示左背景，事件（可能通过转换修改），和右背景。

Fichier concord.html
~~~~~~~~~~~~~~~~~~~~

``concord.html`` 文件是 ``HTML``\ 文件表示一种对应关系。这个文件由
UTF-8编码。

页面的标题是事件的号码。这些对应的语句是被看作是超链接的事件语句编码的，与每个链接相关的参考都是形式 ：

``<a href="X Y Z">``

``X`` 和\ ``Y``
表示\ ``name_of_text.snt``\ 文件里用字符表示的事件开头和结尾的位置。\ ``Z``\ 表示出现在这个事件里的数字。

所有空间被类似于(\ ``&nbsp;`` in
HTML)编码，这可以保持对事件的，即使其中之一，位于文件开始时，已经完成了与空格的左侧上下文。

注意：在用glossanet参数建立的索引中，HTML文件获得相同的结构，除了相关链接。在这些冲突中，事件是返回到GlossaNet应用的服务器上的实际链接。对于GlossaNet上的大部分信息，在Unitex的网站上检查链接(http://www-igm.univ-mlv.fr/ unitex)。

这里是文件的例子:

``<html lang=en>``\ ¶

``<head>``\ ¶

````\ ¶

``   <meta http-equiv="Content-Type" content="text/html;``

``         charset=UTF-8">``\ ¶

``   <title>6 matches</title>``\ ¶

``</head>``\ ¶

``<body>``\ ¶

``<table border="0" cellpadding="0" width="100%" ``

``       style="font-family: 'Arial Unicode MS'; font-size: 12">``\ ¶

``<font face="Courier new" size=3>``\ ¶

``on, there <a href="116 124 2">extended</a>&nbsp;i&nbsp;<br>``\ ¶

``&nbsp;extended <a href="125 127 2">in</a>&nbsp;ancient&nbsp;<br>``\ ¶

``&nbsp;Scott {S}<a href="32 34 2">IN</a>&nbsp;THAT PL&nbsp;<br>``\ ¶

``STRICT of <a href="61 66 2">merry</a>&nbsp;Engl&nbsp;<br>``\ ¶

``S}IN THAT <a href="40 48 2">PLEASANT</a>&nbsp;D&nbsp;<br>``\ ¶

``&nbsp;which is <a href="84 91 2">watered</a>&nbsp;by&nbsp;<br>``\ ¶

``</font>``\ ¶

``</td></table></body>``\ ¶

``</html>``\ ¶

图 [fig-example-concordance-2]对应下面文件的页面。

.. figure:: resources/img/fig10-2.png
   :alt: 一致性的例子 [fig-example-concordance-2]
   :width: 5.00000cm

   一致性的例子 [fig-example-concordance-2]

Fichier diff.html
~~~~~~~~~~~~~~~~~

``diff.html``\ 文件是
``HTML``\ 页面表示两个词汇索引的不同。这个文件由UTF-8编码。这里是一个文件例子(换行已被引入布局)

::

    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html;
    charset=UTF-8">
    <style type="text/css">
    a.blue {color:blue; text-decoration:underline;}
    a.red {color:red; text-decoration:underline;}
    a.green {color:green; text-decoration:underline;}
    </style>
    </head>
    <body>
    <h4>
    <font color="blue">Blue:</font> identical sequences<br>
    <font color="red">Red:</font> similar but different sequences<br>
    <font color="green">Green:</font> sequences that occur in only
    one of the two concordances<br>
    <table border="1" cellpadding="0" style="font-family: Courier new;
    font-size: 12">
    <tr><td width="450"><font color="blue">ed in ancient times
    <u>a large forest</u>, covering the greater par</font></td>
    <td width="450"><font color="blue">ed in ancient times
    <u>a largeforest</u>, covering the greater par</font></td>
    </tr>
    <tr><td width="450"><font color="green">ge forest, covering
    <u>the greater part</u>&nbsp;of the beautiful hills </font>
    </td>
    <td width="450"><font color="green"></font></td>
    </tr>
    </table>
    </body>
    </html>

文本字典
--------

``Dico``\ 程序产生多个代表字典的文件。

dlf et dlc
~~~~~~~~~~

``dlf`` et ``dlc`` 是单词字典包含DELAF格式 (见 [section-DELAF-format])。

err
~~~

该文件逐行包含生词。

tags\_err
~~~~~~~~~

这个文件逐行包含生词。与\ ``err``\ 文件的区别是，其中\ ``tags.ind``\ 文件中已知的词不出现。

tags.ind
~~~~~~~~

[section-tags-ind]
和\ ``concord.ind``\ 有着相同格式的文件获得MERGE或REPLACE模式但是它的开头是\ ``#T``\ 。需要注意的是不以斜杠开始输出。

词典
----

通过
``Compress``\ 程序压缩的DELAF词典产生两个文件：\ ``.bin``\ 文件表示词典文件形式的最小自动机，\ ``.inf``\ 文件包含压缩格式，从这个格式开始重新建立词典语句。本节介绍了这两种类型的文件格式。如
``CHECK_DIC.TXT``\ 文件的格式包含字典的验证结果。

Fichier .bin
~~~~~~~~~~~~

``.bin``
文件是表示自动机的二进制文件。文件的头四个字节代表整数表示文件字节大小。自动机的状态由如下代码表示。

-  头两个字节表示状态是否是结束状态，和转换次数。如果状态为结束，最高位为0，否则为1.其他15位是转换次数的代码。

   比如：有着17个转换的非结束状态由8011十六进制序列表示。

-  如果状态为结束，后三个字节编码压缩文件
   ``.inf``\ 中的索引用来重建这个文件格式的词典语句。

   例子：如果状态返回到索引25133的压缩形式，
   对应的十六进制就是\ ``00622D``\ 。

-  每个转换输出后由5个字节编码。前两个字节表示该标记字符转换，之后的三个字节表示\ ``.bin``\ 文件到达状态的位置。这些状态的转换依次编码。

   例子：被指向第\ :math:`50106`\ 个目标的A所标记的转换，字节将由十六进制序列来表示。

按照惯例，第一个状态就是初始状态。

Fichier.inf
~~~~~~~~~~~

``.inf``\ 文件是描述与\ ``.bin``\ 文件相关联的压缩格式的文档文件。这里是
``.inf`` file文件的例子：

``0000000006``\ ¶

``_10\0\0\7.N``\ ¶

``.PREP``\ ¶

``_3.PREP``\ ¶

``.PREP,_3.PREP``\ ¶

``1-1.N+Hum:mp``\ ¶

``3er 1.N+AN+Hum:fs``\ ¶

文件的第一行表示所包含的压缩文件的号码。
每一行都能包含一个或多个压缩格式。如果有多个格式，要用逗号将它们隔开。每一个压缩格式由一个能从弯曲格式找到的正常的格式的序列组成，接着是与词形变化码，相关联语法，语义的序列。

正常格式的压缩模式根据词尾变化形式的功能不同而不同。如果这两个形式完全一样，压缩的形式就会概括成为语法信息，语义信息和词形变化信息，如下列情况：

``.N+Hum:ms``

如果这些形式不同，压缩程序切入两种单位形式。这些单位可以是一个空间或一个连字符，或不包含空格或破折号字符序列。这种分割模式可以有效地考虑复合词的词形变化形式。

如果词尾变化形式和标准形式不包含相同的数字单元，该程序代码规范的形式由字符数从词尾变化的形式相减，因此，上述文件的第一行是字典行：

``James Bond,007.N``

``James Bond``\ 序列包含三个单元而\ ``007``\ 只有一个，正常形式由\ ``_10\0\0\7``\ 编码。\ ``_``\ 符号表示两种形式不具有相同数量的单元。后面的数字
(这里是
10)表示要减去的字符数。跟在后面的\ ``\0\0\7``\ 序列表示我们应该加上\ ``\0\0\7``\ 序列。数字在字符\ ``\``\ 前面为了不与要减去的字符数相混淆。

当两个形状具有相同数量的单元，这些单元是成对压缩。如果这两个单元构成的空间或连字符的，该单元的压缩形式是单元本身，如以下情况：

``0-1.N:p``

是 ``battle-axes,battle-axe.N:p``\ 的出口

当词典包含复合词时，这可以保存\ ``.inf``\ 文件中特定的变量。

当单元中的至少一个不是空格或连字符时，压缩形式组成的字符数的减去跟随字符添加的序列。
因此词典里的序列：

``première partie,premier parti.N+AN+Hum:fs``

被该语句编码 :

``3er 1.N+AN+Hum:fs``

``3er``\ 码表示我们应该在\ ``première``\ 的序列中减去三个字符并加上\ ``er``
字符来获得\ ``premier``\ 。\ ``1``\ 表示我们应该在\ ``partie``\ 中只删除一个字符来获得\ ``parti``\ 序列。\ ``0``\ 数字用来表示我们不想删除任何字符。

词典的文件信息
~~~~~~~~~~~~~~

在“Apply lexical
resources”框架里，右击鼠标可以获得词典信息。这些词典信息因为名为\ ``biniou.txt``\ 的纯文本而与\ ``biniou.bin``\ 或\ ``biniou.fst2``\ 相关，它们在同一个目录里。

Fichier CHECK\_DIC.TXT
~~~~~~~~~~~~~~~~~~~~~~

该文件由\ ``CheckDic``\ 词典的确认程序产生。
这是一个文本文件，它提供所分析的字典的信息，被分成四个部分。

第一部分给出的列表中，可能是空的，所有在字典中找到的语法错误：没有词尾变化的形式或规范的形式，缺少语法代码，空行等。由受影响的语句的数量，描述错误的性质的消息，该行的内容中描述的每个错误。这里是一个信息的例子：

::

    第 12451行: 语句意外结束
    garden,N:s

第二和第三部分分别给出语法、语义、词形变化的代码清单。为了避免编码错误，该程序报告包含空格代码、标签或非ASCII字符。而且如果一个希腊语词典包含\ ``ADV``\ 代码，\ ``A``\ 符号和
``A``\ 希腊语代替了拉丁语\ ``A``\ ，该程序警告如下：

::

    ADV warning: 1 suspect char (1 non ASCII char): (0391 D V)

非ASCII字符以他们的十六进制数表示。在上面的例子中 ``0391``
代码表示希腊字符 ``A`` 。\ ``SPACE``\ 序列表示空格。

::

    Km s warning: 1 suspect char (1 space): (K m SPACE s)

当检查一下词典时：

::

    1,2 et 3!,.INTJ 
    abracadabra,INTJ 
    supercalifragilisticexpialidocious,.INTJ
    damned,. INTJ
    Paul,.N+Hum+Hum
    eat,.V:W:P1s:Ps:P1p:P2p:P3p

我们可以得到 ``CHECK_DIC.TXT`` 文件，如下 :

``Line 1: unprotected comma in lemma``\ ¶

``1,2 et 3!,.INTJ ``\ ¶

``Line 2: unexpected end of line``\ ¶

``abracadabra,INTJ ``\ ¶

``Line 5: duplicate semantic code``\ ¶

``Paul,.N+Hum+Hum``\ ¶

``Line 6: an inflectional code is a subset of another``\ ¶

``eat,.V:W:P1s:Ps:P1p:P2p:P3p``\ ¶

``-----------------------------------``\ ¶

``-------------  Stats  -------------``\ ¶

``-----------------------------------``\ ¶

``File: D:\My Unitex\English\Dela\axe.dic``\ ¶

``Type: DELAF``\ ¶

``6 lines read``\ ¶

``2 simple entries for 2 distinct lemmas``\ ¶

``0 compound entry for 0 distinct lemma``\ ¶

``-----------------------------------``\ ¶

``----  All chars used in forms  ----``\ ¶

``-----------------------------------``\ ¶

``a (0061)``\ ¶

``c (0063)``\ ¶

``d (0064)``\ ¶

``e (0065)``\ ¶

``f (0066)``\ ¶

``g (0067)``\ ¶

``i (0069)``\ ¶

``l (006C)``\ ¶

``m (006D)``\ ¶

``n (006E)``\ ¶

``o (006F)``\ ¶

``p (0070)``\ ¶

``r (0072)``\ ¶

``s (0073)``\ ¶

``t (0074)``\ ¶

``u (0075)``\ ¶

``x (0078)``\ ¶

``-------------------------------------------------------------``\ ¶

``----    2 grammatical/semantic codes used in dictionary  ----``\ ¶

``-------------------------------------------------------------``\ ¶

``INTJ``\ ¶

`` INTJ warning: 1 suspect char (1 space): (SPACE I N T J)``\ ¶

``-----------------------------------------------------``\ ¶

``----    0 inflectional code used in dictionary  -----``\ ¶

``-----------------------------------------------------``\ ¶

``eat``\ 的词形变化码没有被报告，因为在此行中发生错误。

Fichiers ELAG
-------------

Fichier tagset.de
~~~~~~~~~~~~~~~~~

见 [section-elag-tagset], 页面 .

Fichiers .lst
~~~~~~~~~~~~~

LES FICHIERS .LST NE SONT PAS CODÉS EN UNICODE.

``.lst``\ 文件包含一个文件名列表\ ``.grf``\ 。如果文件名不确定，就与\ ``elag.lst``\ 文件的位置相对。这里是\ ``elag.lst``\ 文件的法文版：

``PPVs/PpvIL.grf``\ ¶

``PPVs/PpvLE.grf``\ ¶

``PPVs/PpvLUI.grf``\ ¶

``PPVs/PpvPR.grf``\ ¶

``PPVs/PpvSeq.grf``\ ¶

``PPVs/SE.grf``\ ¶

``PPVs/postpos.grf``\ ¶

.elg files
~~~~~~~~~~

``.elg`` 文件包含编译的ELAG规则。这些文件都是 ``.fst2``\ 格式。

Fichier .rul
~~~~~~~~~~~~

RUL文件不是用Unicode编码的。

。 ``.rul``\ 文件和\ ``.elg``\ 文件由同样多的部分组成。每一个部分由和
``.elg``\ 文件对应的ELAG语法列表组成。\ ``.elg``\ 文件名为英文。由表格开始的语句都为批注而且被\ ``Elag``\ 程序忽略。这里是\ ``elag.rul``\ 文件默认为法语：

``    PPVs/PpvIL.elg``\ ¶

``    PPVs/PpvLE.elg``\ ¶

``    PPVs/PpvLUI.elg``\ ¶

``<elag.rul-0.elg>``\ ¶

``    PPVs/PpvPR.elg``\ ¶

``    PPVs/PpvSeq.elg``\ ¶

``    PPVs/SE.elg``\ ¶

``    PPVs/postpos.elg``\ ¶

``<elag.rul-1.elg>``\ ¶

Fichier taggeur
---------------

本节介绍了TrainingTagger标注器和程序使用的产品和文件。

Fichier corpus.txt
~~~~~~~~~~~~~~~~~~

[section-corpus-file] 该文件所使用的
TrainingTagger程序来计算Tagger程序的统计信息。它包含在其中的每个字在一个单独的语句示出的短语。
每一行语句表示一个单词是由另一个单词或复合词构造的，后面试斜杠和单词的标签。
这个标签是由语法代码组成，每次后接\ ``'+'``\ 和语法和语义代码。词形变化码是在\ ``':'``\ 之后。如果单词是复合词，里面包含的单词就会用\ ``'_'``\ 隔开。这里是一个例子：

``The/DET+Ddef:s``\ ¶

``GATT/N:s``\ ¶

``had/V:I3s``\ ¶

``formerly/ADV``\ ¶

``a/DET+Dind:s``\ ¶

``political/A``\ ¶

``assessment/N:s``\ ¶

``of/PREP``\ ¶

``the/DET+Ddef:s``\ ¶

``behavior/N:s``\ ¶

``of/PREP``\ ¶

``foreign_countries/N:p``\ ¶

``./PONCT``\ ¶

¶

``She/PRO+Nomin:3fs``\ ¶

``closed/V:I3s``\ ¶

``easily/ADV``\ ¶

``her/DET+Poss3fs:p``\ ¶

``eyes/N:p``\ ¶

``when/CONJ``\ ¶

``some/DET+Dadj:p``\ ¶

``infractions/N:p``\ ¶

``might/V:I3p``\ ¶

``appear/V:W``\ ¶

``justified/V:K``\ ¶

``against/PREP``\ ¶

``higher/A``\ ¶

``interests/N:p``\ ¶

``./PONCT``\ ¶

¶

注意：这些句子应该用空行分割。

``.txt``\ 格式同样可以被运用（见[section-texts]）。文本的每一个字必须用一个有效的词汇标签来表示(\ ``{aujourd'hui,.ADV}``)，并且每句话应由\ ``{S}``\ 分隔。这里是
``.txt``\ 格式：

| ``{The,.DET+Ddef:s}`` ``{GATT,.N:s}`` ``{had,.V:I3s}``
  ``{formerly,.ADV}``
| ``{a,.DET+Dind:s}`` ``{political,.A}`` ``{assessment,.N:s}``
  ``{of,.PREP}``
| ``{the,.DET+Ddef:s}`` ``{behavior,.N:s}`` ``{of,.PREP}``
  ``{foreign countries,.N:p}``
| ``{.,.PONCT}`` ``{S}`` ``{She,.PRO+Nomin:3fs}`` ``{closed,.V:I3s}``
  ``{easily,.ADV}``
| ``{her,.DET+Poss3fs:p}`` ``{eyes,.N:p}`` ``{when,.CONJ}``
  ``{some,.DET+Dadj:p}``
| ``{infraction,.N:p}`` ``{might,.V:I3p}`` ``{appear,.V:W}``
  ``{justified,.V:K}``
| ``{against,.PREP}`` ``{higher,.A}`` ``{interests,.N:p}``
  ``{.,.PONCT}`` ``{S}``

Le fichier de données du taggueur
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

[section-training-dict]
TrainingTagger程序管理两个由Tagger使用用来计算二阶 Markov模型数据文件
(默认)。这些文件包含单字母，双字母组合三个字母组来处理corpus.txt标签。元组是由任一的2或3个标签序列组成的（为了计算转移概率）或是在0或1的标签之前的一个语句（计算发射的概率）。在一个元组的单位，必须由制表分开。这些元组由序列定界符监视“。”然后由一个整数，表示该元组在语料库中出现的次数。

文件名以“cat”或“morph”为后缀。首先，元组由代码标记语法，句法和语义。其次，由元组组成的代码标记语法，句法和语义每次后接\ ``':'``\ 和词形变化码。
这里是有着“cat”类型的标签的数据文件例子：

``the,.9630``\ ¶

``those,.236``\ ¶

``eyes,.32``\ ¶

``DET+Ddef   the,.9630``\ ¶

``DET+Ddem   those,.140``\ ¶

``PRO+Pdem   those,.96``\ ¶

``N        eyes,.32``\ ¶

``DET    N,.62541``\ ¶

``PREP  DET  N,.25837``\ ¶

¶

这里是有着“morph”类型的标签的数据文件例子：

``the,.9630``\ ¶

``those,.236``\ ¶

``eyes,.32``\ ¶

``DET+Ddef:s     the,.4437``\ ¶

``DET+Ddef:p     the,.5193``\ ¶

``DET+Ddem:p     those,.140``\ ¶

``PRO+Pdem:p     those,.96``\ ¶

``N:p          eyes,.32``\ ¶

``DET:s  N:s,.18489``\ ¶

``PREP    DET:s  N:s,.6977``\ ¶

¶

如果文件包含“cat”或“morph”标签，就需要具体的语句加入到数据文件进行确认。
这一行包含\ ``CODE FEATURES``\ ，后面是代表“cat”的0，或代表“morph”的1

注意：在最后一步， TrainingTagger压缩两个数据文件到\ ``.bin``\ 格式。

配置文件
--------

Fichier Config
~~~~~~~~~~~~~~

当用户为特定的语言修改配置时，这些保存在可以在当前语言目录中找到、名为\ ``Config``\ 的文档文件中。这个文件的语法如下（该行的顺序可能会有所不同）：

``#Unitex configuration file of 'paumier' for 'English'``\ ¶

``#Fri Oct 10 15:18:06 CEST 2008``\ ¶

``TEXT\ FONT\ NAME=Courier New``\ ¶

``TEXT\ FONT\ STYLE=0``\ ¶

``TEXT\ FONT\ SIZE=10``\ ¶

``CONCORDANCE\ FONT\ NAME=Courier new``\ ¶

``CONCORDANCE\ FONT\ HTML\ SIZE=12``\ ¶

``INPUT\ FONT\ NAME=Times New Roman``\ ¶

``INPUT\ FONT\ STYLE=0``\ ¶

``INPUT\ FONT\ SIZE=10``\ ¶

``OUTPUT\ FONT\ NAME=Arial Unicode MS``\ ¶

``OUTPUT\ FONT\ STYLE=1``\ ¶

``OUTPUT\ FONT\ SIZE=12``\ ¶

``DATE=true``\ ¶

``FILE\ NAME=true``\ ¶

``PATH\ NAME=false``\ ¶

``FRAME=true``\ ¶

``RIGHT\ TO\ LEFT=false``\ ¶

``BACKGROUND\ COLOR=-1``\ ¶

``FOREGROUND\ COLOR=-16777216``\ ¶

``AUXILIARY\ NODES\ COLOR=-3289651``\ ¶

``COMMENT\ NODES\ COLOR=-65536``\ ¶

``SELECTED\ NODES\ COLOR=-16776961``\ ¶

``PACKAGE\ NODES\ COLOR=-2302976``\ ¶

``CONTEXT\ NODES\ COLOR=-16711936``\ ¶

``CHAR\ BY\ CHAR=false``\ ¶

``ANTIALIASING=false``\ ¶

``HTML\ VIEWER=``\ ¶

``MAX\ TEXT\ FILE\ SIZE=2097152``\ ¶

``ICON\ BAR\ POSITION=West``\ ¶

``PACKAGE\ PATH=D\:\\repository``\ ¶

``MORPHOLOGICAL\ DICTIONARY=D\:\\MyUnitex\\English\\Dela\\zz.bin``\ ¶

``MORPHOLOGICAL\ NODES\ COLOR=-3911728``\ ¶

``MORPHOLOGICAL\ USE\ OF\ SPACE=false``\ ¶

前两行是注释行。接下来的三行显示用于显示文本的名称，样式和字体大小，词典，词汇单元，文本自动机的句子等。

``CONCORDANCE FONT NAME``\ 和 ``CONCORDANCE FONT HTML SIZE``
定义名称并用于显示HTML匹配的字体大小。字体大小必须在1和7之间。

参数\ ``INPUT FONT ...``\ 和\ ``OUTPUT FONT ...``
定义用于显示路径和传导图字体的名称，样式和尺寸。

以下10个参数对应于标头图表提议的参数。 [tab-parameters]表描述对应关系。

+---------------------------------------------+--------------+
| ``Config``\ 文件配置和 ``.grf``\ 文件配置   |              |
+=============================================+==============+
| ``DATE``                                    | ``DDATE``    |
+---------------------------------------------+--------------+
| ``FILE NAME``                               | ``DFILE``    |
+---------------------------------------------+--------------+
| ``PATH NAME``                               | ``DDIR``     |
+---------------------------------------------+--------------+
| ``FRAME``                                   | ``DFRAME``   |
+---------------------------------------------+--------------+
| ``RIGHT TO LEFT``                           | ``DRIG``     |
+---------------------------------------------+--------------+
| ``BACKGROUND COLOR``                        | ``BCOLOR``   |
+---------------------------------------------+--------------+
| ``FOREGROUND COLOR``                        | ``FCOLOR``   |
+---------------------------------------------+--------------+
| ``AUXILIARY NODES COLOR``                   | ``ACOLOR``   |
+---------------------------------------------+--------------+
| ``COMMENT NODES COLOR``                     | ``SCOLOR``   |
+---------------------------------------------+--------------+
| ``SELECTED NODES COLOR``                    | ``CCOLOR``   |
+---------------------------------------------+--------------+

Table: 参数说明[tab-parameters]

``PACKAGE NODES``\ 配置表示目录里子图的调用颜色。

``CONTEXT NODES`` 配置表示对应于上下文的开始或结束的框的颜色。

``CONTEXT NODES``\ 配置表示当前语言是否应被视为字符。

``ANTIALIASING``
配置指定图形和句子自动机是否要在默认情况下使用平滑处理的效果显示。

``HTML VIEWER``\ 配置表示要用来查看匹配的浏览器的名称。如果没有指定浏览器的名称，词汇索引将在Unitex窗口显示。

``MAX TEXT FILE SIZE``\ 配置不再被使用。

``ICON BAR POSITION``\ 配置定义在图形窗口中的图标条的位置。

``PACKAGE PATH``\ 配置定义用于该语言的目录。

``MORPHOLOGICAL DICTIONARY``\ 配置列出了字典形态模式，用分号隔开。

``MORPHOLOGICAL NODES COLOR``\ 配置形态模式\ ``$<`` et
``$>``\ 标签的颜色。

``MORPHOLOGICAL USE OF SPACE``\ 配置表示\ ``Locate``\ 程序是否能通过识别领域开始。（默认不是）。

Fichier system\_dic.def
~~~~~~~~~~~~~~~~~~~~~~~

``system_dic.def``\ 文件是描述系统字典列表，默认将应用于文本文件。该文件位于当前的语言的目录。每一个语句对应\ ``.bin``\ 文件的名字。该系统的词典必须在Unitex系统目录，在子目录内。
这里是文件的范例 ：

``delacf.bin``\ ¶

``delaf.bin``\ ¶

Fichier user\_dic.def
~~~~~~~~~~~~~~~~~~~~~

``user_dic.def``\ 文件是描述用户默认情况下应用于词典列表的文本文件。该文件是在当前的语言的目录，并具有相同的格式文件。用户词典必须在个人工作目录的子目录\ ``(langue courante)/Dela``\ 里。

文件 (用户姓名).cfg et .unitex.cfg
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

在Linux和Mac OS，Unitex认为工作人员的工作目录被命名为 ``unitex``
并且位于用户根目录中
(``$HOME``\ :math:`)。如果要更改此默认位置,\verb+.unitex.cfg+文件在根目录中创建，它包含到工作目录Unitexd的路径。这个文件是UTF8文件。如果\verb+.unitex.cfg+Linux并不包含对现有目录的有效路径，则会被忽视\,\footnote{可以在Linux，Window上运行Unitex，共享文件~：通向Unitex个人工作目录的Windows路径在\texttt中指出{.unitex.cfg}，而在Linux中运行时，Unitex会忽视}，

\bigskip
在Windows,它并不是总是可以默认与用户相连的目录。为了解决这个问题，Unitex为每个用户创建 \verb+.cfg+文件，包含包含工作目录的路径。该文件在Unitex系统目录的字目录\verb+Users+下保存为\verb+(用户名).cfg+，\index{Répertoire!système Unitex}如果用户没有权限写入该目录，\verb+.unitex.cfg+文件被并保存在用户配置备份文件目录中~，

\begin{itemize}
\item 在 \verb+文件和设置\(user login)+ 在Windows XP上
\item 在 \verb+Users\(user login)+ 在Windows Vista或更高版本。
\end{itemize}

\bigskip
\noindent
注意~：本文件并不以Unicode的方式保存工作人员的工作。\index{Répertoire!个人工作}
后面没有语句。

\section{ CasSys 文件}

\subsection{配置文件 CasSys csc}
为了存储CasSys级联转换器列表，我们使用一个文本文件（CSV），其中每一语句包含转换器监测输出模式路径（合并/替换）应用到换能器。
csc文件的语句格式是： Name\_and\_path\_of\_transducer 合并
级联CSC文件的例子：


\ttfamily
"C:`\\\ :math:`apps`\\\ :math:`my\_unitex`\\\ :math:`French`\\\ :math:`Graphs`\\\ :math:`grf1.fst2" Merge

"C:`\\\ :math:`apps`\\\ :math:`my\_unitex`\\\ :math:`French`\\\ :math:`Graphs`\\\ :math:`grf2.fst2" Replace
\rmfamily

\section{其他文件}

对于每个文本，Unitex创建在GUI包含要显示的信息的多个文件。本节介绍了这些文件。

\subsection{Fichier dlf.n, dlc.n, err.n et tags\_err.n}
\index{Fichier!\verb+dlf.n+}\index{Fichier!\verb+dlc.n+}\index{Fichier!\verb+err.n+}\index{Fichier!\verb+tags_err.n+}
\index{Fichier!\verb+dlf+}\index{Fichier!\verb+dlc+}\index{Fichier!\verb+err+}\index{Fichier!\verb+tags_err+}
这三个文件是文本目录中的文本文件。它们分别包含\verb+dlf+, \verb+dlc+, \verb+err+ 和\verb+tags_err+文件的语句数量。这些数字后面跟着一个换行符。

\subsection{Fichier stat\_dic.n}
\index{Fichier!\verb+stat_dic.n+}
该文件是在文本目录中的文本文件。它包含三个语句，包括\verb+dlf+, \verb+dlc+ 和 \verb+err+文件的语句数。

\subsection{Fichier stats.n}
\index{Fichier!\verb+stats.n+}
该文本文件是在文本目录并包含以下语句：


\bigskip
\verb`\ 3949 sentence delimiters, 169394 (9428 diff) tokens, 73788
(9399):math:`

\verb`\ simple forms, 438 (10) digits\ :math:`\P

\bigskip
\noindent
所指的数字解释以下方法：


\begin{itemize}
  \item \verb+sentence delimiters+:句子分隔符的数量
  (\verb+{S}+);\index{\verb+{S}+}
  \index{Séparateur!de phrases}

  \item \verb+tokens+: 
  
  
  令牌文本的总数。 之前的数字\verb+diff+表示不同单元的数量;  

  \item \verb+simple forms+: 
  由字母组成的词汇单元文本总数。括号中的数字表示其中由字母不同词汇单元的数目；
  
  \item \verb+digits+: 
文本中的总数。括号中的数字表示显示的数字（最多10个）。

\end{itemize}


\subsection{Fichier concord.n}
\index{Fichier!\verb+concord.n+}
\verb+concord.n+文件是文本文件，在文本目录。它包含这个文本模式进行的最新的研究资料，情况如下：

\bigskip
\verb`\ 6 matches\ :math:`\P

\verb`\ 6 recognized units\ :math:`\P

\verb`\ (0.004
第一行给出了发现出现的次数，由这些出现覆盖单元的第二个数字。第三行表示的的覆盖单元的数目和文字单元的总数之间的比率。

Fichier concord\_tfst.n
~~~~~~~~~~~~~~~~~~~~~~~

``concord_tfst.n``\ 文件是在文本目录中的文本文件。它包含对文本自动机的最新研究信息，如下所示：

``23 matches(45 outputs)``\ ¶

文件规范化规则
~~~~~~~~~~~~~~

[section-normalization-file]
该文件由\ ``Normalization``\ 程序和\ ``XMLizer``\ 程序使用。它代表了规范化规则。每一行代表一个规则。根据以下格式(\ :math:`\longmapsto`\ 代表制表符)

``input sequence`` :math:`\longmapsto` ``output sequence``

如果您想使用的选项卡或换行，你必须用一个反斜杠，像这样：

``123\``

:math:`\longmapsto` ``ONE_TWO_THREE_NEW_LINE``

被禁止的单词文件
~~~~~~~~~~~~~~~~

[section-forbidden-words]
``PolyLex``\ 程序该计划需要为荷兰和挪威语的禁词。

Le programme ``PolyLex`` requiert un de mots interdits pour le
hollandais et le norvégien.这个纯文本文件应该被称为
``ForbiddenWords.txt`` .
它可以在对应于当前语言的\ ``Dela``\ 目录里找到。每一行应该包含一个禁止的单词。

日志文件
~~~~~~~~

[section-log-file]
``UnitexToolLogger``\ 程序，如果\ ``unitex_logging_parameters.txt``\ 文件
被发现有一个路径（要保存日志文件）创建一个文件。运行选择Unitex工具.ulp日志。

它创建\ ``unitex_logging_parameters_count.txt``
文件，仅包含最后创建的日志文件的数目。
日志文件（扩展名为.ulp）是一种未压缩的压缩文件，解压后用兼容并解压缩所有的标准工具。我们可以重新创建InfoZip的ZIP（-X选项-0）。它包含文件：

-  ``test_info/command_line.txt``:
   用于运行工具的命令行参数的列表。有每行的参数。第一行包含返回值，第二行的参数的数量;

-  ``test_info/command_line_synth.txt``:
   单个语句和命令语句的摘要用来执行；

-  ``test_info/list_file_in.txt``: 由工具创建的文件的列表。
   第一列是文件大小，第二个是CRC32，第三个是该文件名;

-  ``test_info/list_file_out.txt``: 由工具创建的文件的列表。
   第一列是文件大小，第二个是CRC32，第三个是该文件名;

-  ``test_info/std_out.txt``: 控制台的标准输出内容;

-  ``test_info/std_err.txt``: 在控制台上的输出内容的错误;

-  ``src/xxx``: 由工具（再次操作日志所需）读取文件的副本;

-  ``dest/xxx``:由工具创建的文件的副本

如果第二行Unitex parameters.txt包含0，这些文件不会被保存;如果此行包含1，他们登记;

阿拉伯语排版规则: arabic\_typo\_rules.txt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

在阿拉伯语中，字典查找可以与描述了某些排版变化的是否允许或不允许的文件进行配置。此文件包含这样的线路：

``fatha omission=YES``

``fatha omission``
是规则的名称。有关所有可用规则的完整说明，请参阅在源程序中的文件
``Arabic.h`` dans les sources du programme.

fichier d’offsets de différence
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

， DumpOffsets([section-DumpOffsets]), Normalize([section-Normalize]),
Fst2Txt([section-Fst2Txt]), Tokenize([section-Tokenize]),
Concord([section-Concord]) 和 GrfTest,
并被Tokenize([section-Tokenize])读取。 这些文本文件由含有4个整数， A B C
D的每一行对应于所述文本的修改，如下列语句所示：

区间[A，B[文字\*\*\*\*\*\*任何处理由范围[C替换之前; D
[处理后，A，B，C和D在文本文件中的字符位置之中。

例如，如果规格化程序被施加到文本“Hello
World”（字之间包含两个空格），会出现这样的语句：

``5 7 5 6``

这意味着两个字符（2个空格）的序列是由一个字符的序列代替。

其原理是，以产生一个新的文件偏移对每个程序应用到修改的文本，以作为输入由前面的程序产生的偏移文件。因此，看着最后一个偏移量产品的文件，我们知道，每行ABCD，区间[C;
D [.snt文件中对应于区间[A，B [在首发.txt文件

抵消了公共区域的文件
~~~~~~~~~~~~~~~~~~~~

偏移文件被DumpOffsets读取，编写。

这些文本文件由含有4个整数 A B C
D的每一行对应于所述文本的修改，如以下语句表示：
区间[A，B[对应区间[C原文; D
[处理后，A，B，C和D在文本文件中的字符位置之中。在每一行，B-A-C = D。

例如，如果规格化程序被施加到文本“Hello
World”（字之间有两个空格），会出现这样的语句： ``0 5 0 5`` ``7 12 6 11``

这意味着0字符（包括）到5（不含税）两个文件包含完全相同的文字，这7（含）到12（不包括）第一个文本包含相同的文本6（含）至11（不含）。

偏移文件UIMA
~~~~~~~~~~~~

UIMA偏移文件由Tokenize编写并由 Concord读取 (利用工具 ``--uima=``,
``--xml-with-header=`` ou ``--xml=``)
这些文件建立每个连续标记和原始文件中的位置之间的对应关系。
这些文本文件是包含三个整数A B C与文本之间<et>语句。

每一行对应表述如下令牌：
令牌数A是对应于原始文件中的C（不含税）的位置B（包含）的文本，和在<et>中提到的的令牌。
令牌数A的数量对应tokens.txt出现的语句数量（加1个tokens.txt标题行（参考标记-TXT文件））

.. |image| image:: resources/img/korean_letters.png
   :height: 0.50000cm
.. |image| image:: resources/img/thai_letter.png
   :height: 0.30000cm
