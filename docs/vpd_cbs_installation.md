# VPD-CBS Tracker Installation Annex

Package Version 1.0
DHIS2 Version compatibility 2.34.1 and above

Demo:
[https://who-demos.dhis2.org/surveillance](https://who-demos.dhis2.org/surveillance)

## Overview

The VPD-CBS package was developed on DHIS2 2.34.1. In order to use the package, it is recommended that you install it into a DHIS2 instance using DHIS 2.34.1 or above. If you will be setting this up on a new instance, please refer to the [DHIS2 installation guide](#installation).

VPD-CBS package is self-contained, meaning it can be installed on its own. However, it is worth noticing that this package contains some metadata from the IDSR package. The reason for this is that there is a comparative table which makes it possible to compare the aggregated data and the tracker data. Thus, we recommend installing the IDSR package prior to this one, although it is not a mandatory requirement.

### Generic metadata

The package contains some metadata which is labeled as “generic”. It is likely that you have similar elements already in your database. These generic elements are used in some indicators and they are part of the IDSR package.

Data Elements used in CBS package

| Object                       | UID         | API endpoint                                                 |
|------------------------------|-------------|--------------------------------------------------------------|
| GEN - Population             | DkmMEcubiPv | `../api/dataElements.json?filter=name:like:GEN - Population` |
| GEN - Population < 15years   | cPLAnOTldta | `../api/dataElements.json?filter=name:like:GEN - Population` |
| GEN - Population live births | iKxybad85rv | `../api/dataElements.json?filter=name:like:GEN - Population` |
| GEN - Population weekly      | iLEkjJcYTJd | `../api/dataElements.json?filter=name:like:GEN - Population` |

Category options, categories, category Combos for ages

| Object             | UID         | API endpoint                                         |
|--------------------|-------------|------------------------------------------------------|
| 0-4 years          | UPvKbcqTEY3 | `../api/categoryOptions.json?filter=name:like:years` |
| 5+ years           | afpMrUgPzl3 | `../api/categoryOptions.json?filter=name:like:years` |
| Age (surveillance) | wAZr8Iv7S64 | `../api/categories.json?filter=name:like:Age`        |
| Age (surveillance) | eg8enaFY861 | `../api/categoryCombos.json?filter=name:like:Age`    |

### Predictors using Organisation Unit Level district

There are many predictors in the package which are using a placeholder for district Organisation Unit Level (OUL). The API endpoint for them would be: `../api/predictors?filter=organisationUnitLevels:!null`

The placeholder uses the label <OU_LEVEL_DISTRICT_UID>. Before attempting to import the package you need to replace this label with the UID of the equivalent OUL in your system.

### Sharing

There are three user groups that come with the package:

* CBS access
* CBS admin
* CBS 19 data capture

By default the following is assigned to these user groups

| Object              | User Groups                        |                                             |                                                |
|---------------------|------------------------------------|---------------------------------------------|------------------------------------------------|
|                     | CBS access                         | CBS admin                                   | CBS data capture                               |
| Tracked entity type | Metadata : can view <br> Data: can view | Metadata : can edit and view <br> Data: can view | Metadata : can view <br> Data: can capture and view |
| Program             | Metadata : can view <br> Data: can view | Metadata : can edit and view <br> Data: can view | Metadata : can view <br> Data: can capture and view |
| Program Stages      | Metadata : can view <br> Data: can view | Metadata : can edit and view <br> Data: can view | Metadata : can view <br> Data: can capture and view |
| Dashboards          | Metadata : can view <br> Data: can view | Metadata : can edit and view <br> Data: can view | Metadata : can view <br> Data: can view             |
