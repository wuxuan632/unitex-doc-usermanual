文本自动机
==========

通常来说，语言都会有在词汇上的歧义。
文本自动机是一种可以表达出这些歧义的有效且直观的工具。
文本里的每一句话都可以通过文本自动机表达出其可能存在的所有解释。

本章介绍文本自动机的创建细节以及可对其进行应用的操作，尤其是通过ELAG对其进行歧义消除。
自2.1版本之后，可以在文本自动机上实现搜索消除理由。(见 [section-locate-tfst]).

介绍
----

文本自动机可以表达出一个单词所有可能的词汇解释。这些不同的解释就是存在于文本字典里的不同词条。
图 [fig-sentence-automaton] 显示的是文本中第四句的自动处理 *Ivanhoe*.

.. figure:: resources/img/fig7-1.png
   :alt: Exemple d’automate de phrase[fig-sentence-automaton]
   :width: 15.50000cm

   Exemple d’automate de phrase[fig-sentence-automaton]

我们可以从图看出 [fig-sentence-automaton]单词 ``Here`` 在这里有三种解释
(形容词,副词
和名词),\ ``haunted``\ 有两种解释(形容词和动词),等等。所有可能的组合都会被表示出来，因为每一个词的每一个解释都和其上下文有所关联。

如果在一个词组和一个单字序列之间存在竞争，自动机包含一条由词组标记的路径，该路径与单字组合的路径并行。图表 [fig-overlap]就词组
``courts of law`` 和单字组合之间的竞争加以说明。

.. figure:: resources/img/fig7-2.png
   :alt: 词组与单字组合之间的竞争[fig-overlap]
   :width: 12.50000cm

   词组与单字组合之间的竞争[fig-overlap]

通过其构造，文本自动机没有循环。我们称其为非循环文本自动机。
*acyclique*.

注释：“文本自动机”是被大量使用的语言。的确，实际上每一句文本都有一个自动机。然而，所有自动机串联起来才能对应所有文本的自动机。因此，尽管实际上它并不因实际原因操作对象，我们也运用“文本自动机”这个词。

构造
----

为了构造一个文本的自动机，您需要打开该文档，然后在菜单中在“Construire
FST-Text...”选项中点击“Text”
建议该文本应被分解成以句子为单位，并将其运用进字典。如果您没有将其分解成以句子为单位，结构程序将会随意地把该文本分解成由2000个词汇组成的序列而不是通过句子构造成自动机。如果您没有运用字典，那么已得到的句子的自动机I将只会建立一条只包含生词的路径。

构造文本自动机的规则
~~~~~~~~~~~~~~~~~~~~

句子自动机是从文本字典开始构造。文本歧义度和其所运用的字典描述得精确与否有直接关系。
从图 [fig-ambiguity-of-which]中的句子自动机上,我们可以发现单词 ``which``
已经两次在该类的两个子类中被编译为限定词。如果我们只在语法范畴内考虑该单词，那么对该词的精确描述将没有任何必要。因此，我们应调整字典的精确度以便运用到搜索中去。

.. figure:: resources/img/fig7-3.png
   :alt: Double entrée pour ``which`` en tant que
   déterminant[fig-ambiguity-of-which]
   :width: 10.60000cm

   Double entrée pour ``which`` en tant que
   déterminant[fig-ambiguity-of-which]

对于句子里的每一个词汇的组合,Unitex会在文本单字字典里搜索所有可能的解释。接着我们在构成该文本的所有单词的词典里搜索有一种解释的所有词汇组合系列。所有的解释结合在一起形成句子自动机。

注释：当该文本包含词汇标签时(\ *e.g.*
``{aujourd’hui,.ADV}``),这些标签会在自动机里以相同的形态重现，没有程序会尝试分解它们表示出来的序列。

在每一个盒子中，第\ :math:`1\iere`\ 行包括文本中找到的词尾变化形式，如果形式不一样，第\ :math:`2\ieme`\ 行包括规范形式。其他信息在盒子中进行编码。
(见一段截取 [section-displaying-sentence-automata]).

分隔单个词汇的空格不会被转录进自动机中，除了复合词内部的空格。

单个词汇存放的字盒被保留。比如我们找到了单词 ``Here``,
我们保留其大写字母 (见图 [fig-sentence-automaton]).
这样可以避免切换到文本自动机时丢失信息，在重要的字盒里这是非常有用的方法，比如对专有名词的核对。

将歧义形式标准化
~~~~~~~~~~~~~~~~

在创建自动机时，通过运用标准语法化方法可以实现将歧义形式标准化。该语法需要被命名\ ``Norm.fst2``\ ，并存放在您的个人目录中所需语言的子目录里
``/Graphs/Normalization``\ 。
歧义形式的标准语法化在部分 [section-normalizing-text-automataon]作介绍。
如果文本序列经语法标准化认证，所有由该语法描述的解释将会被插入文本自动机。图 [fig-example-tfst-normalization-graph]指出法语中关于解释\ ``l'``\ 的语法使用摘要。

.. figure:: resources/img/fig7-4.png
   :alt: Normalisation de la séquence
   ``l’``\ [fig-example-tfst-normalization-graph]
   :width: 8.60000cm

   Normalisation de la séquence
   ``l’``\ [fig-example-tfst-normalization-graph]

如果我们将这个语法运用到包含\ ``l'``\ 的法语句子中，我们可以获得一个类似于图 [fig-tfst-normalization-results]的句子自动机。

.. figure:: resources/img/fig7-5.png
   :alt: Automate normalisé avec la grammaire de la
   figure [fig-example-tfst-normalization-graph]
   [fig-tfst-normalization-results]
   :width: 10.20000cm

   Automate normalisé avec la grammaire de la
   figure [fig-example-tfst-normalization-graph]
   [fig-tfst-normalization-results]

在得到的自动机中，我们可以看到四个\ ``l'``\ 的重写规则都被运用了，它们在其中被加入了4个标签。
因为有探索法“keep best
paths”的存在，这些标签没有为事先存在的\ ``l’``\ 的两条路径产生竞争(见
[section-keeping-best-paths]).

文本自动机结构的标准化使这些路径被加入进自动机，而且并不将其删除。
如果有些路径被选择删除，探索法“keep best
paths”将会对其部分进行作用。为了更进一步优化，建议您使用ELAG系统的歧义消除功能。

