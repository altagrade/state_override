State Override
--------------

When implementing the move to configuration in core (CMI), some of the variables were found
to be not [actually configuration](https://api.backdropcms.org/change-records/statekey-value-storage-system-implemented),
and as such, they are stored in a special state storage system. Unlike configuration variables,
"state" variables are used for saving long-term values in the database that are environment-specific.
Examples of some "state" variables are:

    cron_key
    cron_last
    css_js_query_string
    install_task
    install_time
    maintenance_mode

While it is possible to override most configuration variables in the `settings.php` file using
[configuration overrides](https://api.backdropcms.org/change-records/any-config-value-can-be-overridden-via-settingsphp),
you cannot override "state" variables, module states, or role-based permissions directly.

This utility module enables you to override "state" variables, control the enabled or disabled
status of modules, and define role permissions in the same way configuration variables can be overridden
in the `settings.php` file. This is particularly useful for:

- Syncing databases between environments with different maintenance modes
- Enabling specific modules only in development environments
- Managing user role permissions for specific environments

### New Features

In addition to overriding "state" variables, **State Override** now includes the following capabilities:
- **Module State Control**: Enable or disable specific modules dynamically across environments.
- **Role Permissions Management**: Set or revoke role-based permissions based on your environment configuration.

Installation
------------

- Install and enable the State Override module using the official Backdrop CMS instructions at
  https://backdropcms.org/user-guide/modules;
- Alternatively, use [Bee](https://backdropcms.org/project/bee) to download,
  install, and enable it with a single CLI command: `brush -y en state_override`.

Usage
-----

Open the `settings.php` file and add your overrides like so:

```php
// Override state variables.
$config['state']['maintenance_mode'] = TRUE;
$config['state']['cron_key'] = 'w5AXKo9UdkoVRp9rT_0gqtdG2h322LGJ_sYuJN6aWpk1';

// Control module state (enable or disable).
$config['module']['devel'] = TRUE; // Enable 'Devel' module.
$config['module']['search_krumo'] = TRUE; // Enable 'Search Krumo' module.
$config['module']['nicemessages'] = FALSE; // Disable 'Nice Messages' module.

// Manage role permissions.
$config['role']['anonymous']['access devel information'] = TRUE; // Grant access devel information.
$config['role']['authenticated']['access devel information'] = TRUE; // Grant access devel information.
$config['role']['authenticated']['access content'] = TRUE; // Grant access content permission.
$config['role']['anonymous']['post comments'] = FALSE; // Revoke post comments permission.
```

Credits and current Maintainers
-------------------

- Created and maintained by [Alan Mels](https://github.com/alanmels)

License
-------

This project is GPL v3 software.
See the LICENSE.txt file in this directory for the complete text.
