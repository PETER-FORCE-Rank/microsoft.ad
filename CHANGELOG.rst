================================================
Ansible Microsoft Active Directory Release Notes
================================================

.. contents:: Topics

v1.9.2
======

Release Summary
---------------

Release summary for v1.9.2

Bugfixes
--------

- microsoft.ad.object_info - Correctly return multivalued attributes with one entry as array with on item (instead of returning a string) - https://github.com/ansible-collections/microsoft.ad/issues/199

v1.9.1
======

Release Summary
---------------

Release summary for v1.9.1

Bugfixes
--------

- microsoft.ad.ldap - Ensure the encrypted LAPS value is marked as unsafe to stop unexpected templating of the raw JSON result value - https://github.com/ansible-collections/microsoft.ad/issues/194

v1.9.0
======

Release Summary
---------------

Release summary for v1.9.0

Minor Changes
-------------

- Set minimum supported Ansible version to 2.16 to align with the versions still supported by Ansible.

Bugfixes
--------

- ldap inventory - Fix up support for Ansible 2.19.

v1.8.1
======

Release Summary
---------------

Minor release for Galaxy/AH documention update

v1.8.0
======

Release Summary
---------------

Release summary for v1.8.0

Minor Changes
-------------

- Added support for Windows Server 2025
- domain - Added ``replication_source_dc`` to specify the domain controller to use as the replication source for the new domain - https://github.com/ansible-collections/microsoft.ad/issues/159
- domain_controller - Added ``replication_source_dc`` to specify the domain controller to use as the replication source for the new domain controller - https://github.com/ansible-collections/microsoft.ad/issues/159
- microsoft.ad.user - Added ``groups.permissions_failure_action`` to control the behaviour when failing to modify the user's groups - (https://github.com/ansible-collections/microsoft.ad/issues/140).

New Plugins
-----------

Filter
~~~~~~

- split_dn - Splits an LDAP DistinguishedName.

v1.7.1
======

Release Summary
---------------

Release summary for v1.7.1. Minor fix for broken action plugin docs

Bugfixes
--------

- Fix ``microsoft.ad.debug_ldap_client`` documentation problem so it appears in the ``ansible-doc`` plugin list and online documentation.

v1.7.0
======

Release Summary
---------------

Release summary for v1.7.0

Minor Changes
-------------

- Set minimum supported Ansible version to 2.15 to align with the versions still supported by Ansible.
- microsoft.ad.computer - Added the ``do_not_append_dollar_to_sam`` option which can create a computer account without the ``$`` suffix when an explicit ``sam_account_name`` was provided without one.
- microsoft.ad.domain - Added ``reboot_timeout`` option to control how long a reboot can go for.
- microsoft.ad.domain_child - Added ``reboot_timeout`` option to control how long a reboot can go for.
- microsoft.ad.domain_controller - Added ``reboot_timeout`` option to control how long a reboot can go for.
- microsoft.ad.membership - Added ``domain_server`` option to specify the DC to use for domain join operations - https://github.com/ansible-collections/microsoft.ad/issues/131#issuecomment-2201151651
- microsoft.ad.membership - Added ``reboot_timeout`` option to control how long a reboot can go for.

Bugfixes
--------

- Removed usages of the python call ``datetime.datetime.utcnow()`` in favour of ``datetime.datetime.now(datetime.timezone.utc)``. The original method is now deprecated in Python 3.12 and will be removed in a later version.
- group - fix error when creating a group with no members explicitly set - https://github.com/ansible-collections/microsoft.ad/issues/141
- ldap - Filter out managed service accounts in the default LDAP filter used. The ``filter_without_computer`` can be used to disable the default filter if needed.
- membership - allow domain join with hostname change if the account for that host already exists - https://github.com/ansible-collections/microsoft.ad/pull/145
- microsoft.ad.computer - Added fallback ``identity`` lookup for ``sAMAccountName`` with the ``$`` suffix. This ensures that finding the computer object will work with or without the ``$`` suffix. - https://github.com/ansible-collections/microsoft.ad/issues/124
- microsoft.ad.group - Fix setting group members of Builtin groups of a domain controller - https://github.com/ansible-collections/microsoft.ad/issues/130

New Modules
-----------

- service_account - Manage Active Directory service account objects

v1.6.0
======

Release Summary
---------------

Release summary for v1.6.0

Minor Changes
-------------

- microsoft.ad AD modules - Added ``domain_credentials`` as a common module option that can be used to specify credentials for specific AD servers.
- microsoft.ad AD modules - Added ``lookup_failure_action`` on all modules that can specify a list of distinguishedName values to control what should happen if the lookup fails.
- microsoft.ad.computer - Added the ability to lookup a distinguishedName on a specific domain server for ``delegates`` and ``managed_by``.
- microsoft.ad.group - Added the ability to lookup a distinguishedName on a specific domain server for ``managed_by`` and ``members``.
- microsoft.ad.ou - Added the ability to lookup a distinguishedName on a specific domain server for ``managed_by``.
- microsoft.ad.user - Added the ability to lookup a distinguishedName on a specific domain server for ``delegates``.
- microsoft.ad.user - Rename the option ``groups.missing_action`` to ``groups.lookup_failure_action`` to make the option more consistent with other modules. The ``missing_action`` option is still supported as an alias.
- microsoft.ad.user - Support group member lookup on alternative server using the DN lookup syntax. This syntax uses a dictionary where ``name`` defined the group to lookup and ``server`` defines the server to lookup the group on.

