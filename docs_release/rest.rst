.. highlightlang:: rest

.. _rst-primer:

reStructuredText入门
=======================

本节简要介绍了reStructuredText (reST)的概念和语法，旨在提供足够的信息来高效地编写文档。因为reST是一个简单的，不显眼的标记语言，这不会花费太长时间来入门。

.. seealso::

   权威的 `reStructuredText用户文档 <http://docutils.sourceforge.net/rst.html>`_。  


段落
----------

段落(:duref:`ref <paragraphs>`)是reST文档中最基本的块。段落是由一个或多个空白行分离的简单的文本块。在Python中，缩进在reST中是具有重要意义，所以同一段落的所有行必须左对齐而且是同一级缩进。


.. _inlinemarkup:

行内标记
-------------
注：因为找不到合适的词语来翻译role，所以没有翻译！

标准的行内标记相当简单：使用

* 单星号： ``*text*`` 强调 (斜体),
* 双星号： ``**text**`` 重点强调 (粗体)，以及
* 反引号： ````text```` 代码示例。

如果星号或反引号出​​现在文本会对行内标记分隔符引起混淆，他们必须用一个反斜杠进行转义。

注意行内标记一些限制:

* 不能嵌套，
* 文本不能以空格开始或者结束： ``* text*`` 是不正确的，
* 必须由空格从周围的文本中分离出来。可以通过使用转义的空格来规避这个限制：thisis\ *one*\ word。

docutils以后的版本可能会取消上列出的这些限制。

reST也允许自定义“文本解释role”，这就意味着所包含的文本应以一种特定的方式解释。Sphinx用它提供了语义标记和交叉引用的标识符。一般的语法格式是 ``:rolename:`content``` 。

标准的reST提供了如下些roles：

* :durole:`emphasis` -- 来替代 ``*emphasis*``
* :durole:`strong` -- 代替 ``**strong**``
* :durole:`literal` -- 代替 ````literal````
* :durole:`subscript` -- 下标文本
* :durole:`superscript` -- 上标文本
* :durole:`title-reference` -- 书，期刊，以及其他材料的标题

Sphinx添加的roles请见 :ref:`inline-markup`。


列表和“类”引用块
---------------------------

列表标记(:duref:`ref <bullet-lists>`) 是自然的：只要在段落开头放置一个星号和缩进正常。带编号的列表同样适用；它们也可以自动编号通过使用标志 ``#``::

   * This is a bulleted list.
   * It has two items, the second
     item uses two lines.

   1. This is a numbered list.
   2. It has two items too.

   #. This is a numbered list.
   #. It has two items too.


嵌套列表是可能的，但要知道，它们必须由空行从父列表中分隔::

   * this is
   * a list

     * with a nested list
     * and some subitems

   * and here the parent list continues

定义列表 (:duref:`ref <definition-lists>`) 的创建::

   term (up to a line of text)
      Definition of the term, which must be indented

      and can even consist of multiple paragraphs

   next term
      Description.

请注意，**term** 不能有一个以上的文本行。

引用段落(:duref:`ref <block-quotes>`) 可以通过比周围的段落更缩进来创建。

行块元素 (:duref:`ref <line-blocks>`) 是防止行被破坏的方式（保留行原样的方式）::

   | These lines are
   | broken exactly like in
   | the source file.

还有其它几个特殊的功能块:

* field lists (:duref:`ref <field-lists>`)
* option lists (:duref:`ref <option-lists>`)
* quoted literal blocks (:duref:`ref <quoted-literal-blocks>`)
* doctest blocks (:duref:`ref <doctest-blocks>`)


源代码
-----------

文字代码块(:duref:`ref <literal-blocks>`)是在段尾加入特殊标记 ``::`` 引入的。文字代码块必须缩进（像所有的段落，是通过空行来分离的）::

   This is a normal text paragraph. The next paragraph is a code sample::

      It is not processed in any way, except
      that the indentation is removed.

      It can span multiple lines.

   This is a normal text paragraph again.

``::`` 标记的处理非常聪明:

* 如果出现在段落本身中，那么整个段落将会从文档中删除（也就是说不会出现在生成的文档中）。
* 如果它前面的空白，标记将被删除。
* 如果它的前面非空白，标记会被单个冒号取代。

通过这种方式，上面第二句将呈现为 "The next paragraph is a code sample:"。


.. _rst-tables:

表格
------

Sphinx支持两种表格形式。对于 *格子表格* (:duref:`ref <grid-tables>`)，必须自己“画”自己的单元格。它们看起来像这样::

   +------------------------+------------+----------+----------+
   | Header row, column 1   | Header 2   | Header 3 | Header 4 |
   | (header rows optional) |            |          |          |
   +========================+============+==========+==========+
   | body row 1, column 1   | column 2   | column 3 | column 4 |
   +------------------------+------------+----------+----------+
   | body row 2             | ...        | ...      |          |
   +------------------------+------------+----------+----------+

