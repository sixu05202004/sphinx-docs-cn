.. _faq:

Sphinx FAQ
==========

这是一个 Sphinx 的常见问题列表。欢迎随时提出新的问题！

我该怎么做...
-----------------

... create PDF files without LaTeX?
   你可以使用版本 0.12 或者更高（ Sphinx 内置整合的） `rst2pdf <http://rst2pdf.googlecode.com>`_ 。详情请见 :ref:`builders`。

... get section numbers?
   在 LaTeX 输出中，它们是自动的；在 HTML 输出中，需要在 :rst:dir:`toctree` 指令（标识符）中添加选项 ``:numbered:``。

... customize the look of the built HTML files?
   使用主题，请参看 :doc:`theming`。

... add global substitutions or includes?
   请在 :confval:`rst_epilog` 配置中添加它们

... display the whole TOC tree in the sidebar?
   使用 :data:`toctree` 的调用在自定义布局模板，大概在 ``sidebartoc`` 块

... write my own extension?
   请参看 :ref:`extension tutorial <exttut>`。

... convert from my existing docs using MoinMoin markup?
   最简单的方法是将其转换为 XHTML，然后在转成 `xhtml to reST`_。你仍然需要标记类等，但标题和代码示例可以不用标记。


.. _usingwith:

使用 Sphinx 在...
--------------------

Read the Docs
    http://readthedocs.org 是一个基于 Sphinx 文档托管服务。他们主要服务于 sphinx 文档，同时支持其他的特性：版本控制，PDF 生成等等。 `Getting
    Started <http://read-the-docs.readthedocs.org/en/latest/getting_started.html>`_ 是最合适初学者文档。

Epydoc
   提供一个 `api role`_ 的第三方扩展，对于一个给定的标识符，它引用了 Epydoc 的 API 文档。

Doxygen
   Michael Jones 正在开发一个 reST/Sphinx 与 doxygen 的桥梁，称为 `breathe <http://github.com/michaeljones/breathe/tree/master>`_。

SCons
   Glenn Hutchings 写了一个使用 SCons 构建脚本生成 Sphinx 的文件；它存放在： https://bitbucket.org/zondo/sphinx-scons。

PyPI
   Jannis Leidel编写一个 `setuptools command
   <http://pypi.python.org/pypi/Sphinx-PyPI-upload>`_，它能够自动地上传 Sphinx 文档到 PyPI 包文档区域：http://packages.python.org/。

GitHub Pages
   默认情况下，使用下划线的目录将被忽略，这将会破坏 Sphinx 的静态文件。GitHub 的预处理为了支持 Sphinx HTML 输出能够 `disabled
   <https://github.com/blog/572-bypassing-jekyll-on-github-pages>`_ 。

MediaWiki
   参见 https://bitbucket.org/kevindunn/sphinx-wiki。

Google Analytics
   你可以定制化 ``layout.html`` 模版，像这样：

   .. code-block:: html+django

      {% extends "!layout.html" %}

      {%- block extrahead %}
      {{ super() }}
      <script type="text/javascript">
        var _gaq = _gaq || [];
        _gaq.push(['_setAccount', 'XXX account number XXX']);
        _gaq.push(['_trackPageview']);
      </script>
      {% endblock %}

      {% block footer %}
      {{ super() }}
      <div class="footer">This page uses <a href="http://analytics.google.com/">
      Google Analytics</a> to collect statistics. You can disable it by blocking
      the JavaScript coming from www.google-analytics.com.
      <script type="text/javascript">
        (function() {
          var ga = document.createElement('script');
          ga.src = ('https:' == document.location.protocol ?
                    'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
          ga.setAttribute('async', 'true');
          document.documentElement.firstChild.appendChild(ga);
        })();
      </script>
      </div>
      {% endblock %}


.. _api role: http://git.savannah.gnu.org/cgit/kenozooid.git/tree/doc/extapi.py
.. _xhtml to reST: http://docutils.sourceforge.net/sandbox/xhtml2rest/xhtml2rest.py


.. _epub-faq:

Epub 信息
---------

epub 生成器目前正处于测试阶段。仅仅完成与 Sphinx 文档本身的测试。如果你想要创建 epubs，下面是一些提示：

* 把文本分割到多个文件中。单个的 HTML 文件越长，ebook 阅读器处理的时间就越长。在极端情况下，阅读器需要花费一分钟来渲染。

* 应尽量减少的标记。这也花费的渲染时间。

* 对于一些阅读器，你可以使用内嵌或者外部的字体使用 CSS ``@font-face`` 指令（标识符）。
  这对于代码是 *极其* 有用，它们经常被右边缘给截断。默认的 Courier 字体是相当的宽，一行只能显示 60 个字符。如果你用一个更窄的字体来替代的话，一行能够显示更多的字符。
  你可能甚至使用  `FontForge <http://fontforge.sourceforge.net/>`_ 以及创建些免费字体的窄变体。以我的情况，一行能够显示 70 个字符。 

  您可能需要试验一下，直到你得到合理的结果。

* 测试所创建的 ePub 文件。可以有多种选择。我所知道的一种是 Epubcheck_, Calibre_, FBreader_ (虽然不支持CSS), 以及 Bookworm_。你可以下载
  http://code.google.com/p/threepress/，在自己的服务器上运行。

* 大型浮动的 div 显示不正确。如果覆盖多个页面，只显示在第一页的 div。
  这种情况，你可以从 ``sphinx/themes/epub/static/`` 拷贝 :file:`epub.css` 到你本地的 ``_static/``  目录，并且删除浮动设置。

* 在 ``toctree`` 指令（标识符）外的文件需要手动导入。有时候这也适用于附录，例如词汇表。你也可以添加它们在 :confval:`epub_post_files` 选项。

.. _Epubcheck: http://code.google.com/p/epubcheck/
.. _Calibre: http://calibre-ebook.com/
.. _FBreader: http://www.fbreader.org/
.. _Bookworm: http://bookworm.oreilly.com/


.. _texinfo-faq:

Texinfo 信息
------------

Texinfo 生成器目前处于试验阶段，但已成功地用于构建 Sphinx 和 Python 的文档。此生成器的设计用途是生成信息文件，然后将其加工成的 Texinfo。

有两个主要的程序读取信息的文件：``info`` 和GNU Emacs。``info`` 特点不多，但是适用大多数的 Unix 环境，并从终端可以快速访问。Emacs 提供了更好的字体和颜色显示，并支持广泛的定制（当然）。


注意事项
~~~~~~~~~~

如果你需要创建 Texinfo 文件，下面这些提示也许是有帮助的:

- 每个部分对应于不同节点。

- 冒号（``:``）不能正确被转义在菜单项和交叉引用中。它们将被用分号替换。

- 在 HTML 和 Tex 的输出，``see`` 会自动插入到所有的交叉引用的前面。

- 外部信息文件的链接可以使用的一些官方的URI方案 ``info``。例如:

     info:Texinfo#makeinfo_options

  将会:

     info:Texinfo#makeinfo_options

- 行内标记会显示如下信息:

  * strong -- \*strong\*
  * emphasis -- _emphasis_
  * literal -- \`literal'

  可以使用 Texinfo 命令行 ``@definfoenclose`` 来改变这种行为。例如，为了使行内标记更接近 reST，增加如下内容到 :file:`conf.py`::

     texinfo_elements = {'preamble': """\
     @definfoenclose strong,**,**
     @definfoenclose emph,*,*
     @definfoenclose code,`@w{}`,`@w{}`
     """}
