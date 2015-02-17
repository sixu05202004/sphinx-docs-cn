.. highlight:: rst

初尝 Sphinx
=======================

本文给出了 Sphinx 所有基本功能的快速教程。

绿色的箭头指定“详细信息”链接，这些链接指向了关于描述的功能的高级话题的章节。


设置文档来源
------------------------------------

一个文档集合的根目录被称为 :term:`源目录`。:term:`源目录` 包含 Sphinx 配置文件 :file:`conf.py`，在配置文件里面可以配置 Sphinx 如何读取源文件以及如何生成文件等等各方面。 [#]_

Sphinx 提供了一个脚本 :program:`sphinx-quickstart`，该脚本能够设置一个源目录以及通过几个简单的问答设置一个默认的配置文件 :file:`conf.py`。只需要运行::

   $ sphinx-quickstart

接着回答问题。（务必选择 "autodoc" 扩展。）

Sphinx 提供的 "API documentation" 生成器称为 :program:`sphinx-apidoc`；更详细的内容参看 :ref:`invocation-apidoc`。


定义文档结构
---------------------------

假设你已经执行了 :program:`sphinx-quickstart`。它创建了一个包含 :file:`conf.py` 以及主文件 :file:`index.rst`  （如果你接受了默认选项）的文件夹。:term:`master document` 的主要作用是一个欢迎页面以及包含了树状内容表的“根”（或者 *toctree*）。

连接多个文件到单个层次结构的文件的方式是 Sphinx 增强了 reStructuredText 的主要事情之一。

.. sidebar:: reStructuredText标识符（指令集）

   ``toctree`` 是 reStructuredText的一个 :dfn:`指令（标识符）`，一个很神奇的标记。指令（标识符）可以有参数，选项和内容。

   *参数* 是直接跟在指令（标识）后的双冒号后面。 每个指令决定是否可以有参数，以及有多少。 

   *选项* 是以一种“字段列表”形式跟随在参数后面。 ``maxdepth`` 就是 ``toctree`` 指令（标识符）的参数。

   *内容* 紧随着参数或者选项，不过两者（内容与参数（选项））之间需要空一行。每个指令决定是否允许内容，并用它做什么。

   **内容与选项的首行需要缩进到同样的位置。**。


toctree 指令（标识符）最初是空的，看起来像这样::

   .. toctree::
      :maxdepth: 2

你可以添加文档列表在指令（标识符）中的*内容*位置::

   .. toctree::
      :maxdepth: 2

      intro
      tutorial
      ...

上面就是包含 toctree 的文件实际的样子。被包含的文档是以 :term:`文件名`\ s 给出，简而言之，你可以脱离文件名扩展而直接使用斜线作为目录分隔符。

|more| 更详细的内容请见 :ref:`toctree 指令（标识符） <toctree-directive>`。

现在，您可以创建你列在 toctree 中的文件，并添加内容，章节的标题会被插入（至多到“最大深度”的层次）到 toctree 指令（标识符）标识的位置。当然，Sphinx 知道你的文件的顺序以及层级结构。（他们可能会包含 ``toctree`` 指令（标识符）本身，这意味着你可以创建深层嵌套的层次结构，如果必要的话。）


添加内容
--------------

在 Sphinx 的源文件中，你可以使用标准 reStructuredText 的大部分功能。Sphinx 也增加一些新的功能。例如，你可以通过使用可移植的方式（适应于所有的输出类型）-- :rst:role:`ref` 来实现跨文件间的引用。

举个例子，如果您正在查看的 HTML 版本，你可以看看这个文件的源代码 - 在侧边栏使用“显示源代码”的链接。

|more| 请参看 :ref:`rst-primer` 更加详细地学习 reStructuredText，可以访问 :ref:`sphinxmarkup` 了解 Sphinx 增加的标记（标识符）列表。


运行构建
-----------------

现在，你已经添加了一些文件和内容，让我们来做第一个文件构建。构建是由 :program:`sphinx-build` 程序开始的，像如下调用::

   $ sphinx-build -b html sourcedir builddir

上面提到的 *sourcedir* 是指 :term:`源目录`，*builddir* 是指你想放置的生成文件的位置。:option:`-b` 选择了生成器；在本例中 Sphinx 将会生成 HTML 格式的文件。

|more| :ref:`invocation` 中列出了 :program:`sphinx-build` 所支持的选项。

因为 :program:`sphinx-quickstart` 生成了 :file:`Makefile` 和 :file:`make.bat` 文件，这些文件能够减少不少工作：有了它们你就可以运行 ::

   $ make html

生成HTML文件在制定的目录。执行无参数的 ``make`` 可以看到哪些目标文件（ makefile 文件）可用。

.. admonition:: 怎样生成 PDF 文件?

   ``make latexpdf`` 运行 :mod:`LaTeX builder
   <sphinx.builders.latex.LaTeXBuilder>` ，实际上是调用 pdfTeX 工具元件。


文档对象
-------------------
注：在这里 domain 翻译成域，可以理解成不同的编程语言的集合对象，像python domain, java domain, C/C++ domain等。

Sphinx 一个主要目标是在任何 :dfn:`域` 中简单的 :dfn:`objects` 文档（从非常笼统的意义上说）。:dfn:`域` 是指一个集合对象类型属于一个整体，完整的标记来创建和引用这些对象的描述。

Python 是最突出的域。如果要记录 python 的内建函数 ``enumerate()``，你只需要添加如下的内容到源文件中::

   .. py:function:: enumerate(sequence[, start=0])

      Return an iterator that yields tuples of an index and an item of the
      *sequence*. (And so on.)

会呈现出（在文档中会显示）:

.. py:function:: enumerate(sequence[, start=0])

   Return an iterator that yields tuples of an index and an item of the
   *sequence*. (And so on.)

指令（标识符）的参数就是描述对象的 :dfn:`说明（签名）`，内容是它的文档。允许多个说明（签名），单独成行（每个独立一行）。

Python 是默认的域，所以不需要在域名前标记前缀::

   .. function:: enumerate(sequence[, start=0])

      ...

做了同样的工作如果你保持默认的域以及它默认的设置。

Sphinx 提供了许多其他的指令（标识符）为了标识 python 对象的其他的类型，例如：:rst:dir:`py:class` or :rst:dir:`py:method`。还设有一个为每个这些对象类型的交叉引用 :dfn:`角色`。 下面的内容会创建一个到 ``enumerate()`` 文档的链接::

   The :py:func:`enumerate` function can be used for ...

这就是结果: 链接到 :func:`enumerate`.

再次提醒，如果使用默认域，``py:`` 是可以不用添加的。不用关心真正包含 ``enumerate()`` 的文档的文件；Sphinx 能够找到以及为它建立链接。

每个域对说明（签名）样式有着特点的规定，并格式化输出显得漂亮些，或者增加些特性如链接到参数类型，像在 C/C++ 域。

|more| 请查看 :ref:`domains` 获取所有可用的域以及指令（标识符）/角色。


基本配置
-------------------

前面我们提到了 :file:`conf.py` 文件控制着Sphinx如何处理文档。该文件，作为Python源文件执行，你可以在文件中赋予的配置值。 对高级用户：因为文件是通过Sphinx执行，用户可以做一些不平凡的任务，像增加 :data:`sys.path` 的值或者导入一个模块找出记录文档的版本。

你可能需要修改的配置值是已经通过 :program:`sphinx-quickstart` 写入到 :file:`conf.py` 中并且注释起来（使用标准python语法： ``#`` 在行的开头）。如果要定制配置值而不是使用 :program:`sphinx-quickstart` 生成的值，只需要增加额外的赋值。

请记住，配置文件使用的是Python的字符串，数字，列表等语法。文件默认情况下是以UTF-8的格式保存，在文件的首行声明编码格式。如果需要使用non-ASCII格式，需要使用python的Unicode字符串*（像 ``project = u'Exposé'``）。

|more| 所有可用的配置值请参看 :ref:`build-config` 。


Autodoc
-------
注：无法找到合适的词语来表示 autodoc，直接用英文代替。

在记录 python 源代码的时候，通常需要在源文件，文档字符串中加入大量的记录（文字）。Sphinx 支持直接使用 python 自身模块的文档字符创通过使用称为 "autodoc" 的 :dfn:`extension`。（这个扩展是 python 的一个模块，为 Sphinx 项目提供额外的特性。） 

为了能够使用 autodoc，你需要通过在配置文件 :file:`conf.py` 中加入字符串 ``'sphinx.ext.autodoc'`` 到 :confval:`extensions` 列表中来激活。接着，你就有一些额外的指令（标识符）可以任由支配了。

例如，为了记录函数 ``io.open()``，从源文件中读取它的说明（签名）以及文档字符串，你可以这些写::

   .. autofunction:: io.open

当然你也能自动地记录整个类或者模块，使用自动的指令（标识符）的 member 选项，像::

   .. automodule:: io
      :members:

autodoc 需要导入模块以便提取文档字符串。因此，必须在配置文件 :file:`conf.py` 中添加模块所在的路径到 :py:data:`sys.path`。

|more| autodoc 更多的特性请参考 :mod:`sphinx.ext.autodoc`。


更多的内容
-------------------------

- 其它扩展 (math, intersphinx, viewcode, doctest)
- 静态文件
- 选择主题
- 模版
- 使用扩展
- 编写扩展


.. rubric:: Footnotes

.. [#] 这是最基本的结构（布局）。:file:`conf.py` 可以放在其他的文件夹， :term:`configuration directory`。请参看 
       :ref:`invocation`.

.. |more| image:: more.png
          :align: middle
          :alt: more info