葡萄牙语附着代词标准化
~~~~~~~~~~~~~~~~~~~~~~

在葡萄牙语中，动词的将来时和条件式可以通过在词根与词尾之间插入附着代词来进行变位。比如词序\ *dir-me-ão*
(*ils me
diront*)，与完整的动词形式\ *dirão*\ 相对应，与代词\ *me*\ 相联系。
为了能执行该重写形式的操作，我们必须将其引进与原始序列并行的自动机。这样用户就可以根据其需求搜索一种或多种形式。图 [fig-1285-not-normalized]
和 [fig-1285-normalized] 表示一个句子自动机在附着介词标准化前后的对比。

.. figure:: resources/img/fig7-6.png
   :alt: Automate de phrase non normalisé[fig-1285-not-normalized]
   :width: 11.00000cm

   Automate de phrase non normalisé[fig-1285-not-normalized]

.. figure:: resources/img/fig7-7.png
   :alt: Automate de phrase normalisé[fig-1285-normalized]
   :width: 11.00000cm

   Automate de phrase normalisé[fig-1285-normalized]

``Reconstrucao``
程序动态地为每个文本建立多种形式的标准化语法。由此产生的语法可以被运用文本自动机的标准化中。构造自动机的配置窗口推出“Build
clitic normalization
grammar”工具（见图 [fig-Txt2Tfst-configuration]）。该工具自动启动标准化语法的建立，如果您已勾选“Apply
the Normalization grammar”，接下来，它就会被运用在文本自动机的建立中。

保存较优路径
~~~~~~~~~~~~

有时候未知单词会与完整的已标序列产生竞争从而干扰文本自动机。如同图 [fig-unknown-word-ambiguity]的句子自动机，我们可以看到副词\ ``aujourd'hui``\ 与省文撇及动词的过去分词\ ``huir``\ 后面的未知单词\ ``aujourd``\ 之间存在竞争，

.. figure:: resources/img/fig7-8.png
   :alt: Ambiguïté due à une séquence contenant un mot
   inconnu[fig-unknown-word-ambiguity]
   :width: 11.60000cm

   Ambiguïté due à une séquence contenant un mot
   inconnu[fig-unknown-word-ambiguity]

.. figure:: resources/img/fig7-9.png
   :alt: Automate d’une phrase thaï[fig-thai-sentence-automaton]
   :width: 14.00000cm

   Automate d’une phrase thaï[fig-thai-sentence-automaton]

我们发现这个现象同样发生在处理某些亚洲文字比如泰文的过程中。当这些次没有被限定范围，就没有其他办法能预计所有可能的组合，从而创造无数条由未知单词组成的路径与已标记路径相干扰。图 [fig-thai-sentence-automaton]表示了泰语中的这种情况下句子自动机的例子。
通过勾选文本自动机构造配置窗口中的工具“Clean Text
FST”一栏(见图 [fig-Txt2Tfst-configuration])，我们可以删除干扰路径。该功能指向可将每一个句子自动机都排查清楚的自动机构造程序

.. figure:: resources/img/fig7-10.png
   :alt: Configuration de la construction de l’automate du texte
   [fig-Txt2Tfst-configuration]
   :width: 14.00000cm

   Configuration de la construction de l’automate du texte
   [fig-Txt2Tfst-configuration]

该排查根据如下主要原则被执行：如果多个路径在自动机中竞争，该程序选择留下包含未知单词最少的路径。比如序列
``aujourd'hui``
，由于该副词包含被分解的\ ``aujourd``\ 跟着一个省文撇和\ ``hui``\ ，因为\ ``aujourd``
是一个未知单词,在复合词的情况下，使用0作为未标记形式。图 [fig-clean-thai-sentence-automaton]表示图 [fig-thai-sentence-automaton]排查后的自动机。

.. figure:: resources/img/fig7-11.png
   :alt: Automate de la figure [fig-thai-sentence-automaton] après
   nettoyage[fig-clean-thai-sentence-automaton]
   :width: 10.00000cm

   Automate de la figure [fig-thai-sentence-automaton] après
   nettoyage[fig-clean-thai-sentence-automaton]

用ELAG消除词汇歧义
------------------

ELAG程序把经过改善的具有歧义的语法运用进自动机。这是一个强大的机制允许每个人创写自己的规则独立于现有的规则。本节将快速相您展示在ELAG运用下的语法形式以及该程序的功能。读者可参阅:raw-latex:`\cite{elag-blanc-dister}`和:raw-latex:`\cite{ELAG}`获取更多细节。

消除歧义的语法
~~~~~~~~~~~~~~

由ELAG配置的语法有一种特殊的句法。它们包含两个部分，我们称其为
*si*\ 部分和\ *alors*\ 部分。ELAG语法中的\ *si*\ 部分被含有\ ``<!>``\ 符号的盒子分配成两个区域。
*alors*\ 部分被符号\ ``<=>``\ 以同样的方式划分。
语法含义如下：文本自动机中，如果我们找到了一个可以被 *si*
识别的序列，那么它也应可以被语法中的\ *alors*\ 部分识别，否则它将从文本自动机中删除。

.. figure:: resources/img/fig7-12.png
   :alt: Exemple de grammaire ELAG ``elag-tu.grf``\ [fig-elag-tu]
   :width: 13.10000cm

   Exemple de grammaire ELAG ``elag-tu.grf``\ [fig-elag-tu]

图 [fig-elag-tu]展示了一个语法例子。\ *si*\ 部分通过连字符和\ ``tu``\ ，辨认出该词为第二人称单数的动词，或者为代词，或者为动词\ ``taire``\ 的过去分词。
*alors*\ 部分指定\ ``tu``\ 被视为代词。图 [fig-applying-tu-grammar]展示了
“*Feras-tu cela
bientôt\ :math:`~`?*”句中语法的应用结果。可以从低处自动机上看到与\ ``tu``\ 的过去分词对应的路径已被删除。

.. figure:: resources/img/fig7-13.png
   :alt: Résultat de l’application de la grammaire de la
   figure [fig-elag-tu] [fig-applying-tu-grammar]
   :width: 14.00000cm

   Résultat de l’application de la grammaire de la figure [fig-elag-tu]
   [fig-applying-tu-grammar]