Bugfixes
--------

- microsoft.ad.membership - Fix hostname check to work with hostnames longer than 15 characters long - https://github.com/ansible-collections/microsoft.ad/issues/113
- microsoft.ad.user - Fix issue when creating a new user account with ``account_locked: false`` - https://github.com/ansible-collections/microsoft.ad/issues/108

v1.5.0
======

Release Summary
---------------

Release summary for v1.5.0

Minor Changes
-------------

- Added ``group/microsoft.ad.domain`` module defaults group for the ``computer``, ``group``, ``object_info``, ``object``, ``ou``, and ``user`` module. Users can use this defaults group to set common connection options for these modules such as the ``domain_server``, ``domain_username``, and ``domain_password`` options.
- Added support for Jinja2 templating in ldap inventory.

Bugfixes
--------

- microsoft.ad.group - Support membership lookup of groups that are longer than 20 characters long
- microsoft.ad.membership - Add helpful hint when the failure was due to a missing/invalid ``domain_ou_path`` - https://github.com/ansible-collections/microsoft.ad/issues/88

New Plugins
-----------

Filter
~~~~~~

- dn_escape - Escape an LDAP DistinguishedName value string.
- parse_dn - Parses an LDAP DistinguishedName string into an object.

v1.4.1
======

Release Summary
---------------

Release summary for v1.4.1

Bugfixes
--------

- debug_ldap_client - handle failures when attempting to get the krb5 context and default CCache rather than fail with a traceback

v1.4.0
======

Release Summary
---------------

Prepare for v1.4.0 release

Minor Changes
-------------

- Make ``name`` an optional parameter for the AD modules. Either ``name`` or ``identity`` needs to be set with their respective behaviours. If creating a new AD user and only ``identity`` is set, that will be the value used for the name of the object.
- Set minimum supported Ansible version to 2.14 to align with the versions still supported by Ansible.
- object_info - Add ActiveDirectory module import

v1.3.0
======

Release Summary
---------------

release summary for v1.3.0

Minor Changes
-------------

- AD objects will no longer be moved to the default AD path for their type if no ``path`` was specified. Use the value ``microsoft.ad.default_path`` to explicitly set the path to the default path if that behaviour is desired.
- microsoft.ad.ldap - Added the option ``filter_without_computer`` to not add the AND clause ``objectClass=computer`` to the final filter used - https://github.com/ansible-collections/microsoft.ad/issues/55

Bugfixes
--------

- Added the missing dependency ``dpapi-ng`` to Ansible Execution Environments requirements file for LAPS decryption support
- Ensure renaming and moving an object will be done with the ``domain_server`` and ``domain_username`` credentials specified - https://github.com/ansible-collections/microsoft.ad/issues/54
- Fix up ``protect_from_deletion`` when creating new AD objects - https://github.com/ansible-collections/microsoft.ad/issues/47
- Fix up date_time attribute comparisons to be idempotent - https://github.com/ansible-collections/microsoft.ad/issues/57
- microsoft.ad.user - Ensure the ``spn`` diff after key is ``spn`` and not ``kerberos_encryption_types``
- microsoft.ad.user - treat an expired account as a password that needs to be changed

v1.2.0
======

Release Summary
---------------

Release summary for v1.2.0

Minor Changes
-------------

- microsoft.ad.debug_ldap_client - Add ``dpapi_ng`` to list of packages checked
- microsoft.ad.ldap - Add support for decrypting LAPS encrypted password
- microsoft.ad.ldap - Allow setting LDAP connection and authentication options through environment variables - https://github.com/ansible-collections/microsoft.ad/issues/34

Deprecated Features
-------------------

- Deprecating support for Server 2012 and Server 2012 R2. These OS versions are reaching End of Life status from Microsoft and support for using them in Ansible are nearing its end.

Bugfixes
--------

- group - Fix idempotency check when ``scope: domainlocal`` is set - https://github.com/ansible-collections/microsoft.ad/issues/31
- microsoft.ad.group - ensure the ``scope`` and ``category`` values are checked as case insensitive to avoid changes when not needed - https://github.com/ansible-collections/microsoft.ad/issues/31

v1.1.0
======

Release Summary
---------------

This release includes the new ``microsoft.ad.ldap`` inventory plugin which can be used to generate an Ansible
inventory from an LDAP/AD source.

Bugfixes
--------

- microsoft.ad.user - Fix setting ``password_expired`` when creating a new user - https://github.com/ansible-collections/microsoft.ad/issues/25

New Plugins
-----------

Filter
~~~~~~

- as_datetime - Converts an LDAP value to a datetime string
- as_guid - Converts an LDAP value to a GUID string
- as_sid - Converts an LDAP value to a Security Identifier string

Inventory
~~~~~~~~~

- ldap - Inventory plugin for Active Directory

New Modules
-----------

- debug_ldap_client - Get host information for debugging LDAP connections

v1.0.0
======

Release Summary
---------------

This is the first release of the ``microsoft.ad`` Ansible collection which contains modules that can be used to managed a Microsoft Active Directory environment.
