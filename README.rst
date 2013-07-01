Documentation repository. Look at the results `here <http://gateway4labs.readthedocs.org/en/latest/>`_.

How to build the documentation::

  $ pip install sphinx
  $ git clone https://github.com/gateway4labs/gateway4labs_doc.git
  $ cd gateway4labs_doc
  $ git submodule init
  $ git submodule update
  $ cd docs
  $ make html

And run your browser on build/html/index.html.
