.. _invocation:

sphinx-build用法
==========================

:program:`sphinx-build` 脚本构建了一个Sphinx文档集。用法如下::

     $ sphinx-build [options] sourcedir builddir [filenames]

在这里，*sourcedir*是指 :term:`源目录`，*builddir*是指你想指定的生成文档的目录。大部分时候，是不需要指定 *filenames*。

:program:`sphinx-build` 脚本有如下的选项:

.. program:: sphinx-build

.. option:: -b buildername

   最重要的选项: 它选择生成器。常见的生成器如下：

   **html**
      生成HTML页面。这是默认生成器。

   **dirhtml**
      生成HTML页面，但是每个文件单独一个目录。如果web服务器提供服务，能够生成漂亮的URLs(没有 ``.html``后缀)。

   **singlehtml**
      整个内容生成一个HTML页面。

   **htmlhelp**, **qthelp**, **devhelp**, **epub**
      生成HTML文件，包含了生成上述格式的文档集合的其他信息。

   **latex**
      生成可以被编译成PDF文件的LaTeX源文件通过使用 :program:`pdflatex`。

   **man**
      生成UNIX操作系统的groff格式的手册。

   **texinfo**
      生成Texinfo文件，它能够通过 :program:`makeinfo` 处理成 Info 文件。

   **text**
      生成纯文本文件。

   **gettext**
      生成gettext的风格的消息目录（``.pot`` 后缀的文件）。

   **doctest**
      如果 :mod:`~sphinx.ext.doctest` 激活，执行文件中所有的doctests。

   **linkcheck**
      检查所有的外部链接的完整性。

   请参看 :ref:`builders`，里面列出了Sphinx自身附带的所有的生成器。用户可以添加自己的生成器扩展。

.. option:: -a

   如果给定，总是生成所有输出文件。默认是只生成新的和更改的源文件的输出文件。（这可能并不适用于所有的生成器。）

.. option:: -E
   
   不要使用已保存的 :term:`环境`（系统缓存所有交叉引用），会完全重新生成。默认是仅仅读取和解析自上次运行后新的或者已更新的源文件。

.. option:: -t tag

   定义标签 *tag*。这跟 :rst:dir:`only` 指令（标识符）关系密切，如果设置标签就会只包含 :rst:dir:`only` 指令（标识符）的内容。

   .. versionadded:: 0.6

.. option:: -d path

   因为Sphinx在生成输出文件之前，必须读取和解析所有的源文件，被解析过的源文件会被缓存为"doctree pickles"。通常，这些缓存文件会被放入于生成目录中的名为 :file:`.doctrees` 的文件夹里；使用该选项可以选择不同的缓存文件夹（所有生成器都可以共享doctrees文件夹）。

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
   Write warnings (and errors) to the given file, in addition to standard error.

.. option:: -W

   把警告转换成错误输出。这就说构建会在第一个警告的时候停止，``sphinx-build`` 会以错误状态1退出。

.. option:: -P

   （仅调试时有用。）构建时候，如果出现未处理的遗产，运行python调试器，:mod:`pdb`。


在命令行中，你可以在源目录以及生成目录后给出一个或者多个文件名。Sphinx 将会尝试构建给出的这些文件的输出（以及它们的依赖。） 


Makefile选项
----------------

The :file:`Makefile` and :file:`make.bat` files created by
:program:`sphinx-quickstart` usually run :program:`sphinx-build` only with the
:option:`-b` and :option:`-d` options.  However, they support the following
variables to customize behavior:

.. describe:: PAPER

   The value for :confval:`latex_paper_size`.

.. describe:: SPHINXBUILD

   The command to use instead of ``sphinx-build``.

.. describe:: BUILDDIR

   The build directory to use instead of the one chosen in
   :program:`sphinx-quickstart`.

.. describe:: SPHINXOPTS

   Additional options for :program:`sphinx-build`.


.. _invocation-apidoc:

Invocation of sphinx-apidoc
===========================

The :program:`sphinx-apidoc` generates completely automatic API documentation
for a Python package.  It is called like this::

     $ sphinx-apidoc [options] -o outputdir packagedir [pathnames]

where *packagedir* is the path to the package to document, and *outputdir* is
the directory where the generated sources are placed.  Any *pathnames* given
are paths to be excluded ignored during generation.

The :program:`sphinx-apidoc` script has several options:

.. program:: sphinx-apidoc

.. option:: -o outputdir

   Gives the directory in which to place the generated output.

.. option:: -f, --force

   Normally, sphinx-apidoc does not overwrite any files.  Use this option to
   force the overwrite of all files that it generates.

.. option:: -n, --dry-run

   With this option given, no files will be written at all.

.. option:: -s suffix

   This option selects the file name suffix of output files.  By default, this
   is ``rst``.

.. option:: -d maxdepth

   This sets the maximum depth of the table of contents, if one is generated.

.. option:: -T, --no-toc

   This prevents the generation of a table-of-contents file ``modules.rst``.
   This has no effect when :option:`--full` is given.

.. option:: -F, --full

   This option makes sphinx-apidoc create a full Sphinx project, using the same
   mechanism as :program:`sphinx-quickstart`.  Most configuration values are set
   to default values, but you can influence the most important ones using the
   following options.

.. option:: -H project

   Sets the project name to put in generated files (see :confval:`project`).

.. option:: -A author

   Sets the author name(s) to put in generated files (see :confval:`copyright`).

.. option:: -V version

   Sets the project version to put in generated files (see :confval:`version`).

.. option:: -R release

   Sets the project release to put in generated files (see :confval:`release`).
