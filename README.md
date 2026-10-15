# Hospital Management System | SQL Project
An end-to-end relational database project built in MySQL, simulating a real hospital's data system — patient records, doctor management, appointments, prescriptions, billing, and lab reports — with business logic enforced directly at the database level.

📌 Project Overview
Hospitals generate data across many interconnected areas: departments, doctors, patients, appointments, prescriptions, billing, and diagnostics. This project models that entire ecosystem as a normalized relational database, then layers real business rules on top using SQL triggers and stored procedures.

🗂️ Database Schema
The database consists of 8 relational tables:

Table	Description
departments	Hospital departments (Cardiology, Neurology, etc.)
doctors	Doctor details, linked to a department
patients	Patient demographic information
appointments	Links patients and doctors with time and status
prescriptions	Medicines prescribed per appointment
bills	Billing details per appointment
labreports	Lab test results per appointment
doctor_credentials	Login credentials, linked 1:1 with doctors
ER Diagram
ER Diagram

⚙️ Key Features
1. Data Creation & Migration
Synthetic hospital data was generated and staged in a raw table (hospital_data), then migrated into normalized, relational tables using INSERT INTO ... SELECT with data type and date format conversions (STR_TO_DATE).

2. Business Rule Enforcement (Trigger)
A BEFORE INSERT trigger on the appointments table enforces two real-world constraints:

Appointments cannot be booked in the past
A doctor cannot have two overlapping "Scheduled" appointments at the same time
3. Role-Based Access Control (Stored Procedure)
view_doctor_data(username, password) authenticates a doctor and returns different data depending on their role:

Senior Consultants see all patient data across their entire department
Other doctors see only their own patients
This procedure joins patients, appointments, doctors, prescriptions, and labreports to build a complete clinical view.

4. Revenue Analytics (Stored Procedure)
sp_monthly_revenue(year, month) aggregates billing data by department for any given month — giving a finance-style, department-wise revenue report.

🛠️ Tech Stack
MySQL
SQL Triggers
Stored Procedures
Relational Database Design / Data Modeling
📁 Files in this Repository
schema.sql — table creation scripts with constraints and foreign keys
trigger_procedures.sql — trigger and stored procedure definitions
sample_queries.sql — example inserts and procedure calls used for testing
hospital_erd.png — entity relationship diagram
🚀 How to Use
Run schema.sql to create the database structure
Load your data into the tables (or use your own data migration script)
Run trigger_procedures.sql to add the trigger and stored procedures
Test using the queries in sample_queries.sql
💡 Key Learning
This project reinforced that data analysis isn't just about querying clean data — it's about understanding how that data is structured, validated, and secured at the source. Building the trigger and role-based access logic required thinking like a database designer, not just an analyst pulling numbers.
