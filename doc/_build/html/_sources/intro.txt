概述
============

这是Sphinx文档生成器的说明书，Sphinx是一个工具，它能够把一组 reStructuredText_ 格式的文件转换成各种输出格式，而且自动地生成交叉引用，生成目录等。也就是说，如果有一个目录，里面包含一堆reST格式的文档（可能子目录里面也同样存在reST格式的文档），Sphinx能够生成一个漂亮的组织结构以及便于浏览和导航的HTML 文件（这些文件在其他的文件夹中）。当然对于同样的来源文件（reST格式），它也能够生成一个能够被编译（生成）PDF版本的LaTeX格式的文件，或者直接使用 `rst2pdf <http://rst2pdf.googlecode.com>`_ 生成PDF文件。

Sphinx注重的是人工的文档，而不是自动生成的API文档。尽管Sphinx或多或少地也支持自动生成的API文档，如果需要纯粹的API文档，可以看看 `Epydoc <http://epydoc.sf.net/>`_ （Epydoc也支持reST格式）。


转换其他文件系统
-----------------------------

本节的目的是为给那些从其他文件系统迁移到reStructuredText/Sphinx上的人提供一些有用的提示。

* Gerard Flanagan写了一个从纯html格式到reST格式的脚本；这个脚本能在
  `Python Package Index <http://pypi.python.org/pypi/html2rest>`_ 上被找到。

* 为了转换旧的Python文档到Sphinx，“转换器”在 `the Python SVN repository
  <http://svn.python.org/projects/doctools/converter>`_ 上。它包含了从python文档形式的LaTeX标记到Sphinx reST的代码。

* Marcin Wojdyr写了一个从Docbook到带有Sphinx标记的reST；它位于 
  `Google Code <http://code.google.com/p/db2rst/>`_。

* Christophe de Vienne 写了一个从Open/LibreOffice文件到Sphinx的转换工具：
  `odt2sphinx <http://pypi.python.org/pypi/odt2sphinx/>`_。

* 为了转换不同的标记，`Pandoc <http://johnmacfarlane.net/pandoc/>`_
  是一个很有用的工具。


使用其他系统（工具）
----------------------

请参看 :ref:`faq`。


安装先决条件
-------------

* 对于Python 2，需要   **Python 2.4** （或者以上版本）
* 对于Python 3，需要  **Python 3.1** （或者以上版本）
* docutils_ （0.7或者SVN上的trunk版本） 和  Jinja2_ 
* Pygments_ （如果需要代码高亮）
* uuid_ （如果使用 **Python 2.4** ）

.. _reStructuredText: http://docutils.sf.net/rst.html
.. _docutils: http://docutils.sf.net/
.. _Jinja2: http://jinja.pocoo.org/
.. _Pygments: http://pygments.org/
.. The given homepage is only a directory listing so I'm using the pypi site.
.. _uuid: http://pypi.python.org/pypi/uuid/


如何使用Sphinx
-----

请参看 :doc:`tutorial`。:doc:`tutorial` 包含了手册里面很多高级的话题。

