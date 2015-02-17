.. highlight:: rst
.. _toctree-directive:

TOC 树
============

.. index:: pair: table of; contents

由于 reST 不便于多个文件相互关联或者分割文件到多个输出文件中，Sphinx 通过使用自定义的指令（标识符）来处理构成文档的单个文件的关系，这同样适用于内容表。``toctree`` 指令（标识符）就是核心要素。

.. note::

   使用 :dudir:`include` 指令（标识符）能够实现简单的一个文件在另一个文件的“包含”。

.. rst:directive:: toctree

   该指令（标识符）使用在指令（标识符）主体中给出的文件作为单个 TOCs(包含"sub-TOC树")，在当前位置插入一个"TOC树"。相对文件名 ​​（不以斜杠开始）是相对于指令（标识符）所在文件，绝对名称是相对于源目录。一个数字的 ``maxdepth`` 选项表示的树的深度 。默认情况下，所有级别是包含的。 [#]_

   仔细看看下面这个例子 (来自于的 Python 文档库参考页)::

      .. toctree::
         :maxdepth: 2

         intro
         strings
         datatypes
         numeric
         (many more documents listed here)

   这将会完成两件事情:

   * 所有这些文件的内容表被加入，最大的深度为2，这意味着一个嵌套标题。在这些文件中的 ``toctree`` 指令（标识符）也会被考虑到（识别）。
   * Sphinx 清楚文档  ``intro``，``strings`` 等等的顺序，当然也清楚它们是索引页的子页。通过这些信息能够生成“下一章”，“前一章”以及“主章节”的链接。

   **条目**

   在 :rst:dir:`toctree` 中的文件标题会自动从引用的文件中读取出来。如果这不是你想要的，你可以通过使用一个类似于 reST 超链接的语法（ :ref:`cross-referencing syntax <xref-syntax>` ）指定一个明确的标题和目标。这就像::

       .. toctree::

          intro
          All about strings <strings>
          datatypes

   上面的第二行，将链接到 ``strings`` 文件，但将使用的标题是 “All about strings”，而不是 ``strings`` 文件的标题。

   您还可以添加外部链接，使用一个 HTTP 地址，而不是一个文件名。

   **章节编号**

   如果你想要在 HTML 输出格式中有章节编号，可以在 rst:directive::toctree 中添加 ``numbered`` 选项。例如::

      .. toctree::
         :numbered:

         foo
         bar

   编号开始于 ``foo`` 的标题。Sub-toctrees 自动编号（不给Sub-toctrees ``numbered`` 的标志）。

   编号到一个特定的深度也是可以的，给予深度为一个参数: ``numbered`` 。

   **附加选项**

   如果你想仅显示在树中的文件的标题，而不是其他的同级别的标题，你可以用 ``titlesonly`` 选项::

      .. toctree::
         :titlesonly:

         foo
         bar
   
   你可以在 toctree 指令（标识符）中使用“匹配”，使用 ``glob`` 选项。所有的条目都将进行匹配而不是直接按照列出的条目，匹配的结果将会按照字母表顺序插入。例如::

      .. toctree::
         :glob:

         intro*
         recipe/*
         *
   
   这将首先包含文件名开始是 ``intro`` 的文件，接着包含 ``recipe`` 文件夹下所有的文件，最后是剩余的文件（显然，不包含主指令（标识符）的文件。） [#]_

   特殊的条目 ``self`` 表示包含 toctree 指令（标识符）的文件。如果想要从 toctree 生成 "sitemap" 的话，这是非常有用的。

   你也能使用“隐藏”选项，像这样::

      .. toctree::
         :hidden:

         doc_1
         doc_2

   这将仍然会告知 Sphinx 文档的层次结构，但是不会插入链接到指令（标识符）所在的文件--在不同风格或者 HTML 侧边栏，如果想要自己插入链接，这是非常有意义的。
   
   最后，所有在 :term:`源目录` （或者其子目录）必须出现在 ``toctree`` 中；如果发现文件不在 ``toctree`` 中，Sphinx 将会抛出警告，因为这意味着，通过标准的导航，这个文件将是不可到达的。使用 :confval:`unused_docs` 明确构建时候忽略的文件，使用 :confval:`exclude_trees` 明确构建时间忽略的目录。

   
   "主文件" ( :confval:`master_doc` )是 TOC 属结构的“根”。它能够被用于文件的主要页面，或者作为一个“完整的目录”如果你不给 ``maxdepth`` 的选项。

   .. versionchanged:: 0.3
      添加 "globbing" 选项。

   .. versionchanged:: 0.6
      添加选项 "numbered" 和 "hidden"，支持外部链接和 "self" 选项。

   .. versionchanged:: 1.0
      添加 "titlesonly" 选项。

   .. versionchanged:: 1.1
      添加编号选项参数 "numbered"。


特殊名称
-------------

Sphinx 保留了一些供自己使用的文件名，你不应该试图创建具有这些名称的文件 - 这将导致问题。

特殊的文件名（和他们生成的页面名）是：

* ``genindex``, ``modindex``, ``search``

  这些都是分别用于总索引，Python 模块索引，和搜索页。

  总索引用于模块和所有的生成索引 :ref:`object descriptions <basic-domain-markup>` 的条目，以及 :rst:dir:`index` 指令（标识符）。
  
  Python 模块索引包含了每一个 :rst:dir:`py:module` 指令（标识符）条目。

  搜索页包含一个生成的 JSON 搜索索引和 JavaScript 的形式，它使用全文搜索在生成的文件中搜索关键词，它应该兼容每一个主要的浏览器，支持最新的 JavaScript。

* 以 ``_`` 开头的名称

  尽管目前 Sphinx 只使用少数带 ``_`` 开头的名称，你应该不要创建这样的文件名或者目录名。


.. rubric:: Footnotes

.. [#] ``maxdepth`` 选项对 LaTeX 不起作用，内容始终是在文档的最前面，它的深度可以通过 ``tocdepth`` 来控制，你可以重设 :confval:`latex_preamble` 配置值。例如：  ``\setcounter{tocdepth}{2}``。

.. [#] 可用的匹配格式提示：你可以用标准的 shell 格式 ``*``, ``?``, ``[...]`` and ``[!...]``。 