.. figure:: resources/img/fig7-14.png
   :alt: Utilisation du point de
   sychronisation[fig-synchronization-point]
   :width: 14.00000cm

   Utilisation du point de sychronisation[fig-synchronization-point]

同步点
^^^^^^

ELAG语法中的 *si*\ 部分和\ *alors*\ 部分被\ *si*\ 部分中的第二个符号
``<!>``\ 和\ *alors*\ 部分的第二个符号\ ``<=>``\ 分隔成两块。这些符号形成了一个\ *同步点*\ 。
这将使您可以在\ *si*\ 和\ *alors*\ 的约束
下写自己的规则，而不需要排列整齐，如图 [fig-synchronization-point]列举的情况。该语法的解释如下：如果我们找到了破折号后接\ ``il,\verb``\ elle
或
``on``\ ，那么该破折号前应加一个动词，如有需要可后接\ ``-t``\ 。如果我们细看图 [fig-est-il]中由
*Est-il*\ 作为开头的句子，我们可以发现没有翻译成动词Est的解释的都被删除了。

.. figure:: resources/img/fig7-15.png
   :alt: Résultat de l’application de la grammaire de la
   figure [fig-synchronization-point][fig-est-il]
   :width: 14.00000cm

   Résultat de l’application de la grammaire de la
   figure [fig-synchronization-point][fig-est-il]

ELAG语法的编写
~~~~~~~~~~~~~~

在可以运用进文本自动机之前ELAG语法需要被编译成\ ``.rul``.文件。这项操作通过菜单里的“Text”中的“Elag
Rules”指令执行，如图1.16里的窗口显示。

.. figure:: resources/img/fig7-16.png
   :alt: ELAG语法编写窗口[fig-elag-rules]
   :width: 15.00000cm

   ELAG语法编写窗口[fig-elag-rules]

如果右边的框架中已经包含您不需要的语法，您可以通过“<<”犍将其删除。然后在左边框架里的资源管理器中选择您的语法,点击“>>”将其加入右框架的列表中。点击“Compile”犍启动\ ``ElagComp``
程序编译已选择的语法，建立默认名为\ ``elag.rul`` 的文件。

如果您已经在右边的框架中选择了语法，您可以点击“Locate”按钮搜索语法可辨认的模式。打开“Locate
Pattern”窗口，自动列举由\ ``-conc.fst2``.结尾的图形名称。该图形语法中的\ *si*\ 部分相对应。您可以因此获得文本的语法应用情况。

注意：点击“Compile”选项进行编译ELAG语法的过程中会生成用来确定语法中\ *si*\ 部分的\ ``-conc.fst2``\ 文件。因此在使用“Locate”犍进行搜索之前，首先应该先编译好您的语法

消除歧义
~~~~~~~~

当您编译好您的语法文件
``elag.rul``\ 时，您可以将其应用进文本自动机中。在文本自动机窗口中，点击“Apply
Elag
Rule”,会弹出一个对话框询问您要使用的\ ``.rul``\ 文件名称（见图 [fig-text-auto1]）。如默认文件是\ ``elag.rul``\ ，点击“OK”，启动
``Elag``\ 程序实现消除歧义。

.. figure:: resources/img/fig7-17.png
   :alt: 文本自动机窗口[fig-text-auto1]
   :width: 12.00000cm

   文本自动机窗口[fig-text-auto1]

当程序结束时，您可以点击 “Open Elag
Frame”查看自动机运行后的结果。如图 [fig-text-auto2]所示，窗口被分成两块：上方显示的是最初的自动机，下方显示的是自动机运行后的的结果。

.. figure:: resources/img/fig7-18.png
   :alt: 分成两部分的文本自动机窗口 [fig-text-auto2]
   :width: 12.00000cm

   分成两部分的文本自动机窗口 [fig-text-auto2]

如果下方的自动机显示结果较为复杂，不要惊讶。这是因为被分解的词汇条目 [1]_也会被显示出来,便于分开处理每个词形变化的说明。为了重组这些条目，点击“Implode”。单击“Explode”显示文本自动机分解图。

如果您点击“Replace”，自动机运行结果就会成为新的文本自动机。因此，如果您使用另外的语法，而那些语法已经部分消除歧义，那么将会有多个语法合并的效果。

语法集和
~~~~~~~~

为了只需要申请一次，我们可以重组多个ELAG语法使之成为一个语法集合。ELAG语法集合描述在\ ``.lst``\ 文件中。它们是从ELAG的语法编辑窗口中处理的
(图 [fig-elag-rules])。左上方的标签表示当前集合的名字，默认为
``elag.lst``\ 。这是显示在右边窗口框架的集合的内容。

如果要重命名该集合，点击“Browsz”。在弹出的对话框中，选择您想要赋予您的集合\ ``.lst``\ 的文件名。

如果要在集合中添加语法，在左侧任务栏的文件导航中对其进行选择，然后点击按钮>>。如果想撤销集合里的语法，在右侧任务栏中对其进行选择，然后点击按钮<<。当您已经选择所有的语法，点击“Compile”对其进行编译。这将会生成一个支持右下方文件名的\ ``.rul``\ 文件（文件名是通过由\ ``.rul``\ 扩展为\ ``.lst``\ 而得到）

您现在可以应用您的语法集合了。如以上所述，在文本自动机窗口点击 “Apply
Elag
Rule”犍。当对话框弹出，询问您要使用的文件名\ ``.rul``\ 时，点击“Browse”犍，选择您的集合。文本自动机的运行结果和每个已经成功应用的语法是一致的。

处理ELAG的窗口
~~~~~~~~~~~~~~

在消除歧义的过程中，
``Elag``\ 程序在处理窗口中运行，可以看到在其执行过程中通过程序发送的信息。

比如，当文本自动机包含未与ELAG的标签集进行匹配的标签时（见下一节），会有一条信息指出错误性质。同样的，当一句句子被排斥时（所有的可能的分析都会被语法删除），一条信息就会指出句子的号码。就可以快速的确定问题的来源。

评估歧义率
^^^^^^^^^^

歧义率的评估并不是仅仅基于每个单词的平均解释次数。为了能有一个更具代表性的测量，该系统还需要考虑到单词的不同组合。在消除歧义过程中,
``Elag``\ 程序（根据自动机里的可能路径）计算文本自动机中变更前后可能的分析次数。基于这个数值，程序计算每个单词句子的平均歧义，这是用于表示文本歧义率的最后一项测量，因为它不会随着语料库大小和句子数量的变化而变化。应用计算公式为：

