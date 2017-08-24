macos munki localonly manifest
==============================

Description
-----------
This role is used to manage the localonlymanifest feature of munki as described in
the `munki wiki <https://github.com/munki/munki/wiki/Preferences#localonlymanifest>`_

If the localonly manifest changes, a file will be created at :code:`/private/tmp/.com.googlecode.munki.updatecheck.launchd`
to activate an update check using :code:`/Library/LaunchDaemons/com.googlecode.munki.managedsoftwareupdate-manualcheck.plist`

In order for this to work, munki has to be configured to use localonlymanifests.
Otherwise, munki will ignore the settings and delete the manifest.

Usage
------
The variables written to munki's localonlymanifest are defined in the following tasks:
* managed\_installs\_list.yml
* managed\_uninstalls\_list.yml

To add support for new software, add a corresponding variable to these two tasks.

To use these variables, define them in group\_vars or host\_vars. Undefined variables are ignored.

Generic placeholders :code:`macos_munki_localonlymanifest__managed_installs/uninstalls_other[01-10]`
have been provided to add custom software.

Notes
------
Ansible 2.4.0 will ship with it's own xml module.
(See this `github issue <https://github.com/ansible/ansible/pull/25323>`_)
This role could be rewritten to take advantage of the native xml support.