*简单表格* (:duref:`ref <simple-tables>`) 更容易书写，但是有限制：表格必须是两行以及以上，而且第一列不能包含多行。它们看起来像这样::

   =====  =====  =======
   A      B      A and B
   =====  =====  =======
   False  False  False
   True   False  False
   False  True   False
   True   True   True
   =====  =====  =======


超链接
----------

外部链接
^^^^^^^^^^^^^^

使用 ```Link text <http://example.com/>`_`` 来实现内嵌的网页链接。如果链接文本是Web地址，你一点都不需要特殊标记，解析器可以识别在普通的文本的链接和邮件地址。

你也可以把链接和目标定义(:duref:`ref <hyperlink-targets>`)分开，像这样::

   This is a paragraph that contains `a link`_.

   .. _a link: http://example.com/


内部链接
^^^^^^^^^^^^^^

内部链接是通过Sphinx提供的一个特殊的reST role来实现的，请看 :ref:`ref-role`.


章节
--------

章节头 (:duref:`ref <sections>`) 是用特殊的标点符作为章节标题的下划线来创建的（上划线是可选的），只要文字::

   =================
   This is a heading
   =================

通常，没有特定的字符指定给标题级别，因为结构是用从继承的标题来确定的。对于python文档，本公约您可以按照：

* ``#`` with overline, for parts
* ``*`` with overline, for chapters
* ``=``, for sections
* ``-``, for subsections
* ``^``, for subsubsections
* ``"``, for paragraphs

当然，您可以自由使用自己的标记字符（参看reST文档），并使用一个更深层次的嵌套级别，但请记住，大多数的目标格式（HTML，LaTeX）有限地支持嵌套深度。


显式标记
---------------

"显式标记" (:duref:`ref <explicit-markup-blocks>`) 在reST中是用于需要进行特殊处理的结构，比如脚注，特别突出的段落，注释，和通用指令（标识符）。

显式标记块的第一行是以 ``..`` 开始，接着是紧随着空格，被结束于同样层级缩进的下一段落。（显式标记和正常的段落之间需要有一个空行。当你写它的时候，可能听起来有点复杂，但它是直观的。）


.. _directives:

指令（标识符）
----------------

指令或者标识符（:duref:`ref <directives>`）是一个通用的显式标记块。除了roles，指令或者标识符是reST的扩展机制，Sphinx大量地使用了它。

Docutils支持如下的指令（标识符）：

* 警告: :dudir:`attention`, :dudir:`caution`, :dudir:`danger`,
  :dudir:`error`, :dudir:`hint`, :dudir:`important`, :dudir:`note`,
  :dudir:`tip`, :dudir:`warning` 以及 :dudir:`admonition`。

* 图片:

  - :dudir:`image` (请见下面的 Images_ )
  - :dudir:`figure` (带有标题和可选的图例的图片)

* 其它内容元素:

  - :dudir:`contents <table-of-contents>` （一个局部的，即只对当前文件的，内容表）
  - :dudir:`container` （具有特定类的容器，用于HTML生成 ``<div>`` ）
  - :dudir:`rubric` (一个与文件章节无关的标题)
  - :dudir:`topic`, :dudir:`sidebar` (特别强调了内容元素)
  - :dudir:`parsed-literal` (支持行内标记的文字块)
  - :dudir:`epigraph` (带有属性行的块引用)
  - :dudir:`highlights`, :dudir:`pull-quote` （带自己的类属性的块引用）
  - :dudir:`compound` (组合段落)

* 特色表格:

  - :dudir:`table` （带标题的表格）
  - :dudir:`csv-table` （由逗号分开的值生成的表格）
  - :dudir:`list-table` （由一系列列表生成的表格）

* 特色指令（标识符）:

  - :dudir:`raw` （包括原生格式标记）
  - :dudir:`include` (包含其他文件的reStructuredText)
    -- 在Sphinx中，当给定一个绝对的文件路径，该指令（标识符）将其作为相对于源目录来处理 
  - :dudir:`class` (class属性赋给下一个元素) [1]_

* HTML特性:

  - :dudir:`meta` (生成HTML ``<meta>`` 标签)
  - :dudir:`title` (覆盖文件的标题)

* Influencing markup:

  - :dudir:`default-role` (设置一个新的默认role)
  - :dudir:`role` (创建一个新的role)

请 *不要* 使用指令（标识符） :dudir:`sectnum`， :dudir:`header` 以及
:dudir:`footer`。

Sphinx自己增加的指令（标识符）是在 :ref:`sphinxmarkup` 中描述的。

基本上，指令（标识符）由一个名称，参数，选项和内容组成。（请记住这些术语，它被用来在接下来的章节描述了自定义指令或者标识符。）请看例子，::

   .. function:: foo(x)
                 foo(y, z)
      :module: some.module.name

      Return a line of text input from the user.

