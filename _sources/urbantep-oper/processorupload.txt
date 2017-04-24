Operational procedure for processor registration after upload
-------------------------------------------------------------

An expert user can upload a new processor to one of the processing centres using an automated upload script. Behind the scenes the actions are slightly different, and not fully automated. The upload script to the IT4I processing centre creates a ticket in behalf of the user. This ticket is necessary for the manual steps of WPS configuration and portal configuration. For the BC processing system the deployment of processors is fully automated, but the registration in the portal requires manual portal configuration the first time a (versioned) processor is deployed.

* The help desk operator is automatically informed about the new ticket. The operator forwards the ticket to the IT4I processing system operator and to the portal operator.
* The IT4I processing centre operator configures the new processor into the WPS configuration to make it available to the portal.
* For processors to be uploaded to the BC processing centre the portal configuration may already be initiated during the expert user registration if the processor is known at that time already.
* The Portal operator (see next operational procedure) configures a new processor into an existing application for the user, or it creates a new application. Initially, the processor is only accessible by the user.
* The help desk operator informs the user about the finalisation of the configuration.