*taux
d’ambiguïtés*\ :math:`=exp^{\frac{log(nombre de chemins)}{longueur du texte}}`

语法变更前后的歧义率之间的联系提供了了它的效率量度。所有的信息都在ELAG的处理窗口中显示。

标签规则说明
~~~~~~~~~~~~

程序\ ``Elag``\ 和\ ``ElagComp``
需要已用字典的正式标签规则的说明。该说明大致包括所有字典中现有语法种类的目录,每一种语法中与句法、词形变化有关的代码条目和和它们之间可能的组合描述。这些信息描述在主目录里名为\ ``tagset.def``\ 文件夹中，在语言选择的子目录下。

``tagset.def`` 文件
^^^^^^^^^^^^^^^^^^^

这里是一个使用法语的\ ``tagset.def``\ 文件摘要。

::



    NAME french

    POS ADV
    .

    POS PRO
    flex:
    pers   = 1 2 3
    genre  = m f
    nombre = s p
    discr:
    subcat = Pind Pdem PpvIL PpvLUI PpvLE Ton PpvPR PronQ Dnom Pposs1s...
    complete:
    Pind     <genre> <nombre>
    Pdem     <genre> <nombre>
    Pposs1s  <genre> <nombre>
    Pposs1p  <genre> <nombre>
    Pposs2s  <genre> <nombre>
    Pposs2p  <genre> <nombre>
    Pposs3s  <genre> <nombre>
    Pposs3p  <genre> <nombre>
    PpvIL    <genre> <nombre> <pers>
    PpvLE    <genre> <nombre> <pers>
    PpvLUI   <genre> <nombre> <pers>      #
    Ton      <genre> <nombre> <pers>      # lui, elle, moi
    PpvPR                                 # en y
    PronQ                                 # ou qui que quoi
    Dnom                                  # rien
    .

    POS A ## adjectifs
    flex:
    genre  = m f
    nombre = s p
    cat:
    gauche = g
    droite = d
    complete:
    <genre> <nombre>
    _  # pour {de bonne humeur,.A}, {au bord des larmes,.A} par exemple
    .


    POS V
    flex:
    temps  = C F I J K P S T W Y G X
    pers   = 1 2 3
    genre  = m f
    nombre = s p
    complete:
    W
    G
    C <pers> <nombre>
    F <pers> <nombre>
    I <pers> <nombre>
    J <pers> <nombre>
    P <pers> <nombre>
    S <pers> <nombre>
    T <pers> <nombre>
    X 1 s   # eusse dusse puisse fusse (-je)
    Y 1 p
    Y 2 <nombre>
    K <genre> <nombre>
    .

``#``\ 符号指的是该行其余部分都是注释。注释可以出现在文件中的任何位置。文件始终由\ ``NAME``\ 开始，随后是一个识别码(\ ``比如french``)。该文件的其余部分由
``POS``\ 节(即 Part-Of-Speech,
词类部分)组成，每个语音类别分别有一节。每一节都描述了属于该语法范畴词汇标签的结构。每一节由四个部分组成，以下可供选择：

-  ``flex``\ ：
   这部分列出了相关的语法范畴由词形变化的代码。例如代码\ ``1,2,3``
   表示进入的人，对于代词时贴切的，但并不适用于主语。每一行表示与词形变化相关的属性（性别，时间等），并且由\ ``=``\ 后的属性名称和它可以采取的值组成；比如以下的一行表示的是可以取值为\ :math:`1`,
   :math:`2` 或 :math:`3`\ 的\ :math:`pers`\ 属性。

   ::

       pers = 1 2 3

-  ``cat``:
   该部分表示的是句法和语义的属性，它们可以归因于属于该语法范畴的输入。每一行描述一个属性和它可以采取的值。表示同一属性的代码必须是互相排斥的。也就是说，入口不可以同一属性采取多个值。然而存在给定一个属性而不采取任何值的标签。比如，定义\ ``niveau_de_langue``
   属性，取值\ ``z1``, ``z2`` et ``z3``\ ，表示如下：

   ::

       niveau_de_langue = z1 z2 z3

   但是这个属性不一定存在于所有的单词中。

-  ``discr``:
   该部分是由单个属性声明构成。语义与\ ``cat``\ 部分是一样的并且这里表示的属性不应在\ ``cat``\ 里重复;在有相似词形变化的属性的语法目录中，该部分可将语法目录分成子目录\ *discriminantes*\ 。比如代词，指代人，属于人称代词的子类别，但是并不再关系代词的条目中。在\ ``complete``\ 部分中会对依赖关系进行说明；

-  ``complete``:
   这部分解释属于常见的语法类词的形态标记。每一行根据子目录的判断描述词形变化代码的有效组合（如果这样的类已经声明）。当属性名称显示在(\ ``<``\ 和\ ``>``)之间时，这意味着任何值都适用于该属性。也可以利用只包含
   ``_``
   (下划线)的一行声明一个条目不包含任何字符。比如，如果我们将以下的字行看作与动词描述相关的摘要：

   ::

       W
       K <genre> <nombre>

   这可以表示没有其他词性变化特征的动词不定式（由\ ``W``\ 表示）而当是过去分词(code
   ``K``)时需要与性与数相配合。

词形变化码的说明
^^^^^^^^^^^^^^^^

``discr``\ 部分的主要作用是区分子目录下有相似形态特性的标签。然后该子目录可方便编写
``complete``\ 部分。

为了ELAG语法的可读性，尽可能相同子目录下的元素都有相同的词形变化特征；在这情况下，每个子目录，\ ``complete``
部分都只由一行组成。

比如参考以下例子，选自代词的说明：

::

    Pdem  <genre> <nombre>
    PpvIl <genre> <nombre> <pers>
    PpvPr

这些行表示:

-  所有指示代词(\ ``PRO+Pdem>``)都有性与数的特征；
   (``<PRO+PpvIl>``)是由一个人、性与数进行形态标记；

-  介词代词 (*en*, *y*)没有词性变化特征。

所有出现在词典里的词形变化特征和判别式组合都应描述在\ ``tagset.def``\ 文件夹里；
否则相应的条目会被ELAG删除

