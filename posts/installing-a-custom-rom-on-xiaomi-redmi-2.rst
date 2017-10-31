.. title: Installing a custom ROM on Xiaomi Redmi 2
.. slug: installing-a-custom-rom-on-xiaomi-redmi-2
.. date: 2017-10-31 11:08:36 UTC+05:30
.. tags: android, redmi2
.. category: android
.. link: 
.. description: 
.. type: text

I've been installing and testing a lot of custom ROMs recently on my Redmi 2.
This is a brief tutorial describing all the steps involved in installing a
custom ROM (with specific steps required for Redmi 2).

**Before proceeding, make sure you have backed up all your important data to
another device.**

Custom Recovery
---------------

Most custom ROMs require a custom recovery. In this section, I will provide the
steps for installing the most popular recovery nowadays - `TWRP
<https://twrp.me>`_.

- First step is to install the *Android SDK platform tools* which include the
  ``fastboot`` command. ``fastboot`` is necessary for installing the custom
  recovery. You can get the platform tools for most OS `here
  <https://developer.android.com/studio/releases/platform-tools.html>`_. If you
  are on Ubuntu, there is a very `convenient package
  <https://packages.ubuntu.com/xenial/android-sdk-platform-tools>`_.

  If you have downloaded the platform tools manually, extract the archive to a
  directory of your choice, and open up your command line/terminal in the said
  directory.

- Switch off your phone, and enter fastboot mode by pressing the volume down
  button and power button simultaneously. Connect the phone to your computer
  using a USB cable.

  In your terminal, type ``fastboot devices`` to make sure your phone is being
  detected. The output of the command should list your device. If not, check your
  USB cable connection. If it is still not being detected, you may have a broken
  USB port on your phone or a broken USB cable.

- Download the TWRP image from `dl.twrp.me/wt88047/ <https://dl.twrp.me/wt88047/>`_. (Note
  that the image is for **wt88047** which includes the following models -
  **20148(11/17/18/19)**. I'm not sure if this image works on **wt86047
  (2014813)**. You can find an appropriate TWRP image on MIUI or XDA forums.
  Note down the path to where you have downloaded the image.) It will be
  convenient to copy it to your current working directory.

- Now, flash the recovery using the following command:

.. code:: bash

  fastboot flash recovery /path/to/twrp/image

- If you restart your phone now, MIUI may rewrite your recovery. Instead, you
  should reboot directly to your new recovery once before rebooting to MIUI.
  This can be done by

.. code:: bash

  fastboot boot /path/to/twrp/image

- That's it. You have successfully installed a custom recovery. You can now
  reboot into MIUI from the recovery.

Firmware
--------

- You have to ensure that your phone has the correct firmware version. Some
  (actually, most) ROMs require the Lollipop (Android 5.x) bootloader. If your
  MIUI is already on Lollipop, you can skip this section. If your MIUI is on
  Kitkat (Android 4.x) or lower, you need to flash the Lollipop bootloader. The
  requisite zip files can be found in the `Lineage OS thread at XDA
  <https://forum.xda-developers.com/showpost.php?p=70328051&postcount=3>`_ by
  *nicknitewolf*. I'm reproducing the links here - `wt88047
  <https://androidfilehost.com/?fid=673368273298919092>`_, `wt86047
  <https://androidfilehost.com/?fid=385035244224408045>`_.

- Copy the zip file onto your phone's SD card. Reboot to your custom recovery
  (Switch off your phone, and press volume up, volume down, and power buttons
  simultaneously). Choose the **Install** option which will take you to a file
  browser. Find the zip file you just copied and select it. In the next screen,
  confirm that you want to flash this file. That's it. You have successfully
  updated your firmware.

ROM
---

Whichever custom ROM you have chosen should have detailed installation
instructions. I will provide the *general* steps involved in flashing a new ROM
here.

- Download the zip file for the ROM, and get the appropriate Google apps
  (GApps) from `opengapps.org <http://opengapps.org/>`_. Copy both zip files to
  your phone's SD card. Reboot into recovery (power off, and press vol. up +
  vol. down + power).

- Choose the **Wipe** option in recovery. Choose the **Advanced wipe** option
  in the next screen. In the following screen, select **Dalvik/ART Cache,
  System, Data, and Cache**. Confirm that you want to wipe the selected
  partitions.

- Next, go back to the home screen of your recovery, and choose the **Install**
  option. In the file browser, find your **ROM zip** and confirm its
  installation. Once the installation is done, choose **Install** again, and
  select your **GApps zip** in the file browser. Wait for the installation to
  finish, and reboot. You should now be greeted by the boot animation of your
  new ROM.

- That's it. Enjoy your new ROM!

