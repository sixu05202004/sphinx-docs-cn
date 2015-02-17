.. _invocation:

sphinx-build 用法
==========================

:program:`sphinx-build` 脚本构建了一个 Sphinx 文档集。用法如下::

     $ sphinx-build [options] sourcedir builddir [filenames]

在这里，*sourcedir* 是指 :term:`源目录`，*builddir* 是指你想指定的生成文档的目录。大部分时候，是不需要指定 *filenames*。

:program:`sphinx-build` 脚本有如下的选项:

.. program:: sphinx-build

.. option:: -b buildername

   最重要的选项: 它选择生成器。常见的生成器如下：

   **html**
      生成HTML页面。这是默认生成器。

   **dirhtml**
      生成HTML页面，但是每个文件单独一个目录。如果 web 服务器提供服务，能够生成漂亮的 URLs(没有 ``.html`` 后缀)。

   **singlehtml**
      整个内容生成一个 HTML 页面。

   **htmlhelp**, **qthelp**, **devhelp**, **epub**
      生成 HTML 文件，包含了生成上述格式的文档集合的其他信息。

   **latex**
      生成可以被编译成 PDF 文件的 LaTeX 源文件通过使用 :program:`pdflatex`。

   **man**
      生成 UNIX 操作系统的 groff 格式的手册。

   **texinfo**
      生成 Texinfo 文件，它能够通过 :program:`makeinfo` 处理成 Info 文件。

   **text**
      生成纯文本文件。

   **gettext**
      生成 gettext 的风格的消息目录（``.pot`` 后缀的文件）。

   **doctest**
      如果 :mod:`~sphinx.ext.doctest` 激活，执行文件中所有的 doctests。

   **linkcheck**
      检查所有的外部链接的完整性。

   请参看 :ref:`builders`，里面列出了 Sphinx 自身附带的所有的生成器。用户可以添加自己的生成器扩展。

.. option:: -a

   如果给定，总是生成所有输出文件。默认是只生成新的和更改的源文件的输出文件。（这可能并不适用于所有的生成器。）

.. option:: -E
   
   不要使用已保存的 :term:`环境` （系统缓存所有交叉引用），会完全重新生成。默认是仅仅读取和解析自上次运行后新的或者已更新的源文件。

.. option:: -t tag

   定义标签 *tag*。这跟 :rst:dir:`only` 指令（标识符）关系密切，如果设置标签就会只包含 :rst:dir:`only` 指令（标识符）的内容。

   .. versionadded:: 0.6

.. option:: -d path

   因为 Sphinx 在生成输出文件之前，必须读取和解析所有的源文件，被解析过的源文件会被缓存为"doctree pickles"。通常，这些缓存文件会被放入于生成目录中的名为 :file:`.doctrees` 的文件夹里；使用该选项可以选择不同的缓存文件夹（所有生成器都可以共享 doctrees 文件夹）。

.. option:: -c path

   使用给定的配置文件目录，忽略源文件中的 :file:`conf.py` 配置文件。值得注意的是配置文件中的其他文件以及路径可能会跟配置文件目录有关，所以也必须使用指定的路径。

   .. versionadded:: 0.3

.. option:: -C
   
   不使用配置文件；使用 ``-D`` 选项后的配置值。

   .. versionadded:: 0.5

.. option:: -D setting=value

   覆盖配置文件 :file:`conf.py` 中一个配置值对。该值必须是一个字符串或者字典值。对于字典值，需要给吃键值对类似：``-D latex_elements.docclass=scrartcl``。对于布尔值，使用 ``0`` 或者 ``1``。

   .. versionchanged:: 0.6
      The value can now be a dictionary value.

.. option:: -A name=value

   在HTML模版中，把 *value* 赋给 *name* 。

   .. versionadded:: 0.5

.. option:: -n

   运行在严格模式。目前，这会对所有丢失的引用抛出警告。

.. option:: -N
   
   禁止带颜色的输出。（Windows下任何的带颜色的输出都是无效的。）

.. option:: -q

   不要在标准输出上输出任何东西，只给出标准错误的警告和错误。

.. option:: -Q

   不要在标准输出上输出任何东西，也包括警告。只有错误被写入标准错误。

.. option:: -w file

   输出除标准错误外的警告（和错误）到指定的文件。

.. option:: -W

   把警告转换成错误输出。这就说构建会在第一个警告的时候停止，``sphinx-build`` 会以错误状态1退出。

.. option:: -P

   （仅调试时有用。）构建时候，如果出现未处理的遗产，运行 python 调试器，:mod:`pdb`。


在命令行中，你可以在源目录以及生成目录后给出一个或者多个文件名。Sphinx 将会尝试构建给出的这些文件的输出（以及它们的依赖。） 


Makefile选项
----------------

由 :program:`sphinx-quickstart` 生成的 :file:`Makefile` 和 :file:`make.bat` 文件是只使用了 :program:`sphinx-build` 的 :option:`-b` 和 :option:`-d` 参数。 然而， 它们支持以下的变量（参数）来定制化：

.. describe:: PAPER

   :confval:`latex_paper_size` 的值。

.. describe:: SPHINXBUILD

   替代 ``sphinx-build`` 的命令。

.. describe:: BUILDDIR

   指定生成的目录，而不是使用在 :program:`sphinx-quickstart` 中选择的路径。

.. describe:: SPHINXOPTS

   :program:`sphinx-build` 的附加选项。


.. _invocation-apidoc:

调用sphinx-apidoc
===========================

:program:`sphinx-apidoc` 能够对一个 python 包生成完全的自动的API文档。调用它像这样::

     $ sphinx-apidoc [options] -o outputdir packagedir [pathnames]

*packagedir* 是指生成文档的包所在的路径， *outputdir* 生成的文档所存放的路径。任何给定的 *pathnames* 是在生成过程中需要忽略的路径名（[pathnames]里的东西在生成文档中是忽略的。）

:program:`sphinx-apidoc` 有如下些选项:

.. program:: sphinx-apidoc

.. option:: -o outputdir

   给出生成的文档所在的路径。

.. option:: -f, --force

   通常，sphinx-apidoc不会重新生成任何文件。使用这个选项强制重新生成所有的文件。

.. option:: -n, --dry-run
   
   使用这个选项的话，不会有任何文件生成。（空运行，或者称为干运行。）

.. option:: -s suffix

   这个选项指定了输出的文件的文件名后缀。默认情况下，后缀是 ``rst``。

.. option:: -d maxdepth

   如果存在内容表，设置内容表的最大深度。

.. option:: -T, --no-toc

   这可以防止生成的表的内容文件 ``modules.rst``。但是当 :option:`--full` 给出的时候，本选项就不起作用了。

.. option:: -F, --full

   此选项使得 sphinx-apidoc 创建一个完整的 Sphinx 项目，与 :program:`sphinx-quickstart` 使用同样的机制。大部分的配置值是设置成默认的值，但是你可以通过如下选项修改一些重要的配置值。

.. option:: -H project

   设置项目名称，使得生成到输出的文件 (请见 :confval:`project`).

.. option:: -A author

   设置作者名，使得生成到输出的文件 (请见 :confval:`copyright`).

.. option:: -V version

   设置项目版本，使得生成到输出的文件 (请见 :confval:`version`).

.. option:: -R release

   设置项目发布，使得生成到输出的文件 (请见 :confval:`release`).