在同一个子目录下的单词被它们的词形变化特征区分的情况下，
必须在\ ``complete``\ 部分写若干行。这种描述方式不足的地方是在ELAG语法下在这些单词间进行区分比较困难。

参考上述例子的说明，有些法语中的形容词有性数的特征，而另一些没有词形变化的特征。比如固定短语如\ *de
bonne humeur*\ ，它的句法特征与形容词相似。

，因而不用遵循词形变化。问题是如果我们想在消除歧义的语法里只参考这一类的形容词，
``<A>``\ 标志是不包含在其中的，因为它是给所有形容词的。
为了解决这个问题，在符合这个属性的其中一个值前面写下\ ``@``
这个字符时，可以否认词形变化属性。因此\ ``<A:@m@p>``\ 符号可以识别所有既没有数量也没有性别的形容词。在这个操作下，现可以写出如同图 [fig-NA]的语法，规定名词与形容词之间的性别与数量的配合 [2]_。

这样的句子是被归纳在法语词典里的只要形容词词尾不变，没有词形变化。问题是，如果我们只想在歧义消除语法中参考这一类的形容词，\ ``<A>``\ 符号不适用，因为它只是适用于所有形容词。为了避免这个问题，可以通过在符合这种属性的可能的值之前写下\ ``@``\ 来否定其词形变化属性，因此\ ``<A:@m@p>``\ 符号可以辨识所有没有性数的形容词。通过这个操作，目前可以写出如图 [fig-NA]的语法，使名词与形容词之间的性数相配合，如 [3]_.这个语法保留句子的正确分析如：\ *Les
personnes de bonne humeur m’insupportent*.

然而建议少使用@操作，因为它会影响文法的可读性。最好区分在\ ``discr``\ 部分，通过子目录判别定义接受不同词形变化部分的标签。

.. figure:: resources/img/fig7-19.png
   :alt:  ELAG文法纠正名词与形容词之间的性数配合，如下 [fig-NA]
   :width: 12.00000cm

    ELAG文法纠正名词与形容词之间的性数配合，如下 [fig-NA]

可选码
^^^^^^

句法代码和可选的语义在猫部分声明。他们
可以在ELAG文法与其它代码一起使用。所不同的是，在加载文本自动机时，
这些代码不会参与决定一个标签是否应被拒绝 禁用与否。

这些都是可选的代码，与其他代码相独立，像比如语言级别属性(\ ``z1``,
``z2`` 或 ``z3``)。 与之相同的还有词形变化码，它同样可以在名词属性前写
``!``\ 符号时拒绝词形变化属性。因此同我们的示例文件，\ ``<A!gauche:f>``\ 标志可以识别所有没有\ ``gauche``\ 码的阴性形容词，
 [4]_.

``tagset.def``
文件中声明的代码都会被ELAG忽略。如果一个词典条目有这样的代码，ELAG会产生警告并删除此代码。

因此如果两个并发的条目因代码没有声明而没有在原始的文本自动机中区分，这些条目会通过程序区分并且统一到自动机结果中的单个条目里。

因此在\ ``tagset.def``
文件里的标签设置可以减少歧异，分解只与没有声明的代码不同的和与应用语法相独立的单词。

例如在最完整的法语字典里，每一个动词区分检查的特征在于它是通过参考描述它的词汇文法表。到目前为止，我们考虑信息重组，词法语法分析，而且我们没有因此掺入标签集的描述。因此加载文本自动机的时候它可以自动降低歧异率从而自动消除。

为了很好得区分与ELAG语法的标签设置的相关效果，建议在运用消除歧异语法前先进行一步文本标准化。此标准化化是不给文本自动机的语法施加任何约束来实现，如图 [fig-elag-norm]。注意出，此语法在Unitex中通常存在并在\ ``norm.rul``.文件中预编译。

.. figure:: resources/img/fig7-20.png
   :alt: Grammaire ELAG n’exprimant aucune contrainte[fig-elag-norm]
   :width: 9.00000cm

   Grammaire ELAG n’exprimant aucune contrainte[fig-elag-norm]

这个语法的运用结果是原始自动机的所有没有写进\ ``tagset.def``,
文件的、没有与这个描述一致（因为属于未知活用语法范畴或性数无配合）的代码都会被清除。因此在通过以标准化的自动机替换文本自动机时，我们可以确定之后的自动机调整都只是因为ELAG语法的作用。

优化语法
~~~~~~~~

通过\ ``ElagComp``
程序执行的语法的汇编包含建立一个自动机，其语言是一组没有被文法拒绝词汇条目序列（或一个句子或词汇的解释）。这个任务是复杂的，可能需要较长的时间，但写入文法时它可以显著加快观察某些原则。

限制分支数量 *alors*
^^^^^^^^^^^^^^^^^^^^

建议可以减少\ *alors*\ 部分的数量，这可以显著减少编译文法的时间。大多数情况下，一个有许多\ *alors*\ 部分的语法可以用一个或两个
*then*\ 部分不损失易读性地重写。比如图 [fig-NA-bad]中的语法规定它后面的动词和代词之间的约束。

.. figure:: resources/img/fig7-21.png
   :alt: Grammaire ELAG vérifiant l’accord entre verbe et
   pronom[fig-NA-bad]
   :width: 15.00000cm

   Grammaire ELAG vérifiant l’accord entre verbe et pronom[fig-NA-bad]

如图 [fig-NA-good]所示，我们可以写一个等效语法逐一分解所有textitalors部分。两个语法将具有完全相同的文字自动机相同的效果，但在第二次将被更快地编译。

.. figure:: resources/img/fig7-22.png
   :alt: 优化的ELAG语法修正动词与名词之间的配合[fig-NA-good]
   :width: 15.00000cm

   优化的ELAG语法修正动词与名词之间的配合[fig-NA-good]

词法符号的使用
^^^^^^^^^^^^^^

最好只在必要的时候使用该辅助定理，尤其时对于那些符合语法规则的词的子目录和它们的辅助定理拥有同样多的信息的时候。如果非要在符号里使用辅助定理，建议尽可能使语法、语义、歧义精确。比如法语字典中，用
``<PRO+PpvI1:1s>``\ 符号来替代
``<je.PRO:1s>``\ ，\ ``<je.PRO+PpvIL:1s>``
，\ ``<je.PRO>``\ 这些符号会更好。实际上，这些符号都是一样的，都只能识别\ ``{je,PRO+PpvIL:1ms:1fs}``\ 字典词条这种程度。然而，如该程序不能自动推断该信息，如果不使这些功能精确，那么该程序就会认为
``<je.PRO:3p>``, ``<je.PRO+PronQ>`` 等标签不存在，是徒劳的。

