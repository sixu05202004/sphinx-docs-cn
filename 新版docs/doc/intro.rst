概述
============

这是 Sphinx 文档生成器的说明书，Sphinx 是一个工具，它能够把一组 reStructuredText_ 格式的文件转换成各种输出格式，而且自动地生成交叉引用，生成目录等。也就是说，如果有一个目录，里面包含一堆 reST 格式的文档（可能子目录里面也同样存在 reST 格式的文档），Sphinx 能够生成一个漂亮的组织结构以及便于浏览和导航的 HTML 文件（这些文件在其他的文件夹中）。当然对于同样的来源文件（reST 格式），它也能够生成一个能够被编译（生成）PDF 版本的 LaTeX 格式的文件，或者直接使用 `rst2pdf <http://rst2pdf.googlecode.com>`_ 生成 PDF 文件。

Sphinx 注重的是手写文档，而不是自动生成的 API 文档。尽管 Sphinx 或多或少地也支持自动生成的 API 文档，如果需要纯粹的 API 文档，可以看看 `Epydoc <http://epydoc.sf.net/>`_ （Epydoc 也支持 reST 格式）。

对于编写一个优秀的 “介绍” 文档，一般是 -- 为什么以及如何，请参看 `Write the docs <http://write-the-docs.readthedocs.org/>`_，由 Eric Holscher 撰写。


转换其他文件系统
-----------------

本节的目的是为给那些从其他文件系统迁移到 reStructuredText/Sphinx 上的人提供一些有用的提示。

* Gerard Flanagan 写了一个从纯 html 格式到 reST 格式的脚本；这个脚本能在
  `Python Package Index <http://pypi.python.org/pypi/html2rest>`_ 上被找到。

* 为了转换旧的 Python 文档到 Sphinx，“转换器”在 `the Python SVN repository
  <http://svn.python.org/projects/doctools/converter>`_ 上。它包含了从 python 文档形式的 LaTeX 标记到 Sphinx reST 的代码。

* Marcin Wojdyr 写了一个从 Docbook 到带有 Sphinx 标记的 reST；它位于 
  `Google Code <http://code.google.com/p/db2rst/>`_。

* Christophe de Vienne 写了一个从 Open/LibreOffice 文件到 Sphinx 的转换工具：
  `odt2sphinx <http://pypi.python.org/pypi/odt2sphinx/>`_。

* 为了转换不同的标记，`Pandoc <http://johnmacfarlane.net/pandoc/>`_
  是一个很有用的工具。


使用其他系统（工具）
----------------------

请参看 :ref:`faq`。


安装先决条件
-------------

* 对于 Python 2，需要   **Python 2.6** （或者以上版本）
* 对于 Python 3，需要  **Python 3.3** （或者以上版本）
* docutils_ （0.10 或者 部分 SVN 主干快照） 和  Jinja2_ 
* Pygments_ （如果需要代码高亮）

.. _reStructuredText: http://docutils.sf.net/rst.html
.. _docutils: http://docutils.sf.net/
.. _Jinja2: http://jinja.pocoo.org/
.. _Pygments: http://pygments.org/



如何使用 Sphinx
---------------

请参看 :doc:`tutorial`。:doc:`tutorial` 包含了手册里面很多高级的话题。

