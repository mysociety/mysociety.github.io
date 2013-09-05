---
layout: page
title: Installation Standards (Draft)
---

<div class="panel">
This is a draft document. Suggestions for improvements and changes are welcome; just open a pull request with your proposed edits.
</div>

### Redeployable Code

Redeployable code is designed to be able to be picked up and installed by any interested third parties. Released code falls into one of the following groups, based on its ease of installability.

#### Lead

* The software can be installed, but it may require significant amounts of hand-holding, rely on undocumented configuration aspects, require significant domain knowledge etc.

#### Bronze

* The software has a fully documented installation process, which can be followed by anybody with reasonable technical and domain knowledge to build a working deployment.

#### Silver

* Bronze standard documentation, plus:
* Vagrant support: Cloning the repository, `cd` to the directory and `vagrant up` will result in a working development instance.
* There is an internationalization mechanism.

#### Gold

* Silver standard features, plus:
* A script, Puppet manifest or Chef cookbook (or combination of) which will provision and configure the server, install the code and result in a working (but not configured or fully provisioned) instance of the software.
* Comprehensive documentation on taking an unprovisioned production instance and bringing it up to production standard, for example instructions on:
  * Necessary external dependencies.
  * Importing data.

### SAAS Code

SAAS code is not intended to be generally redeployable by end users (although there is certainly nothing stopping them trying). This code is instead intended to be run by mySociety, with smaller instances being generated automatically.

SAAS code has no particular standards for installability, although it *should* be comprehensively documented and, for the sake of sanity, consider including features such as Vagrant support for ease of development.