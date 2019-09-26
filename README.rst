.. _section-role-shibboleth:

Role **shibboleth**
================================================================================

Ansible role for managing Shibboleth SSO service.

* `Ansible Galaxy page <https://galaxy.ansible.com/honzamach/shibboleth>`__
* `GitHub repository <https://github.com/honzamach/ansible-role-shibboleth>`__
* `Travis CI page <https://travis-ci.org/honzamach/ansible-role-shibboleth>`__


Description
--------------------------------------------------------------------------------

This role will perform installation and configuration of Shibboleth SSO service
for `Apache2 <https://httpd.apache.org/>`__ webserver. It is particularly customized
to work within the `eduID <https://www.eduid.cz/en/index>`__ federation, so the
built-in template files are composed according to the relevant policies.

.. note::

    This role requires the :ref:`secure registry <section-overview-secure-registry>`
    feature. The account registry will be used to fill-in technical contacts into
    generated metadata.

    This role supports the :ref:`template customization <section-overview-customize-templates>`
    feature.


Dependencies
--------------------------------------------------------------------------------

This role is not dependent on any other role.

No other roles have direct dependency on this role.


Requirements
--------------------------------------------------------------------------------

This role does not have any special requirements.


Managed files
--------------------------------------------------------------------------------

This role directly manages content of following files on target system:

* ``/etc/shibboleth/shibboleth2.xml``
* ``/etc/shibboleth/attribute-map.xml``
* ``/etc/shibboleth/shibboleth_contact_template.xml``


Role variables
--------------------------------------------------------------------------------

There are following internal role variables defined in ``defaults/main.yml`` file,
that can be overriden and adjusted as needed:

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


Usage and customization
--------------------------------------------------------------------------------

This role is (attempted to be) written according to the `Ansible best practices <https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html>`__. The default implementation should fit most users,
however you may customize it by tweaking default variables and providing custom
templates.


Variable customizations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Most of the usefull variables are defined in ``defaults/main.yml`` file, so they
can be easily overridden almost from `anywhere <https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable>`__.


Template customizations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This roles uses *with_first_found* mechanism for all of its templates. If you do
not like anything about built-in template files you may provide your own custom
templates. For now please see the role tasks for list of all checked paths for
each of the template files.


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


Example Playbook
--------------------------------------------------------------------------------

Example content of inventory file ``inventory``::

    [servers_shibboleth]
    localhost

Example content of role playbook file ``playbook.yml``::

    - hosts: servers_shibboleth
      remote_user: root
      roles:
        - role: honzamach.shibboleth
      tags:
        - role-shibboleth

Example usage::

    ansible-playbook -i inventory playbook.yml
    ansible-playbook -i inventory playbook.yml --extra-vars '{"hm_shibboleth__download_metadata":true}'


License
--------------------------------------------------------------------------------

MIT


Author Information
--------------------------------------------------------------------------------

Jan Mach <jan.mach@cesnet.cz>, CESNET, a.l.e.
