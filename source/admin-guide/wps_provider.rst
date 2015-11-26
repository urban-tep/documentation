WPS providers management
========================

| The WPS providers management page contains a list of all existing WPS providers in DB, with the possibility for an Administrator to *Create* a new WPS provider, *Update* or *Delete* an existing one.
| The Administrator can also *Update* a WPS provider (by clicking on |update|). This action will do a request to the WPS provider (GetCapabilities) to check weither there are new WPS services available. If so, these services will be automatically added to the list of existing WPS services in DB.

.. req:: TS-FUN-370
	:show:

	This section describes how a new WPS service is added by the administrator once accessible from the WPS provider.


.. |update| image:: ../includes/update.png
