.. title: How to flash MIUI Fastboot ROM from Linux
.. slug: how-to-flash-miui-fastboot-rom-from-linux
.. date: 2017-10-31 10:19:08 UTC+05:30
.. tags: android, linux, miui
.. category: android
.. link: 
.. description: 
.. type: text

- Download the ROM suitable for your device from the `MIUI
  site <http://en.miui.com/a-234.html>`_ and extract the downloaded archive

- Download and extract the `Android SDK Platform Tools
  <https://developer.android.com/studio/releases/platform-tools.html>`_

- Make sure ``adb`` and ``fastboot`` (components of platform-tools) are in your
  path

.. code:: bash

    $ export PATH=path/to/android/sdk/platform-tools:$PATH

- Connect your device to your computer using a USB cable and enable *USB
  Debugging* in your device's settings. Check if your device is detected.

.. code:: bash

    $ adb devices

- If device is listed, reboot to bootloader

.. code:: bash

    $ adb reboot bootloader

- Check if your device is detected by fastboot

.. code:: bash

    $ fastboot devices

- You may need to use ``sudo`` before ``fastboot`` if you get a permission denied
  error

- There are two scripts for flashing the ROM:

  1. ``flash_all.sh`` - Flash ROM and erase user data

  2. ``flash_all_except_data_storage.sh`` - Flash ROM without erasing user data

- Whichever script you decide to use, make sure that the interpreter is
  mentioned at the top of the script like

.. code:: bash

    #!/bin/sh

- If the above line is missing, add it to the top of the script

- Make the script executable (I've chosen ``flash_all.sh``)

.. code:: bash

    $ cd path/to/extracted/ROM/archive
    $ chmod a+x ./flash_all.sh

- Run the script

.. code:: bash

    $ ./flash_all.sh

- You may need to run ``sudo ./flash_all.sh`` if you had to use ``sudo`` with ``fastboot``

- Sit back and relax. The script needs no user interaction. After flashing the
  ROM, the scipt will reboot your device.

- Reboot will take quit a bit of time. Don't panic.

