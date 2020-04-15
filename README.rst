
pyp
***

.. image:: https://gitlab.com/constrict0r/pyp/badges/master/pipeline.svg
   :alt: pipeline

.. image:: https://travis-ci.com/constrict0r/pyp.svg
   :alt: travis

.. image:: https://readthedocs.org/projects/pyp/badge
   :alt: readthedocs

Ansible role to use as a wrapper for `pip
<https://pypi.org/project/pip/>`_ to install python packages.

.. image:: https://gitlab.com/constrict0r/img/raw/master/pyp/avatar.png
   :alt: avatar

Full documentation on `Readthedocs <https://pyp.readthedocs.io>`_.

Source code on:

`Github <https://github.com/constrict0r/pyp>`_.

`Gitlab <https://gitlab.com/constrict0r/pyp>`_.

`Part of: <https://gitlab.com/explore/projects?tag=doombot>`_

.. image:: https://gitlab.com/constrict0r/img/raw/master/pyp/doombot.png
   :alt: doombot

**Ingredients**

.. image:: https://gitlab.com/constrict0r/img/raw/master/pyp/ingredient.png
   :alt: ingredient


Contents
********

* `Description <#Description>`_
* `Usage <#Usage>`_
* `Variables <#Variables>`_
   * `packages_pip <#packages-pip>`_
   * `configuration <#configuration>`_
* `YAML <#YAML>`_
* `Requirements <#Requirements>`_
* `Compatibility <#Compatibility>`_
* `Limitations <#Limitations>`_
* `License <#License>`_
* `Links <#Links>`_
* `UML <#UML>`_
   * `Deployment <#deployment>`_
   * `Main <#main>`_
* `Author <#Author>`_

Description
***********

Ansible role to use as a wrapper for pip to install python packages.

This role performs the following actions:

* Ensure the requirements are installed.

* Ensure the current user can obtain administrative (root)
   permissions.

* Update the apt cache.

* Ensure dependencies are installed.

* If the **packages_pip** variable is defined, install the python
   packages listed on it.

* If the **configuration** variable is defined, install the python
   packages listed on it.



Usage
*****

* To install and execute:

..

   ::

      ansible-galaxy install constrict0r.pyp
      ansible localhost -m include_role -a name=constrict0r.pyp -K

* Passing variables:

..

   ::

      ansible localhost -m include_role -a name=constrict0r.pyp -K \
          -e "{packages_pip: ['bottle==0.12.17', 'whisper']}"

* To include the role on a playbook:

..

   ::

      - hosts: servers
        roles:
            - {role: constrict0r.pyp}

* To include the role as dependency on another role:

..

   ::

      dependencies:
        - role: constrict0r.pyp
          packages_pip: ['bottle==0.12.17', 'whisper']

* To use the role from tasks:

..

   ::

      - name: Execute role task.
        import_role:
          name: constrict0r.pyp
        vars:
          packages_pip: ['bottle==0.12.17', 'whisper']

To run tests:

::

   cd pyp
   chmod +x testme.sh
   ./testme.sh

On some tests you may need to use *sudo* to succeed.



Variables
*********

The following variables are supported:


packages_pip
============

List of packages to install via pip.

This list can be modified by passing a *packages_pip* array when
including the role on a playbook or via *–extra-vars* from a terminal.

If you want to install a specific package version, append the version
to the package name.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.pyp -K -e \
       "{packages_pip: ['bottle==0.12.17', 'whisper']}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.pyp
         packages_pip:
           - bottle==0.12.17
           - whisper

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{packages_pip: ['bottle==0.12.17', 'whisper']}"


configuration
=============

Absolute file path or URL to a *.yml* file that contains all or some
of the variables supported by this role.

It is recommended to use a *.yml* or *.yaml* extension for the
**configuration** file.

This variable is empty by default.

::

   # Using file path.
   ansible localhost -m include_role -a name=constrict0r.pyp -K -e \
       "configuration=/home/username/my-config.yml"

   # Using URL.
   ansible localhost -m include_role -a name=constrict0r.pyp -K -e \
       "configuration=https://my-url/my-config.yml"

To see how to write  a configuration file see the *YAML* file format
section.



YAML
****

When passing configuration files to this role as parameters, it’s
recommended to add a *.yml* or *.yaml* extension to the each file.

It is also recommended to add three dashes at the top of each file:

::

   ---

You can include in the file the variables required for your tasks:

::

   ---
   packages_pip:
     - ['bottle==0.12.17', 'whisper']

If you want this role to load list of items from files and URLs you
can set the **expand** variable to *true*:

::

   ---
   packages_pip: /home/username/my-config.yml

   expand: true

If the expand variable is *false*, any file path or URL found will be
treated like plain text.



Requirements
************

* `Ansible <https://www.ansible.com>`_ >= 2.8.

* `Jinja2 <https://palletsprojects.com/p/jinja/>`_.

* `Pip <https://pypi.org/project/pip/>`_.

* `Python <https://www.python.org/>`_.

* `PyYAML <https://pyyaml.org/>`_.

* `Requests <https://2.python-requests.org/en/master/>`_.

If you want to run the tests, you will also need:

* `Docker <https://www.docker.com/>`_.

* `Molecule <https://molecule.readthedocs.io/>`_.

* `Setuptools <https://pypi.org/project/setuptools/>`_.



Compatibility
*************

* `Debian Buster <https://wiki.debian.org/DebianBuster>`_.

* `Debian Raspbian <https://raspbian.org/>`_.

* `Debian Stretch <https://wiki.debian.org/DebianStretch>`_.

* `Ubuntu Xenial <http://releases.ubuntu.com/16.04/>`_.



Limitations
***********

* The packages are installed globally.



License
*******

MIT. See the LICENSE file for more details.



Links
*****

* `Github <https://github.com/constrict0r/pyp>`_.

* `Gitlab <https://gitlab.com/constrict0r/pyp>`_.

* `Gitlab CI <https://gitlab.com/constrict0r/pyp/pipelines>`_.

* `Readthedocs <https://pyp.readthedocs.io>`_.

* `Travis CI <https://travis-ci.com/constrict0r/pyp>`_.



UML
***


Deployment
==========

The full project structure is shown below:

.. image:: https://gitlab.com/constrict0r/img/raw/master/pyp/deploy.png
   :alt: deploy


Main
====

The project data flow is shown below:

.. image:: https://gitlab.com/constrict0r/img/raw/master/pyp/main.png
   :alt: main



Author
******

.. image:: https://gitlab.com/constrict0r/img/raw/master/pyp/author.png
   :alt: author

The Travelling Vaudeville Villain.

Enjoy!!!

.. image:: https://gitlab.com/constrict0r/img/raw/master/pyp/enjoy.png
   :alt: enjoy