``function`` 是指令（标识符）的名称。在这里它有两个参数，第一行其余的部分以及第二行，还有一个选项 ``module``
（正如可以看到的，选项是在参数的下一行以及以冒号开始以冒号结束）。选项必须跟指令的内容缩进到相同的水平。

指令（标识符）的内容与选项之间空一行，需要相对于指令（标识符）的首行缩进（以指令的首行为缩进的对照点）。


图片
------

reST支持图片指令（标识符）(:dudir:`ref <image>`)，像这样使用::

   .. image:: gnu.png
      (options)

在Sphinx中使用图片指令（标识符），文件名(这里是指 ``gnu.png``)必须是相对于源文件，或者是绝对的但是相对于顶部的源目录。例如，在 ``sketch/spam.rst`` 文件中可以使用图片 ``images/spam.png``，也可以使用 ``../images/spam.png`` 或者 ``/images/spam.png``。

Sphinx将会自动将图像文件拷贝到输出目录中（例如HTML格式输出，会拷贝到 ``_static`` 目录中。）

对于图片尺寸选项（ ``width`` 和 ``height``）的解释如下：如果大小没有单位或单位是像素，那图片大小将会被那些支持像素的输出格式关心（LaTeX格式就不在乎这种情况的图片大小）。HTML和LaTeX输出格式使用其他的单位（像 ``pt`` 表示像素点）。

Sphinx扩展了标准的docutils的功能，允许文件扩展名为星号::

   .. image:: gnu.*

Sphinx搜索所有的图片匹配提供的模式，并确定其类型。每个生成器会从所有的候选者中选择最佳的图片。比如，如果给出 ``gnu.*`` 这样的文件名以及源代码树中存在 :file:`gnu.pdf` 和 :file:`gnu.png` 这两个文件，LaTeX 生成器会选择前者，HTML生成器则会选择后者。

.. versionchanged:: 0.4
   增加了支持以星号结尾的文件名。

.. versionchanged:: 0.6
   图片的路径可以是绝对的。


脚注
---------

可以使用 ``[#name]_`` 标注在脚注的位置，在文档的最后的 ``.. rubric:: Footnotes`` 后添加脚注的内容，像这样::

   Lorem ipsum [#f1]_ dolor sit amet ... [#f2]_

   .. rubric:: Footnotes

   .. [#f1] Text of the first footnote.
   .. [#f2] Text of the second footnote.

你也可以明确用数字标注脚注或者通过不指定 ``name`` 使用自动数字标记脚注(``[#]_``)。


引文
---------

Sphinx支持标准reST引文(:duref:`ref <citations>`)，增加了所有引文是“全局的”的特性，即：所有的文件可以使用所有的引文。这样使用它们::

   Lorem ipsum [Ref]_ dolor sit amet.

   .. [Ref] Book or article reference, URL or whatever.

引文用法是类似的脚注的用法，但带标签不是数字，或以``#``开始。


替换
-------------

reST支持“替换”(:duref:`ref <substitution-definitions>`)，这是文本和/或标记在文中 ``|name|`` 提到。它们是像脚注用显著的标记块，像这样::

   .. |name| replace:: replacement *text*

或者，这样::

   .. |caution| image:: warning.png
                :alt: Warning!

细节请看 :duref:`reST reference for substitutions <substitution-definitions>`。

如果你想在所有文件使用中一些替换，把它们写入 :confval:`rst_prolog` 或把它们放到一个单独的文件，要使用它们的所有文件中包含它，通过使用 :rst:dir:`include` 指令或者标识符。（务必使得include文件扩展名与其他的源文件不同，以免让Sphinx把它作为一个独立的文件。）

Sphinx自定义了一些默认的替换, 请看 :ref:`default-substitutions`。


评论
--------

不是一个有效的标记结构（如上述的脚注）的每一个明确的标记块被视为一条评论（:duref:`ref <comments>`）。例如::

   .. This is a comment.

您可以缩进文本在注释开始后，这样可以形成多行注释::

   ..
      This whole indented block
      is a comment.

      Still in the comment.


源文件编码
---------------

由于包括特殊字符如在reST中的破折号或版权标志，最简单的方法是直接写为Unicode字符，指定编码。Sphinx假定源文件默认情况下是使用UTF-8编码；你可以改变 :confval:`source_encoding` 这一配置值。


陷阱
-------

这有些问题通常发生在编写reST文档的时候：

* **分离的内嵌标记:** 正如上面所说，行内标记的跨度必须用由非单词字符把周围的文字分开，可以使用转义的空格来避免。详情请看 `the reference
  <http://docutils.sf.net/docs/ref/rst/restructuredtext.html#inline-markup>`_。

* **没有嵌套内联标记:** 像 ``*see :func:`foo`*`` 是不可能存在的。


.. rubric:: Footnotes

.. [1] 当默认域包含一个 :rst:dir:`class` 指令（标识符），该指令将被隐藏。因此，Sphinx将它转为 :rst:dir:`rst-class`。
