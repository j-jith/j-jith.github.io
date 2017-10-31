.. title: Letting Spotlight find Brew Apps on Mac OS X
.. slug: letting-spotlight-find-brew-apps-on-mac-os-x
.. date: 2017-10-31 10:52:05 UTC+05:30
.. tags: mac, osx
.. category: misc
.. link: 
.. description: 
.. type: text

Say, you want spotlight to find MacVim. Doing

.. code:: bash

    $ brew linkapps macvim


creates a symlink in ``/Applications``. But Spotlight seems to ignore it. Instead, remove the symlink


.. code:: bash

    $ rm /Applications/MacVim.app


and do


.. code:: bash

    $ osascript -e 'tell application "Finder" to make alias file to POSIX file "/usr/local/opt/macvim/MacVim.app" at POSIX file "/Applications"'

