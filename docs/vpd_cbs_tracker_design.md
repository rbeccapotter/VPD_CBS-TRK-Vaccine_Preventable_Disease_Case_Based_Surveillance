# VPD Case-based Surveillance Tracker Design { #vpd-tracker-design }

## Introduction

The Vaccine Preventable Disease (VPD) Case Based Surveillance (CBS) system is designed to integrate the reporting of nine (9) vaccine-preventable diseases, link laboratory results with the case file, generate alerts, and facilitate analysis of case-basedd data alongside weekly reporting through the complementary aggregate IDSR package. The integrated VPD case-based system in DHIS2 has several advantages over traditionally centralized (national level) reporting into disease-specific forms:

1. Integrated system across diseases: All reported diseases being included in one place, rather than managing and merging different databases for entry, analysis and administration. This approach is more sustainable in most settings, as a single database can be managed across diseases. 
2. Increased timeliness through decentralized case-reporting: facilities can immediately report on a suspected case and laboratory users or users at higher levels can apend the laboratory results and final classification to the case file in DHIS2 as data becomes available at each level;
3. Improved access at district & facility levels: Allowing staff to remotely access details related to a case they are working on (ie. lab staff, clinical staff)
4. Reduced burden on upwards reporting: Allowing case reports captured in the national DHIS2 system to be syncronized to a regional platform through electronic data exchange, rather than through manual processes. 

For AFRO Member States, the package also serves as a replacement for centralized, offline reporting into the Epi-Info databse that has traditionally been used for submitting case reports to the Regional Office. Additional data exchange apps have been developed to facilitate pushing case reports from a country's DHIS2 instance to the AFRO regional surveillance platform (also using DHIS2). As such, data elements have been aligned to the standard VPD case reports used across the region. The package can be adapted to local needs and national guidelines; however any key elements that are required by the regional platform will be mandatory and should therefore not be modified.

For non-AFRO Member States, the package can be further modified to include/exclude diseases and data variables from the tracker program according to national policies on reportable and notifiable diseases. The overall tracker program design for linking case reporting with laboratory results and classification is flexible for national and regional modification.

### Acknowledgements
This package was developed according to standards-based content provided by and in close collaboration with the WHO World Health Emergencies Programme (WHE) and WHO Regional Office for Africa (AFRO). A global expert advisory group consisting of subject matter experts from WHO and US CDC was convened to develop requirements, provide feedback to the system design and ensure the package is designed to meet global standards for case-based surveillance of epidemic prone and vaccine-preventable diseases. HISP extends its gratitude to Gavi, the Vaccine Alliance for supporting the development of this package as a global good and its implementation at country level. 

## Diseases Covered

This package integrates reporting workflows for 9 different vaccine-preventable diseases within the same system. This is typically a more sustainable approach compared to having different systems or databases for each individual disease. The diseases covered in this package include:

1. Congenital Rubella Syndrome (CRS)
2. Invasive Bacterial Vaccine Preventable Disease (IBVPD)
3. Measles/Rubella
4. Meningitis
5. Neonatal Tetanus
6. Polio (Acute Flaccid Paralysis)
7. Rotavirus
8. Rotavirus Impact
9. Yellow Fever

The package design is *not* inherently limited to vaccine-preventable disease reporting;  it can be adapted and customized for country implementation to incorporate additional reporting of notifiable, reportable or other epidemic-prone diseases according to country policies. 

## Phases of Development

This use case is divided into 2 development phases as it relates to case based surveillance, with this document covering phase 1 of the initial scope of requirements. In broad terms, the phases are divided into the following

### Phase 1

* Use of DHIS2 to replace all current functionality and workflow of AFRO VPD surveillance EPI Info systems
* Phase out use of EPI Info in AFRO countries; implement DHIS2 as the EPI Info replacement

### Phase 2

* Strengthen response and management of public health actions through the support of local workflows, access control and functionality for identification and management of outbreaks directly within DHIS2
* Expand availability, guidance and implementation support for non-AFRO countries

