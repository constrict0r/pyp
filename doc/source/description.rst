Description
--------------------------------------------------------------

Ansible role to use as a wrapper for pip to install python packages.

This role performs the following actions:

- Ensure the requirements are installed.

- Ensure the current user can obtain administrative (root) permissions.

- Update the apt cache.

- Ensure dependencies are installed.

- If the **packages_pip** variable is defined, install the python packages
  listed on it.

- If the **configuration** variable is defined, install the python packages
  listed on it.