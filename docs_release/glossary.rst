.. _glossary:

术语
========

.. glossary::

   builder（生成器）
      一个解析文档并执行对它们的操作的类（继承自 :class:`~sphinx.builders.Builder`）。通常，生成器把文档转换成输出的格式，不过，也能够使用生成器完成其他的事情：例如检查文档里的链接是否损坏，或者生成覆盖率信息。

      请看 :ref:`builders` 对Sphinx的内置的生成器有个更详细的了解。

   configuration directory（配置文件目录）
      包含 :file:`conf.py` 的目录。默认是与 :term:`source directory` 一样，但是能够通过命令行参数 **-c** 设置成不同的目录。 

   directive（指令或者标识符）
      允许以特定含义标记内容块的reStructuredText标记元素。指令（标识符）不仅仅对docutils模块有用，而且Sphinx以及扩展也能够添加自己的指令（标识符）。最基本的指令（标识符）的格式如下：

      .. sourcecode:: rst

         .. directivename:: argument ...
            :option: value

            指令（标识符）的内容。

      更加详细的信息请查看 :ref:`directives` 。

   document name（文件名）
      因为reST源文件可以有不同的扩展名（有的喜欢 ``.txt``，有的喜欢 ``.rst`` --扩展名能够通过 :confval:`source_suffix` 配置。），同样不同的操作系统有不同的路径分隔符，Sphinx能够转换分隔符：:dfn:`document names` 总是相对于 :term:`source directory`，文件扩展名被去除，路径分隔符被转换成斜线。所有的值，参数以及所谓为“文件”都要求这样的文件名。

      ``index``, ``library/zipfile``, 或者 ``reference/datamodel/types`` 就是文件名的例子。请注意，没有开头或结尾的斜线。

   domain（域）
      域是标记的集合（reStructuredText :term:`directive` 的以及 :term:`role` 的），它是为了描述和链接到 :term:`object` 的集合，比如程序语言的元素集。指令（标识符）以及角色（role）在域（domain）中的名称像 ``domain:name`` ，比如 ``py:function``。

      域（domain）的存在意味着不存在命名的问题当一堆文件需要引用的时候：例如C++和Python的类。这也意味着，全新的语言支持文件的扩展，更容易编写。关于域的更多的信息，请看章节 :ref:`domains`。

   environment（暂时找不到合适的词语来翻译）
      environment保存了根目录下的所有文件，用于交叉引用。它是在解析步骤后被使用，使连续运行只需要读取以及解析新的以及更新的文档。

   master document（主文件）
      包含根指令（标识符） :rst:dir:`toctree` 的文档。

   object（对象）
      Sphinx文档的基本构建块。每一个“对象指定（标识符）” (e.g. :rst:dir:`function` or :rst:dir:`object`)创建这样一个块；大多数的对象是能够交叉引用的。

   role（角色）
      允许标记的一段文字的reStructuredText标记元素。跟指令（标识符）一样，属于可扩展的。基本的格式像这样：``:rolename:content`` 。详细的内容请参看 :ref:`inlinemarkup` 。

   source directory（源目录）
      包含了一个Sphinx项目的所有源文件的目录以及它所有的子目录。