## Program Description

All of the programs in the VPD-CBS package have a similar design, however different sections and variables are attached to each disease **_based on the initial diagnosis that is selected during registration_**. The sections attached to each program are described in the [System Design Summary](#system-design-summary) section of this document. For a full listing of the variables for each disease, please refer to the [surveillance data elements](https://drive.google.com/file/d/1IL2fRyBcVI5IP-cTrwQW9dEqry7RI5dz/view?usp=sharing) document. The program is made up of the following stages in its design:

1. Enrollment Details
2. Diagnostic & Clinical Information
3. Laboratory request
4. Specimen Tracking
5. Laboratory Result
6. Final Classification

Note that Neonatal Tetanus has a slightly different configuration, as it only includes the following stages in its design:

1. Enrollment Details
2. Diagnostic & Clinical Information
3. Final Classification

| Stage | Description |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enrollment details Attributes | The Tracked Entity is the case, which is represented by a Tracked Entity Type of ‘person.’ Cases are uniquely identified by the Disease specific Epid Number that is assigned to them. This number is a combination of their Epid Number and the disease identified during their initial diagnosis. Enrollment date = Date of notification Incident date = Date of symptoms onset Attributes include basic personal information and unique case identifiers. The attributes within this program include: System Generated Case ID Epid number First Name Last Name Date of birth Age (Years) Age (Months) Sex Home address Village/Neighbourhood Town/City District of residence Province of residence Telephone (local) Workplace/school physical address Facility contact number First name (parent or carer) Last name (parent or carer) Clinical diagnosis Disease specific Epid Number |
| Stage 1: Diagnostic & Clinical Information | This stage records a suspected case’s clinical details and admission information, signs and symptoms, vaccination history, notification information and outcome. |
| Stage 2: Lab Request [repeatable] | The lab request records details related to any specimens that are being sent to the lab for processing. The information provided here can help lab personnel prioritize lab tests when resources are limited. The person entering this data could be the same person who registered the suspected case and recorded the patient’s clinical exam and exposures; or may be other personnel charged with making lab requests. |
| Stage 3: Specimen Tracking [repeatable] | Specimen tracking records when lab specimen’s sent for processing were received at various lab levels. |
| Stage 4: Laboratory Result [repeatable] | The lab results stage records the specimen type and results from laboratory testing. It can be done directly at the lab or as secondary data entry. This stage is repeatable as samples for a given case may be tested multiple times (i.e. in the case of an inconclusive laboratory results, a new lab test can be conducted and results recorded) and/or multiple samples may also need to be processed. |
| Stage 5: Final Classification | The final classification records the final confirmed classification of the case as it relates to the initial diagnosis. |

## System Design Summary

The DHIS2 VPD-CBS digital data package metadata is based on reporting templates available for each disease within the EPI-Info application. A full list of variables used for data collection that are included in the package can be viewed in the [surveillance data elements](https://drive.google.com/file/d/1IL2fRyBcVI5IP-cTrwQW9dEqry7RI5dz/view?usp=sharing) document. In addition to the data collection components associated with this package, a number of outputs have been created and are described in more detail in the _**Dashboard Design Summary**_ section of this document.

In the development of this configuration package, an effort has been made to follow UiO’s [general design principles](https://who.dhis2.org/documentation/general_design_principles.html) and a common [naming convention](https://who.dhis2.org/documentation/naming_convention.html).

The VPD-CBS digital data package supports the collection of information based upon the initial clinical diagnosis that is selected. Each initial diagnosis has its own set of associated sections and variables that are displayed based upon the initial diagnosis that is selected. A listing of the program stages and program stage sections for each disease can be found in the subsequent tables within this section of the document. You can select a disease in order to be taken to its design details within the document.

1. [Congenital Rubella Syndrome (CRS)](#cbs_crs)
2. [Invasive Bacterial Vaccine Preventable Disease (IBVPD)](#cbs_ibvpd)
3. [Measles/Rubella](#cbs_measles_rubella)
4. [Meningitis](#cbs_meningitis)
5. [Neonatal Tetanus](#cbs_neonatal_tetanus)
6. [Polio (Acute Flaccid Paralysis)](#cbs_afppolio)
7. [Rotavirus](#cbs_rotavirus)
8. [Rotavirus Impact](#cbs_rotavirus_impact)
9. [Yellow Fever](#cbs_yellow_fever)


### CRS { #cbs_crs }

| Stage | Description |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enrollment details Attributes | The Tracked Entity is the case, which is represented by a Tracked Entity Type of ‘person.’ Cases are uniquely identified by the Disease specific Epid Number that is assigned to them. This number is a combination of their Epid Number and the disease identified during their initial diagnosis. Enrollment date = Date of notification Incident date = Date of symptoms onset Attributes include basic personal information and unique case identifiers. The attributes within this program include: System Generated Case ID Epid number First Name Last Name Date of birth Age (Years) Age (Months) Sex Home address Village/Neighbourhood Town/City District of residence Province of residence Telephone (local) Workplace/school physical address Facility contact number First name (parent or carer) Last name (parent or carer) Clinical diagnosis Disease specific Epid Number |
| Stage 1: Diagnostic & Clinical Information | This stage records a suspected case’s clinical details and admission information, signs and symptoms, vaccination history, notification information and outcome. |
| Stage 2: Lab Request [repeatable] | The lab request records details related to any specimens that are being sent to the lab for processing. The information provided here can help lab personnel prioritize lab tests when resources are limited. The person entering this data could be the same person who registered the suspected case and recorded the patient’s clinical exam and exposures; or may be other personnel charged with making lab requests. |
| Stage 3: Specimen Tracking [repeatable] | Specimen tracking records when lab specimen’s sent for processing were received at various lab levels. |
| Stage 4: Laboratory Result [repeatable] | The lab results stage records the specimen type and results from laboratory testing. It can be done directly at the lab or as secondary data entry. This stage is repeatable as samples for a given case may be tested multiple times (i.e. in the case of an inconclusive laboratory results, a new lab test can be conducted and results recorded) and/or multiple samples may also need to be processed. |
| Stage 5: Final Classification | The final classification records the final confirmed classification of the case as it relates to the initial diagnosis. |

### IBVPD { #cbs_ibvpd }

| Stage | Description |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enrollment details Attributes | The Tracked Entity is the case, which is represented by a Tracked Entity Type of ‘person.’ Cases are uniquely identified by the Disease specific Epid Number that is assigned to them. This number is a combination of their Epid Number and the disease identified during their initial diagnosis. Enrollment date = Date of notification Incident date = Date of symptoms onset Attributes include basic personal information and unique case identifiers. The attributes within this program include: System Generated Case ID Epid number First Name Last Name Date of birth Age (Years) Age (Months) Sex Home address Village/Neighbourhood Town/City District of residence Province of residence Telephone (local) Workplace/school physical address Facility contact number First name (parent or carer) Last name (parent or carer) Clinical diagnosis Disease specific Epid Number |
| Stage 1: Diagnostic & Clinical Information | This stage records a suspected case’s clinical details and admission information, signs and symptoms, vaccination history, notification information and outcome. |
| Stage 2: Lab Request [repeatable] | The lab request records details related to any specimens that are being sent to the lab for processing. The information provided here can help lab personnel prioritize lab tests when resources are limited. The person entering this data could be the same person who registered the suspected case and recorded the patient’s clinical exam and exposures; or may be other personnel charged with making lab requests. |
| Stage 3: Specimen Tracking [repeatable] | Specimen tracking records when lab specimen’s sent for processing were received at various lab levels. |
| Stage 4: Laboratory Result [repeatable] | The lab results stage records the specimen type and results from laboratory testing. It can be done directly at the lab or as secondary data entry. This stage is repeatable as samples for a given case may be tested multiple times (i.e. in the case of an inconclusive laboratory results, a new lab test can be conducted and results recorded) and/or multiple samples may also need to be processed. |
| Stage 5: Final Classification | The final classification records the final confirmed classification of the case as it relates to the initial diagnosis. |

### Measles/Rubella { #cbs_measles_rubella }

| Stage | Description |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enrollment details Attributes | The Tracked Entity is the case, which is represented by a Tracked Entity Type of ‘person.’ Cases are uniquely identified by the Disease specific Epid Number that is assigned to them. This number is a combination of their Epid Number and the disease identified during their initial diagnosis. Enrollment date = Date of notification Incident date = Date of symptoms onset Attributes include basic personal information and unique case identifiers. The attributes within this program include: System Generated Case ID Epid number First Name Last Name Date of birth Age (Years) Age (Months) Sex Home address Village/Neighbourhood Town/City District of residence Province of residence Telephone (local) Workplace/school physical address Facility contact number First name (parent or carer) Last name (parent or carer) Clinical diagnosis Disease specific Epid Number |
| Stage 1: Diagnostic & Clinical Information | This stage records a suspected case’s clinical details and admission information, signs and symptoms, vaccination history, notification information and outcome. |
| Stage 2: Lab Request [repeatable] | The lab request records details related to any specimens that are being sent to the lab for processing. The information provided here can help lab personnel prioritize lab tests when resources are limited. The person entering this data could be the same person who registered the suspected case and recorded the patient’s clinical exam and exposures; or may be other personnel charged with making lab requests. |
| Stage 3: Specimen Tracking [repeatable] | Specimen tracking records when lab specimen’s sent for processing were received at various lab levels. |
| Stage 4: Laboratory Result [repeatable] | The lab results stage records the specimen type and results from laboratory testing. It can be done directly at the lab or as secondary data entry. This stage is repeatable as samples for a given case may be tested multiple times (i.e. in the case of an inconclusive laboratory results, a new lab test can be conducted and results recorded) and/or multiple samples may also need to be processed. |
| Stage 5: Final Classification | The final classification records the final confirmed classification of the case as it relates to the initial diagnosis. |

### Meningitis { #cbs_meningitis }

| Stage | Description |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enrollment details Attributes | The Tracked Entity is the case, which is represented by a Tracked Entity Type of ‘person.’ Cases are uniquely identified by the Disease specific Epid Number that is assigned to them. This number is a combination of their Epid Number and the disease identified during their initial diagnosis. Enrollment date = Date of notification Incident date = Date of symptoms onset Attributes include basic personal information and unique case identifiers. The attributes within this program include: System Generated Case ID Epid number First Name Last Name Date of birth Age (Years) Age (Months) Sex Home address Village/Neighbourhood Town/City District of residence Province of residence Telephone (local) Workplace/school physical address Facility contact number First name (parent or carer) Last name (parent or carer) Clinical diagnosis Disease specific Epid Number |
| Stage 1: Diagnostic & Clinical Information | This stage records a suspected case’s clinical details and admission information, signs and symptoms, vaccination history, notification information and outcome. |
| Stage 2: Lab Request [repeatable] | The lab request records details related to any specimens that are being sent to the lab for processing. The information provided here can help lab personnel prioritize lab tests when resources are limited. The person entering this data could be the same person who registered the suspected case and recorded the patient’s clinical exam and exposures; or may be other personnel charged with making lab requests. |
| Stage 3: Specimen Tracking [repeatable] | Specimen tracking records when lab specimen’s sent for processing were received at various lab levels. |
| Stage 4: Laboratory Result [repeatable] | The lab results stage records the specimen type and results from laboratory testing. It can be done directly at the lab or as secondary data entry. This stage is repeatable as samples for a given case may be tested multiple times (i.e. in the case of an inconclusive laboratory results, a new lab test can be conducted and results recorded) and/or multiple samples may also need to be processed. |
| Stage 5: Final Classification | The final classification records the final confirmed classification of the case as it relates to the initial diagnosis. |

### Neonatal Tetanus { #cbs_neonatal_tetanus }

| Stage | Description |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enrollment details Attributes | The Tracked Entity is the case, which is represented by a Tracked Entity Type of ‘person.’ Cases are uniquely identified by the Disease specific Epid Number that is assigned to them. This number is a combination of their Epid Number and the disease identified during their initial diagnosis. Enrollment date = Date of notification Incident date = Date of symptoms onset Attributes include basic personal information and unique case identifiers. The attributes within this program include: System Generated Case ID Epid number First Name Last Name Date of birth Age (Years) Age (Months) Sex Home address Village/Neighbourhood Town/City District of residence Province of residence Telephone (local) Workplace/school physical address Facility contact number First name (parent or carer) Last name (parent or carer) Clinical diagnosis Disease specific Epid Number |
| Stage 1: Diagnostic & Clinical Information | This stage records a suspected case’s clinical details and admission information, signs and symptoms, vaccination history, notification information and outcome. |
| Stage 2: Lab Request [repeatable] | The lab request records details related to any specimens that are being sent to the lab for processing. The information provided here can help lab personnel prioritize lab tests when resources are limited. The person entering this data could be the same person who registered the suspected case and recorded the patient’s clinical exam and exposures; or may be other personnel charged with making lab requests. |
| Stage 3: Specimen Tracking [repeatable] | Specimen tracking records when lab specimen’s sent for processing were received at various lab levels. |
| Stage 4: Laboratory Result [repeatable] | The lab results stage records the specimen type and results from laboratory testing. It can be done directly at the lab or as secondary data entry. This stage is repeatable as samples for a given case may be tested multiple times (i.e. in the case of an inconclusive laboratory results, a new lab test can be conducted and results recorded) and/or multiple samples may also need to be processed. |
| Stage 5: Final Classification | The final classification records the final confirmed classification of the case as it relates to the initial diagnosis. |

### AFP/Polio { #cbs_afppolio }

| Stage | Description |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enrollment details Attributes | The Tracked Entity is the case, which is represented by a Tracked Entity Type of ‘person.’ Cases are uniquely identified by the Disease specific Epid Number that is assigned to them. This number is a combination of their Epid Number and the disease identified during their initial diagnosis. Enrollment date = Date of notification Incident date = Date of symptoms onset Attributes include basic personal information and unique case identifiers. The attributes within this program include: System Generated Case ID Epid number First Name Last Name Date of birth Age (Years) Age (Months) Sex Home address Village/Neighbourhood Town/City District of residence Province of residence Telephone (local) Workplace/school physical address Facility contact number First name (parent or carer) Last name (parent or carer) Clinical diagnosis Disease specific Epid Number |
| Stage 1: Diagnostic & Clinical Information | This stage records a suspected case’s clinical details and admission information, signs and symptoms, vaccination history, notification information and outcome. |
| Stage 2: Lab Request [repeatable] | The lab request records details related to any specimens that are being sent to the lab for processing. The information provided here can help lab personnel prioritize lab tests when resources are limited. The person entering this data could be the same person who registered the suspected case and recorded the patient’s clinical exam and exposures; or may be other personnel charged with making lab requests. |
| Stage 3: Specimen Tracking [repeatable] | Specimen tracking records when lab specimen’s sent for processing were received at various lab levels. |
| Stage 4: Laboratory Result [repeatable] | The lab results stage records the specimen type and results from laboratory testing. It can be done directly at the lab or as secondary data entry. This stage is repeatable as samples for a given case may be tested multiple times (i.e. in the case of an inconclusive laboratory results, a new lab test can be conducted and results recorded) and/or multiple samples may also need to be processed. |
| Stage 5: Final Classification | The final classification records the final confirmed classification of the case as it relates to the initial diagnosis. |

### Rotavirus { #cbs_rotavirus }

| Stage | Description |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enrollment details Attributes | The Tracked Entity is the case, which is represented by a Tracked Entity Type of ‘person.’ Cases are uniquely identified by the Disease specific Epid Number that is assigned to them. This number is a combination of their Epid Number and the disease identified during their initial diagnosis. Enrollment date = Date of notification Incident date = Date of symptoms onset Attributes include basic personal information and unique case identifiers. The attributes within this program include: System Generated Case ID Epid number First Name Last Name Date of birth Age (Years) Age (Months) Sex Home address Village/Neighbourhood Town/City District of residence Province of residence Telephone (local) Workplace/school physical address Facility contact number First name (parent or carer) Last name (parent or carer) Clinical diagnosis Disease specific Epid Number |
| Stage 1: Diagnostic & Clinical Information | This stage records a suspected case’s clinical details and admission information, signs and symptoms, vaccination history, notification information and outcome. |
| Stage 2: Lab Request [repeatable] | The lab request records details related to any specimens that are being sent to the lab for processing. The information provided here can help lab personnel prioritize lab tests when resources are limited. The person entering this data could be the same person who registered the suspected case and recorded the patient’s clinical exam and exposures; or may be other personnel charged with making lab requests. |
| Stage 3: Specimen Tracking [repeatable] | Specimen tracking records when lab specimen’s sent for processing were received at various lab levels. |
| Stage 4: Laboratory Result [repeatable] | The lab results stage records the specimen type and results from laboratory testing. It can be done directly at the lab or as secondary data entry. This stage is repeatable as samples for a given case may be tested multiple times (i.e. in the case of an inconclusive laboratory results, a new lab test can be conducted and results recorded) and/or multiple samples may also need to be processed. |
| Stage 5: Final Classification | The final classification records the final confirmed classification of the case as it relates to the initial diagnosis. |

### Rotavirus Impact { #cbs_rotavirus_impact }

| Stage | Description |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enrollment details Attributes | The Tracked Entity is the case, which is represented by a Tracked Entity Type of ‘person.’ Cases are uniquely identified by the Disease specific Epid Number that is assigned to them. This number is a combination of their Epid Number and the disease identified during their initial diagnosis. Enrollment date = Date of notification Incident date = Date of symptoms onset Attributes include basic personal information and unique case identifiers. The attributes within this program include: System Generated Case ID Epid number First Name Last Name Date of birth Age (Years) Age (Months) Sex Home address Village/Neighbourhood Town/City District of residence Province of residence Telephone (local) Workplace/school physical address Facility contact number First name (parent or carer) Last name (parent or carer) Clinical diagnosis Disease specific Epid Number |
| Stage 1: Diagnostic & Clinical Information | This stage records a suspected case’s clinical details and admission information, signs and symptoms, vaccination history, parents' interview, household items, notification information and outcome. |
| Stage 2: Lab Request [repeatable] | The lab request records details related to any specimens that are being sent to the lab for processing. The information provided here can help lab personnel prioritize lab tests when resources are limited. The person entering this data could be the same person who registered the suspected case and recorded the patient’s clinical exam and exposures; or may be other personnel charged with making lab requests. |
| Stage 3: Specimen Tracking [repeatable] | Specimen tracking records when lab specimen’s sent for processing were received at various lab levels. |
| Stage 4: Laboratory Result [repeatable] | The lab results stage records the specimen type and results from laboratory testing. It can be done directly at the lab or as secondary data entry. This stage is repeatable as samples for a given case may be tested multiple times (i.e. in the case of an inconclusive laboratory results, a new lab test can be conducted and results recorded) and/or multiple samples may also need to be processed. |
| Stage 5: Final Classification | The final classification records the final confirmed classification of the case as it relates to the initial diagnosis. |

### Yellow Fever { #cbs_yellow_fever }

| Stage | Description |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enrollment details Attributes | The Tracked Entity is the case, which is represented by a Tracked Entity Type of ‘person.’ Cases are uniquely identified by the Disease specific Epid Number that is assigned to them. This number is a combination of their Epid Number and the disease identified during their initial diagnosis. Enrollment date = Date of notification Incident date = Date of symptoms onset Attributes include basic personal information and unique case identifiers. The attributes within this program include: System Generated Case ID Epid number First Name Last Name Date of birth Age (Years) Age (Months) Sex Home address Village/Neighbourhood Town/City District of residence Province of residence Telephone (local) Workplace/school physical address Facility contact number First name (parent or carer) Last name (parent or carer) Clinical diagnosis Disease specific Epid Number |
| Stage 1: Diagnostic & Clinical Information | This stage records a suspected case’s clinical details and admission information, signs and symptoms, vaccination history, notification information and outcome. |
| Stage 2: Lab Request [repeatable] | The lab request records details related to any specimens that are being sent to the lab for processing. The information provided here can help lab personnel prioritize lab tests when resources are limited. The person entering this data could be the same person who registered the suspected case and recorded the patient’s clinical exam and exposures; or may be other personnel charged with making lab requests. |
| Stage 3: Specimen Tracking [repeatable] | Specimen tracking records when lab specimen’s sent for processing were received at various lab levels. |
| Stage 4: Laboratory Result [repeatable] | The lab results stage records the specimen type and results from laboratory testing. It can be done directly at the lab or as secondary data entry. This stage is repeatable as samples for a given case may be tested multiple times (i.e. in the case of an inconclusive laboratory results, a new lab test can be conducted and results recorded) and/or multiple samples may also need to be processed. |
| Stage 5: Final Classification | The final classification records the final confirmed classification of the case as it relates to the initial diagnosis. |

## Program Workflow

As phase 1 of development is intended as an EPI Info replacement, the workflow that is outlined here is not necessarily reflective of each of the individual interactions that may occur within a health system when capturing the data and managing information related to a particular case in field conditions. The workflow outlined below is therefore directly related to the processes resulting in a completed notification/reporting form being entered into DHIS2.

**_All diseases excluding Neonatal Tetanus_**

![workflow for all diseases](resources/images/workflow1.png)

**_Neonatal Tetanus_**

![workflow for neonatal tetanus](resources/images/workflow2.png)

## User Groups

The following user groups are included in the metadata package:

1. CBS admin -- intended for system admins to have metadata edit rights
2. CBS data capture -- intended for data entry staff to have access to capture data
3. CBS access -- intended for users such as analytics users who should be able to view the data, but not edit metadata or data.

Currently, only users assigned to the CBS data capture group will have access to capture data in the program. Please refer to the installation guidance for more instructions.

## Dashboards

Integrated dashboards for each disease have been created. Please select a link below for a description of the corresponding dashboard:

1. [Congenital Rubella Syndrome (CRS)](#cbs_crs)
2. [Invasive Bacterial Vaccine Preventable Disease (IBVPD)](#cbs_ibvpd)
3. [Measles/Rubella](#cbs_measlesrubella)
4. [Meningitis](#cbs_meningitis)
5. [Neonatal Tetanus](#cbs_neonatal_tetanus)
6. [Polio (Acute Flaccid Paralysis)](#cbs_afppolio)
7. [Rotavirus](#cbs_rotavirus)
8. [Rotavirus Impact](#cbs_rotavirus_impact)
9. [Yellow Fever](#cbs_yellow_fever)
10. Alerts/Outbreak
11. Comparative Analysis

## Program Rules

A complete list of program rules is inluded in the metadata reference file for the package, accessed at [dhis2.org/who-package-downloads](https://dhis2.org/who-package-downloads)

## Program Indicators

A complete list of 424 program indicators is inluded in the metadata reference file for the package, accessed at [dhis2.org/who-package-downloads](https://dhis2.org/who-package-downloads)
