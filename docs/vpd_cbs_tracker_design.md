# VPD Case-based Surveillance Tracker Design { #vpd-tracker-design }

## Introduction

The integrated Vaccine Preventable Disease (VPD) Case Based Surveillance (CBS) system is designed to facilitate reporting of nine (9) vaccine-preventable diseases in an electronic system, link laboratory results with the case file, generate automated alerts of possible diseease outbreaks based on thresholds, and facilitate analysis of case-based data alongside aggregated facility-based reporting to inform action. The integrated disease surveillance strategy has been adopted widely in recent decades to promote rational and efficient use of resources by streanlining common surveillance activities and functions ([WHO](https://apps.who.int/iris/bitstream/handle/10665/325015/WHO-AF-WHE-CPI-05.2019-eng.pdf)). An integrated information system design approach to case-based disease surveillance in DHIS2 capitalizes on the similarities of surveillance functions across different diseases such as case notification, sample collection, reporting, analysis and interpretation, feedback, and action -- often carried out in countries using the same structures, processes and personnel. The case-based package is designed to be implemented alongside the aggregate disease surveillance (IDSR) package for weekly/routine reporting of suspected cases and/or syndromes from health facilities on related vaccine-preventable and epidemic-prone diseases.

The integrated VPD case-based system in DHIS2 has several advantages over traditionally centralized (national level) reporting into disease-specific forms:
1. Integrated system across diseases: All reported diseases being included in one place, rather than managing and merging different databases for entry, analysis and administration. This approach is more sustainable in most settings, as a single database can be managed across diseases. 
2. Increased timeliness through decentralized case-reporting: facilities can immediately report on a suspected case and laboratory users or users at higher levels can apend the laboratory results and final classification to the case file in DHIS2 as data becomes available at each level.
3. Improved access at district & facility levels: Allows staff to remotely access details related to a case they are working on (ie. lab staff, clinical staff).
4. Reduced burden on upwards reporting: Enables case reports captured in the national DHIS2 system to be syncronized to a regional platform through electronic data exchange, rather than through manual processes. 

The VPD CBS package was developed in close collaboration with WHO Health Emergencies (WHE) programme and WHO Regional Office for Africa and is intended to strengthen recommendations for improving electronic disease surveillance systems as outlined in the [Technical Guidelines for Integrated Disease Surveillance and Response in the AFRO Region (2019)](https://apps.who.int/iris/bitstream/handle/10665/325015/WHO-AF-WHE-CPI-05.2019-eng.pdf). For AFRO Member States, the package also serves as a replacement for centralized, offline reporting into the Epi Info database that has traditionally been used for submitting case reports to the Regional Office. Additional data exchange apps have been developed to facilitate pushing case reports from a country's DHIS2 instance to the AFRO regional surveillance platform. As such, data elements have been aligned to the standard VPD case reports used across the region. The package can be adapted to local needs and national guidelines; however any key elements that are required by the regional platform will be mandatory and should therefore not be modified.

For non-AFRO Member States, the package can be further modified to include/exclude diseases and data variables from the tracker program according to national policies on reportable and notifiable diseases. The overall tracker program design for linking case reporting with laboratory results and classification is flexible for national and regional modification.

### Acknowledgements
This package was developed according to standards-based content provided by and in close collaboration with the WHO World Health Emergencies Programme (WHE) and WHO Regional Office for Africa (AFRO). A global expert advisory group consisting of subject matter experts from WHO and US CDC was convened to develop requirements, provide feedback to the system design and ensure the package is designed to meet global standards for case-based surveillance of epidemic prone and vaccine-preventable diseases. HISP extends its gratitude to Gavi, the Vaccine Alliance for supporting the development of this package as a global good and implementation efforts at country level. 

## System Design Overview

### Use case 
Surveillance is the ongoing systematic identification, collection, collation, analysis and interpretation of disease occurrence and public health event data, for the purposes of taking timely and robust action, such as disseminating the resulting information to the relevant people, for effective and appropriate action ([WHO](https://apps.who.int/iris/bitstream/handle/10665/325015/WHO-AF-WHE-CPI-05.2019-eng.pdf)). Surveillance is also essential for planning, implementation,
monitoring and evaluation of public health interventions. The DHIS2 VPD case-based surveillance package supports one approach to indicator-based surveillance, which is typically characterized as structured information, reported to public health officials mostly from formal sources such as health care providers, following a standardized format or set of indicator definitions ([WHO](https://apps.who.int/iris/bitstream/handle/10665/325015/WHO-AF-WHE-CPI-05.2019-eng.pdf), [US CDC](https://www.cdc.gov/globalhealth/healthprotection/gddopscenter/how.html#:~:text=Indicator%2Dbased%20surveillance%20involves%20reports,the%20information%20obtained%20is%20standardized)). Systematic reporting of suspected cases or notifiable conditions through indicator-based surveillance forms one key component of an early warning system. 

### Intended users
Through a collaborative process of working with implementing countries and surveillance stakeholders at multiple levels of the health system, the following have been identified as users or potential users of an integrated case-based surveillance system in DHIS2:  
* Health facility staff: facility staff are often the first to report a suspected case through existing passive surveillance systems according to national polivies on reportable diseases and conditions; facility staff may also be engaged in the follow-up of the case's medical care and outcome.
* District surveillance officers: surveillance officers at district or other sub-national administrative levels may be responsible for completing case investigations based on suspected case reports from facilities; following up case notifications and analyzing disease trends and outbreak alerts for their administrative area. 
* Public health staff: receive alerts for potential disease outbreaks generated by the system; analyze surveillance data for trends that may indicate possible disease outbreaks and plan response activities where appropriate. 
* Laboratory staff: receive electronic specimen request forms; may be involved in entering or uploading laboratory results to a longitudinal case record.

### Diseases Covered
This package integrates case-based reporting workflows for 9 different vaccine-preventable diseases within the same system. This is typically a more sustainable approach compared to having different systems or databases for each individual disease. Data variables per diseases have been configured as Data Elements and Tracked Antity Attributes in the DHIS2 tracker program according to a core list of [surveillance data elements](https://drive.google.com/file/d/1IL2fRyBcVI5IP-cTrwQW9dEqry7RI5dz/view?usp=sharing) provided by WHO Health Emergencies & the WHO Regional Office for Africa.

Standardized data variables are incorporated into the VPD case-based tracker program for the following diseases. You can select a disease in order to be taken to its design details within the document. 

1. [Congenital Rubella Syndrome (CRS)](#cbs_crs)
2. [Invasive Bacterial Vaccine Preventable Disease (IBVPD)](#cbs_ibvpd)
3. [Measles/Rubella](#cbs_measles_rubella)
4. [Meningitis](#cbs_meningitis)
5. [Neonatal Tetanus](#cbs_neonatal_tetanus)
6. [Polio (Acute Flaccid Paralysis)](#cbs_afppolio)
7. [Rotavirus](#cbs_rotavirus)
8. [Rotavirus Impact](#cbs_rotavirus_impact)
9. [Yellow Fever](#cbs_yellow_fever)

The package design is *not* inherently limited to vaccine-preventable disease reporting;  it can be adapted and customized for country implementation to incorporate additional reporting of notifiable, reportable or other epidemic-prone diseases according to country policies. 

### Conceptual Workflow
The VPD CBS tracker program supports the collection of information based upon the initial clinical diagnosis that is selected upon enrollment of a new suspected case. **Program rules** are used to show program stages and data variables according to the initial clinical diagnosis of a suspected disease. The conceptual workflow outlined here is not necessarily reflective of each of the individual interactions that may occur within a health system when capturing the data and managing information related to a particular case in field conditions. 

#### **Centralized reporting**
The workflow outlined below illustrates the processes resulting in all relevant case forms being entered into DHIS2 at a centralized level, based on multiple sources of data (e.g. clinical information captured at the facility, laboratory diagnosis, additional details that may be completed by surveillance officers during case investigation). 

This workflow is most closely aligned to the existing cenralized reporting system using Epi-Info. While this workflow is the most straight-forward to replace in a given country, the disadvantage of centralized reporting is that there can be long delays between the time a suspected case is notified from a health facility to the time the completed case details are entered into the systems to generate outbreak alerts or enable analysis. 

**_All diseases excluding Neonatal Tetanus_**
The possibility for laboratory specimen collection and lab diagnosis data to be attached to the case record is incorporated into the program design for all diseases *excluding Neonatal Tetanus (NT)*.

![workflow for all diseases](resources/images/workflow1.png)

**_Neonatal Tetanus_**
The workflow for Neonatal Tetanus excludes laboratory testing. 

![workflow for neonatal tetanus](resources/images/workflow2.png)

#### Decentralized reporting
While centralized reporting of case-based data for VPDs is typical for reporting upwards (e.g. to WHO for IHR compliance or other bodies according to data sharing agreements), many countries have already begun to implement *decentralized* electronic case-based disease surveillance using DHIS2. 

In a decentralized workflow, the configuration of **user groups** allows users and actors at various levels of the health system to apend daata to a shared electronic case record in DHIS2. For example, a health facility user may be responsible for notifying the case by completing an electronic case notification form, entering the clinical details of the suspected case, and completing the lab specimen request form. Once lab results are available for a given case (linked by a unique identifier or lab sample number), a laboratory user can enter the lab results into the Lab program stage. Depending on policies in country, another groups of users such as surveillance officers may be responsible for determining and updating the Final Classification. 

One major benefit of a decentralized reporting system is timeliness of data amd availability of data in the electronic system for outbreak investigation and response. For example, facilities can report suspected cases into the DHIS2 VPD program in near real-time, enhancing the early warning function of the system. When lab results are available, the data can be added to the case record and indicators and outbreak alert thresholds configured into the system will be updated automatically. 

### Analysis & Use 
Surveillance data captured in the DHIS2 case-based system can be made available to users from national to district and facility levels according to the configuration of user access settings. Regardless of which level of the system data are *entered* electronically into the system, data can be made available for analysis automatically down to the level of initial reporting (i.e. facility and upwards). Triangulation of case-based data for VPDs captured in DHIS2 alongside immunization coverage rates and other data sources can be used by national immunization programme staff to identify zero-dose and under-immunized pockets of the population. 

**Program indicators** have been configured as part of the case-based package according to disease-specific requirements, including operational indicators that are useful for planning and mobitoring response activities. In addition to pre-configured **dashboards** included in the package specific to each disease, the following dashboards incorporate data from across diseases:
1.  CBS Alert/Outbreak dashboard: summarizes outbreak alerts (based on pre-configured thresholds for case-based data) across all VPDs included in the package at district level for rapid analysis
2.  CBS-IDSR Comparative Dashboard: when the CBS package is installed with the aggregate surveillance (IDSR) package in DHIS2, this dashbaord enables analysis and data quality/completeness reviews across case-based and aggregate reporting flows for VPDs 

## Program Structure
All of the programs in the VPD-CBS package have a similar design, however different sections and variables are attached to each disease **_based on the initial diagnosis that is selected during registration_**. The program is made up of the following stages in its design:

1. Enrollment Details
2. Diagnostic & Clinical Information
3. Laboratory request
4. Specimen Tracking
5. Laboratory Result
6. Final Classification

Note suspected Neonatal Tetanus cases do not require lab specimen collection or laboratory confirmation. Therefore, program rules are used to show only the following program stages for NT cases: 

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

A complete list of program indicators is inluded in the metadata reference file for the package, accessed at [dhis2.org/who-package-downloads](https://dhis2.org/who-package-downloads)

# Implementation & Local Adaptation 

For AFRO Member States, this package is optimized and approved by the Regional Office to replace the existing AFRO VPD surveillance EPI Info system with DHIS2 VPD surveillance package. The package meets the functional requirements, workflows and mandatory data variables for reporting that have previously been done in EPI Info. Countries using this package can push their case-based data to the AFRO regional respository directly from the national DHIS2 instance where the VPD package is installed & used. Thus, as part of country implementation in AFRO Member States, discussions around how and when to phase out the use of the EPI Info reporting system are recommendec to reduce duplicate data entry and strengthen feedback loops & data quality in the DHIS2-based system.

Extension and expansion of the DHIS2 VPD case surveillance system in future phases is anticipated to:
* Strengthen response and management of public health actions through the support of local workflows for case notification
* Enable the identification and management of outbreaks based on the VPD case reporting system contained in the package.

# References
WHO Regional Office for Africa (2019). Technical guidelines for integrated disease surveillance & response in the WHO AFRO Region. Retrieved from: https://apps.who.int/iris/bitstream/handle/10665/325015/WHO-AF-WHE-CPI-05.2019-eng.pdf

US CDC (2021). Global Disease Detection Operations Center: Overview. Retrieved from: https://www.cdc.gov/globalhealth/healthprotection/gddopscenter/how.html


