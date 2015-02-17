.. highlight:: rest

段落级标记
----------------------

.. index:: note, warning
           pair: changes; in version

这些指令（标识符）创建简短的段落，可用于内部信息的单位以及普通的文本：

.. rst:directive:: .. note::
   
   一个 API 特别重要的提示信息：用户需要注意当使用 API 的时候所涉及到的信息，指令（标识符）的内容应该写完整的句子，包括所有适当的标点符号。

   Example::

      .. note::

         This function is not suitable for sending spam e-mails.

.. rst:directive:: .. warning::

   一个 API 重要的提示信息：用户需要注意当使用 API 的时候所涉及到的警告信息。指令（标识符）的内容应该写完整的句子，包括所有适当的标点符号。这是不同于 :rst:dir:`note`，因为它更多的关注于有关安全的信息。 

.. rst:directive:: .. versionadded:: version

   本指令（标识符）记录项目的版本信息，把所描述的功能添加到库或 C API。当适用于整个模块，它应该被放置在模块部分的顶部之前。

   第一个参数必须给出，它是在问答中的版本号（使用 sphinx-quickstart 时候的问答），你可以添加第二个参数，包含一个 *简短* 的变化原因。

   Example::

      .. versionadded:: 2.5
         The *spam* parameter.

   需要注意的是指令（标识符）和解释之间是没有空行，这是为了让这些块在视觉上看起来像连续的标记。

.. rst:directive:: .. versionchanged:: version

   类似于 :rst:dir:`versionadded`，但是说明了何时和如何以某种方式改变命名特征（新参数，改变后的影响等等。）。

.. rst:directive:: .. deprecated:: version

   类似于 :rst:dir:`versionchanged`，但是说明了什么场合功能不推荐使用。解释可以这样给出::

      .. deprecated:: 3.1
         Use :func:`spam` instead.


--------------

.. rst:directive:: seealso

   许多章节包括了一系列的模块文件或外部文件的引用。这些列表是使用 :rst:dir:`seealso` 指令（标识符）创建的。

   :rst:dir:`seealso` 指令（标识符）通常是在任何子章节之前的位置。对于 HTML 格式输出，它一般远离文本的主要信息显示。

   :rst:dir:`seealso` 指令（标识符）的内容应该是一个 reST 定义列表。

   Example::

      .. seealso::

         Module :py:mod:`zipfile`
            Documentation of the :py:mod:`zipfile` standard module.

         `GNU tar manual, Basic Tar Format <http://link>`_
            Documentation for tar archive files, including GNU tar extensions.

   还有一种 “简短形式” 允许像这样的::

      .. seealso:: modules :py:mod:`zipfile`, :py:mod:`tarfile`

   .. versionadded:: 0.5
      简短形式。

.. rst:directive:: .. rubric:: title

   该指令（标识符）创建一个段落，标题，不使用节点创建一个表的内容。

   .. note::

      如果rubric的 *标题* 是“脚注”(或者是在所选择的语言中含义等价的)，LaTeX 会忽略它。因为它被假定为仅包含脚注的定义以及将创建一个空的标题。


.. rst:directive:: centered

   该指令（标识符）创建一个居中粗体显示的文本行。使用如下::

      .. centered:: LICENSE AGREEMENT


.. rst:directive:: hlist

   该指令（标识符）必须包含一个项目符号列表。根据生成器，通过分发多个项目的水平，或减少项目之间的间距，将它改造成一个更紧凑的列表。

   对于支持的水平分布的生成器，有一个 ``columns`` 选项，用于指定的列数，默认为2。示例::

      .. hlist::
         :columns: 3

         * A list of
         * short items
         * that should be
         * displayed
         * horizontally

   .. versionadded:: 0.6


内容表标记 
------------------------

:rst:dir:`toctree` 指令（标识符）是描述在 :ref:`toctree-directive` ，它生成子文件的内容表。

对于本地内容表，可以用标准的 reST :dudir:`contents directive
<table-of-contents>`。


词汇表
--------

.. rst:directive:: .. glossary::

   该指令（标识符）必须包含一个带有术语和定义的REST的类似定义列表的标记。定义将会被 :rst:role:`term` 引用。例如::

      .. glossary::

         environment
            A structure where information about all documents under the root is
            saved, and used for cross-referencing.  The environment is pickled
            after the parsing stage, so that successive runs only need to read
            and parse new and changed documents.

         source directory
            The directory which, including its subdirectories, contains all
            source files for one Sphinx project.

   相比正常定义列表，每个条目的 *多个* 术语是允许的，行内标记是允许出现在术语中。您可以链接到所有的术语。例如::

      .. glossary::

         term 1
         term 2
            Definition of both terms.

   (词汇​​表进行排序的时候，第一项确定排序的顺序。)

   .. versionadded:: 0.6
      你可以在 glossary 指令（标识符）中用  ``:sorted:`` ，它将按字母对条目进行排序。 

   .. versionchanged:: 1.1
      支持多术语以及术语中出现行内标记。


语法解释器
---------------------------

特殊标记可用于显示形式文法的(productions)。
Special markup is available for displaying the productions of a formal grammar.
The markup is simple and does not attempt to model all aspects of BNF (or any
derived forms), but provides enough to allow context-free grammars to be
displayed in a way that causes uses of a symbol to be rendered as hyperlinks to
the definition of the symbol.  There is this directive:

.. rst:directive:: .. productionlist:: [name]

   This directive is used to enclose a group of productions.  Each production is
   given on a single line and consists of a name, separated by a colon from the
   following definition.  If the definition spans multiple lines, each
   continuation line must begin with a colon placed at the same column as in the
   first line.

   The argument to :rst:dir:`productionlist` serves to distinguish different sets of
   production lists that belong to different grammars.

   Blank lines are not allowed within ``productionlist`` directive arguments.

   The definition can contain token names which are marked as interpreted text
   (e.g. ``sum ::= `integer` "+" `integer```) -- this generates cross-references
   to the productions of these tokens.  Outside of the production list, you can
   reference to token productions using :rst:role:`token`.

   Note that no further reST parsing is done in the production, so that you
   don't have to escape ``*`` or ``|`` characters.

下面是一个来自Python参考手册的例子::

   .. productionlist::
      try_stmt: try1_stmt | try2_stmt
      try1_stmt: "try" ":" `suite`
               : ("except" [`expression` ["," `target`]] ":" `suite`)+
               : ["else" ":" `suite`]
               : ["finally" ":" `suite`]
      try2_stmt: "try" ":" `suite`
               : "finally" ":" `suite`
