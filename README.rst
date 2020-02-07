.. _section-role-shibboleth:

Role **shibboleth**
================================================================================

* `Ansible Galaxy page <https://galaxy.ansible.com/honzamach/shibboleth>`__
* `GitHub repository <https://github.com/honzamach/ansible-role-shibboleth>`__
* `Travis CI page <https://travis-ci.org/honzamach/ansible-role-shibboleth>`__

This role will perform installation and configuration of Shibboleth SSO service
for `Apache2 <https://httpd.apache.org/>`__ webserver. It is particularly customized
to work within the `eduID <https://www.eduid.cz/en/index>`__ federation, so the
built-in template files are composed according to the relevant policies.

**Table of Contents:**

* :ref:`section-role-shibboleth-installation`
* :ref:`section-role-shibboleth-dependencies`
* :ref:`section-role-shibboleth-usage`
* :ref:`section-role-shibboleth-variables`
* :ref:`section-role-shibboleth-files`
* :ref:`section-role-shibboleth-author`

This role is part of the `MSMS <https://github.com/honzamach/msms>`__ package.
Some common features are documented in its :ref:`manual <section-manual>`.


.. _section-role-shibboleth-installation:

Installation
--------------------------------------------------------------------------------

To install the role `honzamach.shibboleth <https://galaxy.ansible.com/honzamach/shibboleth>`__
from `Ansible Galaxy <https://galaxy.ansible.com/>`__ please use variation of
following command::

    ansible-galaxy install honzamach.shibboleth

To install the role directly from `GitHub <https://github.com>`__ by cloning the
`ansible-role-shibboleth <https://github.com/honzamach/ansible-role-shibboleth>`__
repository please use variation of following command::

    git clone https://github.com/honzamach/ansible-role-shibboleth.git honzamach.shibboleth

Currently the advantage of using direct Git cloning is the ability to easily update
the role when new version comes out.


.. _section-role-shibboleth-dependencies:

Dependencies
--------------------------------------------------------------------------------

This role is not dependent on any other role.

Following roles have direct dependency on this role:

* :ref:`alchemist <section-role-monitored>`
* :ref:`mentat_cesnet <section-role-monitored>`


.. _section-role-shibboleth-usage:

Usage
--------------------------------------------------------------------------------

Example content of inventory file ``inventory``::

    [servers_shibboleth]
    your-server

Example content of role playbook file ``role_playbook.yml``::

    - hosts: servers_shibboleth
      remote_user: root
      roles:
        - role: honzamach.shibboleth
      tags:
        - role-shibboleth

Example usage::

    # Run everything:
    ansible-playbook --ask-vault-pass --inventory inventory role_playbook.yml

    # Download locally service metadata:
    ansible-playbook --ask-vault-pass --inventory inventory role_playbook.yml --extra-vars '{"hm_shibboleth__download_metadata":true}'

It is recommended to follow these configuration principles:

* Create/edit file ``inventory/group_vars/all/vars.yml`` and within define some sensible
  defaults for all your managed servers. Example::

        hm_shibboleth__organization_name:
            en: CESNET
            cs: CESNET
        hm_shibboleth__organization_description:
            en: CESNET, NREN for Czech republic
            cs: CESNET, Síť národního výzkumu pro ČR
        hm_shibboleth__organization_url:
            en: http://www.ces.net/
            cs: http://www.cesnet.cz/
        hm_shibboleth__download_metadata: true

* Use files ``inventory/host_vars/[your-server]/vars.yml`` to customize settings
  for particular servers. Please see section :ref:`section-role-shibboleth-variables`
  for all available options. Example::

        hm_shibboleth__service_name:
            en: Mentat - HUB
            cs: Mentat - HUB
        hm_shibboleth__service_description:
            en: Main server for Mentat system.
            cs: Hlavní server pro systém Mentat.


.. _section-role-shibboleth-variables:

Configuration variables
--------------------------------------------------------------------------------


Internal role variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. envvar:: hm_shibboleth__service_name

    Name of the service in multiple localizations.

    * *Datatype:* ``dictionary of strings``
    * *Default:* ``{ "en": "Service name", "cs": "Název služby" }``

.. envvar:: hm_shibboleth__service_description

    Service description in multiple localizations.

    * *Datatype:* ``dictionary of strings``
    * *Default:* ``{ "en": "Service description", "cs": "Popis služby" }``

.. envvar:: hm_shibboleth__organization_name

    Name of the organization in multiple localizations.

    * *Datatype:* ``dictionary of strings``
    * *Default:* ``{ "en": "Organization, a.l.e.", "cs": "Organizace, z.s.p.o." }``

.. envvar:: hm_shibboleth__organization_description

    Organization description in multiple localizations.

    * *Datatype:* ``dictionary of strings``
    * *Default:* ``{ "en": "Organization description", "cs": "Popis organizace" }``

.. envvar:: hm_shibboleth__organization_url

    Organization URL in multiple localizations.

    * *Datatype:* ``dictionary of strings``
    * *Default:* ``{ "en": "http://en.organization.org", "cs": "http://cs.organization.org" }``

.. envvar:: hm_shibboleth__download_metadata

    Download Shibboleth metadata after configuring the service.

    * *Datatype:* ``boolean``
    * *Default:* ``false``


Foreign variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:envvar:`site_users`

    User database will be used to fill in contact information for service administrators.


Built-in Ansible variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:envvar:`group_names`

    List of group names current host is member of. This variable is used to resolve
    :ref:`soft role dependencies <section-overview-role-soft-dependencies>`.

:envvar:`ansible_lsb['codename']`

    Linux distribution codename. It is used for :ref:`template customizations <section-overview-role-customize-templates>`.


.. _section-role-shibboleth-files:

Managed files
--------------------------------------------------------------------------------

.. note::

    This role supports the :ref:`template customization <section-overview-role-customize-templates>` feature.

This role manages content of following files on target system:

* ``/etc/shibboleth/shibboleth2.xml`` *[TEMPLATE]*
* ``/etc/shibboleth/attribute-map.xml`` *[TEMPLATE]*
* ``/etc/shibboleth/shibboleth_contact_template.xml`` *[TEMPLATE]*


.. _section-role-shibboleth-author:

Author and license
--------------------------------------------------------------------------------

| *Copyright:* (C) since 2019 Jan Mach <jan.mach@cesnet.cz>, CESNET, a.l.e.
| *Author:* Jan Mach <jan.mach@cesnet.cz>, CESNET, a.l.e.
| Use of this role is governed by the MIT license, see LICENSE file.
|