涂鸦文本自动化的线性化
----------------------

默认情况下，文本自动机由于包含词汇歧义所以由多个标签路径。线性化的过程是选择一个单一路径，一个通过筛选、删除其他标签得到的标签序列。结果就是一个有着单一路径的文本自动机（如图[section-linear-text]将线性自动机转变成线性文本）。
路径的选择取决于他的得分。 具有最高得分的路径被选择而其他删除
路径的分数是由受过编辑的上一个注释的语料库的统计模型进行计算。
该模型通过TrainingTagger程序（见
[section-TrainingTagger]）使用涂鸦文件数据。
比如，如图[fig7-linearize2]，\ *Les insectes nuisibles envahissent la
maison*\ 的最初的自动机。将其线性化之后，如图 [fig7-linearize3]。

.. figure:: resources/img/fig7-linearize2.png
   :alt: *Les insectes nuisibles envahissent la
   maison.*\ [fig7-linearize2]的文本自动机
   :width: 16.00000cm

   *Les insectes nuisibles envahissent la
   maison.*\ [fig7-linearize2]的文本自动机

.. figure:: resources/img/fig7-linearize3.png
   :alt: 线性文本自动机[fig7-linearize3]
   :width: 16.00000cm

   线性文本自动机[fig7-linearize3]

标签的兼容性
~~~~~~~~~~~~

涂鸦词汇的标签集和语料标签一样或属于统一类型(见下图)。每次使用文本自动机上的涂鸦文本时，我们需要注意标签集和词法。模型的标签集应该与文本自动机的标签集一致。比如，如果统计模型用标签集
``DET`` pour les mots
``the``\ 计算，文本里对应的标签集应该是\ ``DET``\ 。Unitex有一个功能可以改变文本中单词的形式，比如使
``doesn't`` en
``does not``\ 形式化，应用置换图或规范化图形可能导致单词形状的变化。
如果这样的处理被应用到文本，它必须也已应用到训练语料。如果这些规则不遵循，则标记器可能无法找到在文本自动机所需的路径。

TrainingTagger程序产生两种类型的涂鸦文本。第一种删除基于gramaticaux码、语义、句法的过渡口(\ ``that.DET+Ddem``
au lieu de
``that.PRO+Pdem``)。这种处理促进驱动而且那些词性变化的信息不再适用于所有的应用。

标注器的使用
~~~~~~~~~~~~

线性化的文本自动机，则必须选择在配置窗口“的标注器线性化”，构建文本自动机(cf.
图 [fig7-linearize1])。有了这个操作，该程序线性化自动机里的所有句子。
你需要单击“Set”犍同时选择标注器的文件数据 (扩展名是 “.bin”)。后缀为
“morph”标注器文件数据是第一种类型(有词性变化码)
，后缀为“cat”的是第二种类型
（没有词形变化码）。如果你使用“morph”类型，你需要同时点击“Normalize
accordind to Elag tagset.def” （更多细节，看 [section-Tagger]
关于\ ``Tagger``\ 程序）。

.. figure:: resources/img/fig7-linearize1.png
   :alt: 配置文本自动机的线性化[fig7-linearize1]
   :width: 13.00000cm

   配置文本自动机的线性化[fig7-linearize1]

比如图[fig7-linearize3]的文本自动机，是图
[fig7-linearize2]线性文本自动机的出口，“cat”版本。“morph”版本的线性化文本自动机如图[fig7-linearize4]。

.. figure:: resources/img/fig7-linearize4.png
   :alt: 有着“morph”类数据的线性文本自动机[fig7-linearize4]
   :width: 16.00000cm

   有着“morph”类数据的线性文本自动机[fig7-linearize4]

创建一个新的涂鸦文本
~~~~~~~~~~~~~~~~~~~~

为您创造语言的新恶搞，你必须在你自己标注的语料库里启动TrainingTagger程序。标注的资料在[section-corpus-file]编译。正如我们注意到的[section-linearization-tagset]部分，你需要注意标签集和词法。在计算统计模型前，您必须确定您将使用哪个字典和规范化图构建文本自动机，然后，如果单词或标签集的形式不完全相同，你需要改变标注语料库。比如，如果标准化图形转换\ ``jusqu'``
en ``jusque``\ ，在标记的语料库里对应的单词应该是\ ``jusque``\ 。

对于Unitex自带的法语涂鸦文本。它被由缺乏语义和句法的代码的标签组成的标记语料库创建。

操作文本自动机
--------------

显示句子自动机
~~~~~~~~~~~~~~

如之前我们所看到的，文本自动机是文本里所有句子自动机的组合。这个结构可以由\ ``.fst2``\ 展示，被用来表示被编译的语法。然而，
此格式不直接显示的句子控制器。需要使用\ ``Fst2Grf``\ 程序来将句子自动机转换成图形来显示它。当你选择一句句子来生成文件
``.grf``. 时，这个程序会被自动调用。

生成的\ ``.grf``\ 文件不以和用户自己构造的图
``.grf``\ 文件一样的方式解释说明。实际上在一个正常的图中，一个框的线是由
``+``\ 符号分隔开来，
在一个表示句子的图中，每一个框，要么是一个没有标签的词汇的集合，要么是一个由大括号阔起来的字典词条。如果框中只包含了没有标签的词汇集合，后者就会单独出现在框中。如果框中包含一个字典条目，词尾变化的形式也会显现，如果与规范形式不同，规范形式也会显示。语法信息和词性变化信息也会显示在框的下面。

图 [fig-first-sentence-Ivanhoe]指出由第一句话\ *Ivanhoe*\ 得到的图。
``Ivanhoe``, ``Walter``\ 单词和
``Scott``\ 被当作生词。单词\ ``by``\ 在字典中对应两个词条。
``Sir``\ 在字典里也对应两个词条，但是其规范形式是\ ``sir``\ ，用小写字母区分词性变化形式。

