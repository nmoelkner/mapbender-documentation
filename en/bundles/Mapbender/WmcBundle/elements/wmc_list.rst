.. _wmc_list:

WMC List
***********************

Mapbender can save and edit configurations with the WMC Editor. This configurations can be loaded with the element `WMC Loader <../elements/wmc_loader.html>`_.

You can add configurations from the selectbox to your application. 

**Notice:** that all configurations are pubic at the moment. Later in development we want to add access control to this module too.

**Notice:** that you need the element WMC Loader to use this functionality.


.. image:: ../../../../../figures/wmc_list.jpg
     :scale: 80


Configuration
=============

.. image:: ../../../../../figures/wmc_list_configuration.jpg
     :scale: 80


* **Title:** Title of the element. The title will be listed in "Layouts" and allows to distinguish between different buttons. It will be indicated if "Show label" is activated.
* **Tooltip:** text to use as tooltip.
* **Target:** Id of Map element to query.
* **Label:** add title as label in front of selectbox, default is false.

YAML-Definition:
----------------

.. code-block:: yaml

    title: WMC List         
    tooltip: WMC List           # text to use as tooltip
    target: wmcloader           # target to interact with, should be wmcloader
    label: true                 # add title as label in front of selectbox (default is false)


Class, Widget & Style
=====================

* **Class:** Mapbender\\WmcBundle\\Element\\WmcEditor
* **Widget:** <Put Widget name here>
* **Style:** <Put name of css file here>


HTTP Callbacks
==============


<action>
--------

Opens a dialog with an editor in which configurations can be saved and edited.


JavaScript API
==============


<function>
----------


JavaScript Signals
==================

<signal>
--------


