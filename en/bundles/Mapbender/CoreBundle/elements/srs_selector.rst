.. _srs_selector:

Spatial Reference System Selector (SRS Selector)
********************************************************

The spatial reference system selector changes the map's spatial reference system.
Notice: The Selectbox offers the SRS that are defined for the `map element <../elements/map.html>`_.


.. image:: ../../../../../figures/de/srs_selector.jpg
     :scale: 100

Configuration
=============

.. image:: ../../../../../figures/srs_selector_configuration.jpg
     :scale: 80

* **Show label:** indicates the element.
* **Title:** Title of the element. The title will be listed in "Layouts" and allows to distinguish between different buttons. It will be indicated if "Show label" is activated.
* **Tooltip:** text to use as tooltip.
* **Target:** Id of Map element to query.

YAML-Definition:
----------------

.. code-block:: yaml

   tooltip: 'SRS Selector'  # text to use as tooltip
   label: false             # true/false to label the srs selector, default is false
   target: ~                # Id of Map element to query

Class, Widget & Style
=====================

* **Class:** Mapbender\\CoreBundle\\Element\\SrsSelector
* **Widget:** mapbender.element.srsselector.js
* **Style:** mapbender.elements.css

HTTP Callbacks
==============

None.

JavaScript API
==============

showHidde
---------
<>

selectSrs
----------
<>

getSelectedSrs
----------------
<>

isSrsSupported
----------------
<>

isSrsEnabled
----------------
<>

disableSrs
----------------
<>

enableSrs
----------------
<>

enableOnlySrs
--------------------
<>

getFullSrsObj
--------------------
<>

enableAllSrs
----------------
<>

disableAllSrs
----------------
<>

getInnerJoinSrs
----------------
<>

getInnerJoinArrays
----------------------
<>

JavaScript Signals
==================

None.
