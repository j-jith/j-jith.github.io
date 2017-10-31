.. title: How to Compile and Install Vim 8.0 on Ubuntu
.. slug: how-to-compile-and-install-vim-80-on-ubuntu
.. date: 2017-10-31 10:40:07 UTC+05:30
.. tags: ubuntu, vim, linux
.. category: ubuntu
.. link: 
.. description: 
.. type: text

- Install build dependencies

.. code:: bash

    $ sudo apt-get build-dep vim

- Clone git repo

.. code:: bash

    $ git clone https://github.com/vim/vim.git``

- Change to src directory

.. code:: bash

    $ cd vim/src

- Remove files from previous compilation (skip if compiling for the first time)

.. code:: bash

    $ sudo make distclean

- Path to install vim (optional. omit --prefix option in next step if not set)

.. code:: bash

    export PREFIX='/path/to/vim/install'

- Configure with required options (``$ configure --help`` for other config.
  options).
  
  - For python 2.x

  .. code:: bash

     $ ./configure --with-features=huge \
                 --enable-multibyte \
                 --enable-rubyinterp \
                 --enable-pythoninterp \
                 --with-python-config-dir=/usr/lib/python2.7/config-x86\_64-linux-gnu \
                 --enable-perlinterp \
                 --enable-luainterp \
                 --enable-cscope \
                 --enable-gui=auto \
                 --enable-gtk2-check \
                 --with-x \
                 --with-compiledby="j.jith" \
                 --prefix=$PREFIX

  - For python 3.x

  .. code:: bash

      $ ./configure --with-features=huge \
                  --enable-multibyte \
                  --enable-rubyinterp \
                  --enable-python3interp \
                  --with-python3-config-dir=/usr/lib/python3.5/config-3.5m-x86_64-linux-gnu \
                  --enable-perlinterp \
                  --enable-luainterp \
                  --enable-cscope \
                  --enable-gui=auto \
                  --enable-gtk2-check \
                  --with-x \
                  --with-compiledby="j.jith" \
                  --prefix=$PREFIX

- Compile

.. code:: bash

    $ make

- Run tests

.. code:: bash

    $ make test

- Install (may need to use ``sudo`` if you don't have write permission in ``$PREFIX``)

.. code:: bash

    $ make install

- Make default editor/vim/vi/gvim

.. code:: bash

    $ sudo sh -c "update-alternatives --install /usr/bin/editor editor $PREFIX/bin/vim 1;
    update-alternatives --set editor $PREFIX/bin/vim;
    update-alternatives --install /usr/bin/vim vim $PREFIX/bin/vim 1;
    update-alternatives --set vim $PREFIX/bin/vim;
    update-alternatives --install /usr/bin/vi vi $PREFIX/bin/vim 1;
    update-alternatives --set vi $PREFIX/bin/vim;
    update-alternatives --install /usr/bin/gvim gvim $PREFIX/bin/gvim 1;
    update-alternatives --set gvim $PREFIX/bin/gvim"

