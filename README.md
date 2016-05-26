## Lightning Extender
This is a proof of concept showing that a "sibling" profile can be used to extend the funtionality of the installed profile. In this case, "Lightning" is the Installed Profile, and Acme Lightning Extender is the Sibling Profile.

## Background
At it's core, this method uses patch #133 from [Make inherited install profiles load base profile modules/themes in correct order](https://www.drupal.org/node/1356276) to scan the `/profiles/contrib/acme_lightning_extender` directory for modules and config in addition to the Installed Profile's directory (`profiles/contrib/lightning`).

The main problems with this approach are:
* Requires writing to the $settings.php file
* Doesn't allow reading of the Sibling Profiles actual `.profile`, `.install`, or `info.yml` files (need to store that code in a module contained with the Sibling Profile)
* Doesn't allow customization of the install experience

## Description
Acme Lightning Extender is a Drupal Installation Profile that depends on the Lightning Distribution, which itself is an installation profile. Acme Lightning Extender does the following:

* Requires Lightning (via composer)
* Patches core to support sibling profiles
* Patches Lightning so that Lightning will install Acme Lightning Extender Core (which lives within) after installing Lightning
* Writes the path to itself under the `$settings['profile_directories']` array in `settings.php`
* Does some Proof Of Concept stuff like enable a different theme

In the end, you should have a site, build on Lightning, with some extra Out Of The Box configuration.

## Install
* Clone this repo
* From within the repo, run `composer install`
* Install Drupal as usual

