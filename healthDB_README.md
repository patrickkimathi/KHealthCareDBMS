PROJECT TITLE : Kenya Health Management Database System

# Kenya Health Management Database (healthDB)

## Overview
The **Kenya Health Management Database (healthDB)** is a relational database system built using **MySQL** to manage health-related data in Kenya. 
It captures administrative units (counties, subcounties, wards), healthcare facilities, staff, patients, visits, diagnoses, and prescriptions.  

The system is designed to reflect the hierarchical structure of Kenya’s health system and can be used for reporting, analytics, and health information management.

---
## Key Features
- **Administrative Units:** Counties, subcounties, and wards linked in a hierarchical structure.
- **Health Facilities:** Facility types, facility ownership, and facility units.
- **People:** Both patients and healthcare staff with demographics and contact info.
- **Visits & Services:** Patient visits, diagnoses, and prescriptions.
- **Medication Management:** Prescription tracking and medication details.

---

## Database Schema Overview
The database contains the following key entities:
1. **Administrative Tables**
   - counties – Stores county details.
   - subcounties – Linked to counties.
   - wards– Linked to subcounties.

2. **Healthcare Facilities**
   - facilityTypes – Defines types and levels of facilities.
   - facilities – Health facilities located within wards.
   - Facility_units– Departments/units within each facility.

3. **People Management**
   - people – Stores demographic details of staff and patients.
   - staff – Links health workers to facilities.
   - patients – Links patients to facilities and assigns a primary facility.

4. **Clinical Information**
   - visits – Patient visits and service data.
   - diagnoses – Diagnoses recorded per visit.
   - medications – Medication master list.
   - prescription– Prescription records linked to visits.
   - prescription_items – Medications issued within a prescription.

---

## Installation Instructions

1. **Requirements:**
   - MySQL 8.0 or later.
   - MySQL client (Workbench, CLI, or phpMyAdmin).

2. **Steps:**
   -- Drop database if it exists
   DROP DATABASE IF EXISTS healthDB;

   -- Create the database
   CREATE DATABASE healthDB;

   -- Use the database
   USE healthDB;

   -- Run all CREATE TABLE statements from the provided SQL script
Constraints & Relationships:

All necessary primary keys (PK) and foreign keys (FK) are included.

Cascading updates and deletes are implemented where appropriate.

Unique constraints for entity uniqueness (e.g., county names, ward names, facility names).

ERD Diagram
The database is normalized and follows clear relationships:

1 County → Many Subcounties

1 Subcounty → Many Wards

1 Ward → Many Facilities

1 Facility → Many Facility Units, Staff, Patients

1 Patient → Many Visits → Many Diagnoses, Prescriptions


Sample Queries
List all facilities in a county:

SELECT f.FACILITYNAME, c.COUNTYNAME
FROM facilities f
JOIN wards w ON f.WARDID = w.WARDID
JOIN subcounties s ON w.SUBCOUNTYID = s.SUBCOUNTYID
JOIN counties c ON s.COUNTYID = c.COUNTYID
WHERE c.COUNTYNAME = 'Nairobi';
Retrieve patient visit history:


SELECT p.PATIENTID, v.VISITID, v.START_TIME, v.REASON
FROM patients p
JOIN visits v ON p.PATIENTID = v.PATIENTID
WHERE p.PATIENTID = 1;

Author
Project Developer:PATRICK KARIUKI

Date: 22/08/2025
===============================================================================
ENTITY RELATIONSHIP DIAGRAM FOR healthDB
<img width="1007" height="1204" alt="ERD DIAGRAM" src="https://github.com/user-attachments/assets/ca33c348-f7e7-4995-9f34-904cdb340266" />

