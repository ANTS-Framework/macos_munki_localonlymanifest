macos munki localonly manifest
==============================

[![Build Status](https://travis-ci.org/ANTS-Framework/macos_munki_localonlymanifest.svg?branch=master)](https://travis-ci.org/ANTS-Framework/macos_munki_localonlymanifest)

This role is used to manage the localonlymanifest feature of munki as described in
the [munki wiki](https://github.com/munki/munki/wiki/Preferences#localonlymanifest)

In order for this to work, munki has to be configured to use localonlymanifests.
Otherwise, munki will ignore the settings and delete the manifest.

If the localonly manifest changes, a file will be created at `/private/tmp/.com.googlecode.munki.updatecheck.launchd`
to activate an update check using `/Library/LaunchDaemons/com.googlecode.munki.managedsoftwareupdate-manualcheck.plist`

Requirements
------------
This role is useless withouth [munki](https://www.munki.org/munki).

Role Variables
--------------
```yml
# Install the template in this directory
macos_munki_localonlymanifest__path: "/Library/Managed Installs/manifests"
# Name of the template
macos_munki_localonlymanifest__template: "localonly_manifest"
# Name of the local file that will be generated on the client
macos_munki_localonlymanifest__name: "localonly_manifest"

# The variables written to munki's localonlymanifest are defined in the following tasks.
# They have to correspond to the software name in munki.
# To add support for new software, add a corresponding variable.
# To use these variables, define them in group_vars or host_vars. Undefined variables are ignored.

# Software that will be installed is defined in managed_installs_list.yml 
# Naming convention:
macos_munki_localonlymanifest__managed_installs_<software name>
# Software that will be installed is defined in managed_uninstalls_list.yml
# Naming convention:
macos_munki_localonlymanifest__managed_uninstalls_<software name>

# Generic placeholders macos_munki_localonlymanifest__managed_installs/uninstalls_other[01-10]
# have been provided to add custom software.
```

Example Playbook
----------------
```yml

# Clients that are in group_01 and group_02 will install Atom and Cyberduck
# and have Adium as managed uninstall.

- hosts: group_01
  vars:
    - macos_munki_localonlymanifest__managed_installs_atom: "Atom"
    - macos_munki_localonlymanifest__managed_uninstalls_adium: "Adium"
  roles:
  - role: macos_munki_localonlymanifest

- hosts: group_02
  vars:
    - macos_munki_localonlymanifest__managed_installs_cyberduck: "Cyberduck
  roles:
  - role: macos_munki_localonlymanifest
```

Notes
------
Ansible 2.4.0 will ship with it's own xml module.
(See this [github issue](https://github.com/ansible/ansible/pull/25323))
This role could be rewritten to take advantage of the native xml support.

License
-------

GPLv3

Author Information
------------------
Part of the [ANTS Framework](https://ants-framework.github.io/)
