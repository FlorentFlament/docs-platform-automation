---
title: Using Platform Automation for PCF
owner: PCF Platform Automation
---

This topic describes when and how to use Platform Automation for PCF,
and provides an example pipeline that uses Platform Automation for PCF tasks.

##Ops Manager vs Platform Automation for PCF

Ops Manager manages PCF operations manually. Platform Automation for PCF lets you automate them.

###Ops Manager

Ops Manager lets you install and configure PCF and PCF products manually.
Its UI takes you through the configuration decisions or changes that you need to make in situations such as:

* Installing PCF for the first time.

* Changing product configurations as a result of human decisions.

* Running major or minor version upgrades of PCF or PCF products.

###Platform Automation for PCF

You can run Platform Automation for PCF manually from a command line.
But you can also embed them in scripts and pipelines
to perform Ops Manager functions when human attention is not needed, such as:

* Upgrading products to new patch versions.
  - Configuration settings should not differ between successive patch versions within the same minor version line.
    Underlying properties or property names may change,
    but the tile's upgrade process automatically translates properties to the new fields and values.
  - Pivotal cannot guarantee the functionality of upgrade scripts in third-party PCF product tiles.

* Replicating configuration settings from one product tile to the same product tile on a different foundation.
- Because properties and property names can change between patch versions of a product,
  you can only safely apply configuration settings across product tiles if their versions exactly match.

###Ops Comparison

The following table compares how Ops Manager
and Platform Automation for PCF might run a typical sequence of PCF operations:

<table id='compare' border="1" class="nice" >
  <tr>
    <th></th>
    <th>Ops Manager</th>
    <th>Platform Automation for PCF</th>
  </tr><tr>
    <th>When to Use</th>
    <th>First install and minor upgrades</th>
    <th>Config changes and patch upgrades</th>
  </tr><tr>
    <th>1. Create Ops Manager VM</th>
    <td>Manually prepare IaaS and create Ops Manager VM</td>
    <td><code>create-vm</code></td>
  </tr><tr>
    <th>2. Configure Who Can Run Ops</th>
    <td>Manually configure internal UAA or external identity provider</td>
    <td><code>configure-authentication</code> or <code>configure-saml-authentication</code></td>
  </tr><tr>
    <th>3. Configure BOSH</th>
    <td>Manually configure BOSH Director</td>
    <td><code>configure-director</code> with settings saved from BOSH Director with same version</td>
  </tr><tr>
    <th>4. Add Products</th>
    <td>Click <strong>Import a Product</strong> to upload file, then <strong>+</strong> to add tile to Installation Dashboard</td>
    <td><code>upload-and-stage-product</code></td>
  </tr><tr>
    <th>5. Configure Products</th>
    <td>Manually configure product tiles</td>
    <td><code>configure-product</code> with settings saved from tiles with same version</td>
  </tr><tr>
    <th>6. Deploy Products</th>
    <td>Click <strong>Apply Changes</strong></td>
    <td><code>apply-changes</code></td>
  </tr>
</table>