.. figure:: resources/img/fig7-23.png
   :alt: 第一句句子自动化 *Ivanhoe*\ [fig-first-sentence-Ivanhoe]
   :width: 11.00000cm

   第一句句子自动化 *Ivanhoe*\ [fig-first-sentence-Ivanhoe]

手动更改文本自动机
~~~~~~~~~~~~~~~~~~

可以通过手动更改句子自动机，除了出现保存在在ELAG范围
(底部范围)里的。你可以添加，转换，删除框或过渡部分。当一个图被修改，它会被保存在名为``sentenceN.grf``\ 的文本目录里，\ :math:`N`\ 表示句子数量。

当你选择一个句子，如果存在这句话的图形变化，且显示出来。您可以通过点击“Reset
Sentence Graph”实现句子自动化。 (如图 [fig-modified-sentence-automaton])

.. figure:: resources/img/fig7-24.png
   :alt: 句子自动机的修改[fig-modified-sentence-automaton]
   :width: 15.00000cm

   句子自动机的修改[fig-modified-sentence-automaton]

当创建文本自动机时，所有文本目录里目前修改的句子图都会被删除。

注意：手动更改您的账户时可以重新建立您的文本自动机。点击“Rebuild
FST-Text”选项，重新建立。所有已经被修改的句子都会在文本自动机里被修订过的文本替换，新的文本自动机就会重新启动

手动消除歧义
^^^^^^^^^^^^

因为词汇歧义，文本自动机可以包含多条标签路径。你可以用ELAG程序或手动选择句子自动机里一个或所有句子
进行歧义消除。有多个不同标签的框出现时，在你想要保留的框上点击右犍。你选择的框的边缘会加粗而其他的会变灰色(如图 [fig-manually-resolve-ambiguities])。

.. figure:: resources/img/fig7-24b.png
   :alt: 在句子自动机里手动消除歧义[fig-manually-resolve-ambiguities]
   :width: 15.00000cm

   在句子自动机里手动消除歧义[fig-manually-resolve-ambiguities]

点击“Remove greyed
states”犍只保留选择的框。(如图 [fig-removed-ambiguities])。

.. figure:: resources/img/fig7-24c.png
   :alt: 在句子自动机中取出有歧义的框 [fig-removed-ambiguities]
   :width: 11.00000cm

   在句子自动机中取出有歧义的框 [fig-removed-ambiguities]

显示参量
~~~~~~~~

句子自动机和图形遵循同样的显示选项。它们共享相同的颜色和字体，以及使用的抗混叠的影响。为了形成句子自动机的界面，你需要在“Info”菜单里点击
“Preferences...”设置主要外形。更多细节，请看 [section-display-fonts-colors]。

你可以在“FSGraph”菜单中点击“Print...”打印句子自动机或使用快捷键<Ctrl+P>，确保打印方向设置为横向模式。。
，要调整此设置，单击“FSGraph”菜单中的“Page Setup”。

转换文本自动机为线性文本
------------------------

如果文本自动机不再有歧义，可以建立文本文件对应一个唯一路径。进入菜单“Text”点击
“Convert FST-Text to
Text...”。如图所示窗口 [fig-linearization-configuration]，
然后就可以设置输出文本文件

.. figure:: resources/img/fig7-25.png
   :alt: 选择输出文件，文本自动机的线性化[fig-linearization-configuration]
   :width: 10.00000cm

   选择输出文件，文本自动机的线性化[fig-linearization-configuration]

如果自动机没有线性化，一个错误信息会告诉你第一句的编号包含歧义。否则
``Tfst2Unambig``\ 程序根据以下原则构建输出文件

-  文件逐行输出；

-  除了最后一行的句子外所有句子都要以\ ``{S}``\ 结尾；

-  在框里写的程序之后后需要后接空格。

.. figure:: resources/img/fig7-26.png
   :alt: 线性文本自动机的例子[fig-linear-automaton]
   :width: 12.00000cm

   线性文本自动机的例子[fig-linear-automaton]

注意：

NOTE : 空间管理完全留给用户。因此如果初始文本是如图所示的自动机样式
[fig-linear-automaton], 生成的文本将是:

::

    2 3 {cats,cat.N+Anl:p} {are,be.V:P2s:P1p:P2p:P3p} {white,white.A} .

文本自动机里的模式搜索
----------------------

Unitex的\ ``LocateTfst``\ 程序可以在文本自动机中实现搜索。最主要的好处是我们可以：

-  优化消除歧义; (如下);

-  在几个形态层面的工作（复合词，简单的单词语素）。\*
   这个很有趣，因为你可以很容易地操纵汇聚语言，如朝鲜语（见
   [section-korean]）

规则与应用\ ``Locate``\ 搜索特别相似。这里是一些不同点：

Les règles sont très proches de celles qui s’appliquent lors des
recherches avec ``Locate``. Voici les différences:

-  你无法记住变量序列，\ ``Locate`` (如图 [fig-context6], 页面 )

-  你无法识别非文本自动机：如果文本自动机只包含一个词组的标签，却没有其中包含的单词，你就不能识别这些单词。比如在如图的这个句子中 [fig7-locatetfst1]，不可能会识别\ ``soixante``
   或\ ``huit``\ ，因为其路径不存在。

   .. figure:: resources/img/fig7-locatetfst1.png
      :alt: 自动机无法识别的模式 *huit*\ [fig7-locatetfst1]
      :width: 9.00000cm

      自动机无法识别的模式 *huit*\ [fig7-locatetfst1]

-  识别顺序可能会有所不同。实际上文本自动机可以包含不与输入文本匹配的标签，尤其是当语法标准被施加时。比如你在\ *80jours*\ 文本自动机中搜索\ ``<le.DET>``
   模式，你会得到7703匹配，而\ ``Locate``\ 只能搜索到5763个。这是因为，只有几个字已经标准化，
   ``au`` :math:`\rightarrow` ``à le`` ou ``du``
   :math:`\rightarrow`\ ``de le``\ 。因此如果你搜索\ ``<le.DET>``\ ，
   ``LocateTfst``\ 识别由语法标准添加到文本自动机的标签，
   ``Concord``\ 使用原始文本文件建立一致性，如图所示 [fig7-locatetfst2]。

   .. figure:: resources/img/fig7-locatetfst2.png
      :alt: 模式一致 ``<le.DET>``\ [fig7-locatetfst2]
      :width: 14.00000cm

      模式一致 ``<le.DET>``\ [fig7-locatetfst2]

