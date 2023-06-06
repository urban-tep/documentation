# On-boarding

## Expert users

As soon as a new expert user is registered, the following procedures must be followed.

### Test my processor app

To allow the expert user to access the services under the Thematic Application **Test my processor**, the following actions must be performed:

- as admin user, on the control panel (wps provider view), create a new wps provider (where the user services are hosted) with the following settings:

  > - identifier = \<wpsidentifier>\_\<username> (e.g 'brockmann_eboissier')
  > - name = \<wpsidentifier> \<username> (e.g 'brockmann eboissier')
  > - url = url of the wps provider
  > - use proxy = true
  > - auto sync = true
  > - domain = user private domain

- the creation of the wps provider automatically add existing services with property *available* set to false, go to the control panel / wps services view and update availability of services linked to this new wps provider if necessary (as a sanity check, see that they have as domain the user private domain)

- if the wps services implements the quotation mode, update the accounting rates defined at the **wps provider** level

- when a new service is added on the wps provider, the agent running on the server will detect it and make it available for the user (available is automatically set to true)

- the user will then be able to see the service(s) in the Thematic Application **Test my processor**
