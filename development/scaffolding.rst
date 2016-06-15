.. title:: Scaffolding

Scaffolding
===========

Virtual Machine
---------------

Most of the local development is done under a local Virtual Machine powered by `Vagrant`_, it uses
a basic LAMP stack that mimics the Staging and Live servers so every environment is similar to
minimize cross platform issues.

The VM's configuration can be downloaded from `Github`_ and with instructions on how to use it as
well.

.. _Vagrant: https://www.vagrantup.com/
.. _Github: https://github.com/jahvi/vagrant-vm

Module Generator
----------------

For Magento projects it's useful to be able to create custom modules quickly, the
`Magento Module Generator`_ powered by `Yeoman`_ is used to create the folder structure for Magento
extensions as well as intial configuration files that might be depended upon.

The geenrator can be installed from `npm`_ using the following commands:

.. code-block:: bash

    npm install -g yo
    npm install -g generator-magento-module

Then generate each extension with:

.. code-block:: bash

    yo magento-module

.. figure:: /_static/terminal.png
    :align: center

    Prompt screen of Magento Module Generator.

.. _Magento Module Generator: https://github.com/jahvi/generator-magento-module
.. _Yeoman: http://yeoman.io/
.. _npm: https://www.npmjs.com/