-  ``<TOKEN>``
   不能识别这些在\ ``tokens.txt``\ 定义的tokens。它识别任何文本自动机的标签。如果时词组的标签，识别的标签可能比tokens更长，如果自动机包括类似\ ``un``\ 的形态分析，甚至会更短如图[morphoB]，页面
   。

-  即使没有进入形态模式，你可以定义变量字典(cf.
    [dictionary-variables])。然后可以处理有词性变化的变量，规范形式和相应的代码词汇，语法类提取物，
   它们的语义代码，它们的屈折码和值
   ``yyy``\ 属性的\ ``zzz``\ ，如果是否含有以下形式的代码
   ``yyy=zzz``\ ，

。

显示表格
--------

句子自动机可以以表格形式显示。要做到这一点，只需
选择在控制器文本框中的“表格”选项卡。你会看到一个表格，如图[fig7-table1]。

.. figure:: resources/img/fig7-table1.png
   :alt: 显示表格[fig7-table1]
   :width: 14.50000cm

   显示表格[fig7-table1]

此表是不完全等同于句子自动机，因为它仅显示为每个单个或复合词可能的POS。它应被视为包含在控制器中的信息中粗略的和紧凑的图。您还可以过滤语法/语义代码显示。选择“All”然后你可以看到所有代码。选择
“Only POS category”第一个代码（代表POS类别）。如果你选择 “Use filter”
写一个正则表达式\ :math:`X`\ ，不会被\ :math:`X`\ 识别的代码将会被删除。所有
POSIX 的正则表达式都会作为过滤器被接受。确认“Always show POS
category”也就是说POS类将会被保留即使没有被过滤器匹配。详情请见
[fig7-table2]，展示了一个过滤结果，
经\ ``^[A-Z]``\ 筛选过滤匹配任何由大写字母开头的单词，因此去除\ ``z1``\ 这样的字符。

.. figure:: resources/img/fig7-table2.png
   :alt: 显示筛选表格[fig7-table2]
   :width: 14.50000cm

   显示筛选表格[fig7-table2]

“Export all text as POS
list”犍可以用来在文本文件里输出自动文本集显示在表格里，使用最常用的表格。实际上这个功能时有实验性的病并且将来还有可能作调整。这里是输出实例。

::

    (Je/N:ms:mp)|(Je/PRO/PpvIL:1fs:1ms) (suis/V:P1s)|(suis/V:Y2s:P2s:P1s) 
    M/N:mp:ms . Mdiba (de/DET/Dind:fp:mp:fs:ms)|(de/PREP)|(de/PREP/z1
    +de la/DET/Dind/z1:fs)|(de/PREP/z1+des/DET/Dind/z1:mp:fp)|(de/PREP/z1
    +du/DET/Dind/z1:ms)|(de la/DET/Dind/z1:fs)|(des/DET/Dind/z1:mp:fp)|
    (du/DET/Dind/z1:ms) LG - ville/N:fs . {S}

韩语的特殊情况
--------------

韩国是一个具有非常特殊形态的粘着语：单词音节代表韩文称为字符组成，但Hangul字符对应的字母JAMO的几个字符。比如我们从图
[fig7-korean1] 看出两个Hangul的例子，后接它们同等的Jamo。

.. figure:: resources/img/fig7-korean1.png
   :alt: 符号和它们对应的字母 [fig7-korean1]
   :width: 4.50000cm

   符号和它们对应的字母 [fig7-korean1]

另外，词素不必对应于朝鲜文字符。如图[fig7-korean2]表示一个给定的令牌（绿色）必须分析
作为两个元素的组合：一个动词和变指数。问题是变指数只形成与动词
Hangul最后一个字符组合的Jamo字符作为韩文整个单词的最后一个字符（绿色）。绿色的令牌与没有被标注的令牌对应。没有被标注的令牌在其他语言中没有被标为绿色。

.. figure:: resources/img/fig7-korean2.png
   :alt: Hangul字符分解[fig7-korean2]
   :width: 6.00000cm

   Hangul字符分解[fig7-korean2]

因此，使用韩语的人优先用一个
Hangul和Jamo字符的结合来写语法。因此，如图[fig7-korean3]的语法识别如图[fig7-korean4]的序列。

.. figure:: resources/img/fig7-korean3.png
   :alt: 有两个Jamo字母的语法[fig7-korean3]
   :width: 5.50000cm

   有两个Jamo字母的语法[fig7-korean3]

.. figure:: resources/img/fig7-korean4.png
   :alt: 通过图[fig7-korean3][fig7-korean4]
   :width: 13.00000cm

   通过图[fig7-korean3][fig7-korean4]

的语法识别的句子自动机

注意:

#. Jambo
   字母不再包含韩语字母的文件(\ ``Alphabet.txt``)中。不要添加到这个文件中，因为这会导致程序出现故障.

#. 该脚本文件包含某些中国字符和一些韩文。在实践中，如果语法同时包含中文和韩文，可以在文本自动机中自动将他识别出来。比如[fig7-korean5]图所示的语法可以识别[fig7-korean4]图中的句子。因为字母表包含了相同的字符如图所示
   [fig7-korean6].

.. figure:: resources/img/fig7-korean5.png
   :alt: 有汉字的语法[fig7-korean5]
   :width: 5.00000cm

   有汉字的语法[fig7-korean5]

.. figure:: resources/img/fig7-korean6.png
   :alt: 处理包含韩文的文件[fig7-korean6]
   :width: 3.50000cm

   处理包含韩文的文件[fig7-korean6]

.. [1]
   这些条目重组多个随词形变化的解释，比如：\ ``{se,.PRO+PpvLE:3ms:3fs:3mp:3fp}``.

.. [2]
   这个语法并不是完全正确，因为它排除了一些情况，比如分析这句：\ *J’ai
   reçu des coups de fil de ma mère hallucinants.*\ 时，判断其为正确

.. [3]
   这个语法比你个不是完全正确，因为它排除了一些情况，比如分析这句\ *J’ai
   reçu des coups de fil de ma mère hallucinants.*\ 时，判断其为正确

.. [4]
   这个代码表示形容词应该出现在所形容的名词左边，像\ *bel*\ 这样的情况Ce
