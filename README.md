Abstract
The Student Placement Management System (SPMS) is a centralized, database-driven application that replaces the spreadsheets, emails and notice boards a college placement cell typically relies on. It serves three roles: students, recruiters and the placement officer. Students maintain a profile and apply only to drives they are eligible for. Recruiters post drives, shortlist candidates and record interview outcomes. The placement officer approves companies, sets eligibility rules and generates reports. By automating eligibility checks, application tracking and notifications, the system reduces manual effort and missed deadlines, and gives the placement cell a single, reliable record of every student's placement status.
Keywords: placement management, campus recruitment, eligibility automation, role-based access, relational database.
1. Introduction
Campus placement is one of the most important services a technical college offers, and it involves many people at once: hundreds of students, dozens of visiting companies and a small placement cell coordinating them.
In most colleges this coordination still runs on spreadsheets, email threads and printed notices. Each drive needs eligibility criteria checked against student records, shortlists shared with companies, interview schedules announced and results recorded. When these steps are manual, data is duplicated across files, students miss notices, and the placement cell cannot easily answer simple questions such as who is eligible for a drive or how many students are placed.
The Student Placement Management System addresses this by keeping all placement data in one relational database and exposing it through role-based interfaces. Each user sees only what is relevant to them, and routine work such as eligibility filtering and status tracking is done by the system rather than by hand.
2. Problem Statement and Objectives
Placement records are scattered and manually maintained, which causes duplicated data, missed deadlines, inconsistent eligibility decisions and no single view of placement status.
Objectives
1. Provide one centralized database for student profiles, companies, drives and applications.
2. Let students register, build a profile, upload a resume and apply to drives online.
3. Check eligibility automatically against criteria such as CGPA, backlogs and branch.
4. Let recruiters post drives, shortlist candidates, schedule interview rounds and record results.
5. Give the placement officer tools to approve companies and drives, manage records and generate reports.
6. Keep students informed of new drives and status changes through notifications.
7. Protect data with role-based access, so each user can reach only the functions meant for them.
3. Scope of the Project
The system covers the full placement cycle inside one institution, from student registration to recording the final offer.
In scope
• Student, recruiter and placement officer accounts with role-based access
• Student profiles, resumes and academic records
• Company registration and drive creation, with approval by the placement officer
• Eligibility rules, online applications and status tracking
• Interview scheduling, result entry and offer records
• Notifications and placement reports
Out of scope
• Online aptitude tests or video interviews
• Payment handling or salary negotiation
• Integration with external job portals
4. Existing and Proposed System
The proposed system replaces manual coordination with a single database and automated rules.
Aspect
Existing (manual) system
Proposed system
Data storage
Separate spreadsheets and files
One relational database
Eligibility check
Done by hand per drive
Automatic, from stored rules
Notifications
Notice boards and email
Sent by the system on each event
Application tracking
Asked for from the placement cell
Visible to the student at any time
Reports
Compiled manually
Generated on demand
Access control
Anyone with the file
Role-based accounts
Data consistency
Duplicates and conflicting copies
One record per entity
5. Requirement Analysis
Functional requirements
• Users register and log in with a role of student, recruiter or placement officer.
• Students create and edit a profile, upload a resume and view eligible drives.
• Students apply to a drive and see the status of each application.
• Recruiters register a company, post drives with eligibility criteria and view applicants.
• Recruiters shortlist candidates, schedule rounds and record results and offers.
• The placement officer approves companies and drives, edits eligibility rules and views reports.
• The system sends a notification when a drive is posted or an application status changes.
Non-functional requirements
• Security: passwords stored hashed, and every page checks the user's role.
• Usability: a simple interface that a first-time student can use without training.
• Reliability: data is never lost on a failed request, using database transactions.
• Maintainability: modules for each role kept separate so each can change independently.
• Performance: common lists, such as eligible drives, load quickly using indexed queries.
Hardware and software requirements
Item
Requirement
Client device
Any computer or phone with a modern web browser
Server
A machine able to run the chosen back-end and database
Database
A relational database system
Back end and front end
[YOUR TECH STACK]
7. Database Design
The database holds seven core entities. A student applies to many drives, a company runs many drives, and each application links one student to one drive, which makes Application the central table.
Table
Key columns
Purpose
User
user_id (PK), email, password_hash, role
Login and role-based access
Student
student_id (PK), user_id (FK), name, roll_no, branch, section, cgpa, backlogs, resume
Student profile and academic record
Company
company_id (PK), user_id (FK), name, industry, approved
Recruiting organisation and approval status
Drive
drive_id (PK), company_id (FK), title, package_details, min_cgpa, max_backlogs, eligible_branches, deadline, approved
A job opening with its eligibility rules
Application
application_id (PK), student_id (FK), drive_id (FK), status, applied_on
One student's application to one drive
Interview
interview_id (PK), application_id (FK), round, scheduled_at, result
Interview rounds and outcomes
Notification
notification_id (PK), user_id (FK), message, sent_at, read
Messages shown to users
Relationships
• One User has one Student or one Company profile.
• One Company posts many Drives.
• One Student submits many Applications, and one Drive receives many Applications.
• One Application has many Interview rounds.
• One User receives many Notifications.
A unique constraint on (student_id, drive_id) stops a student from applying to the same drive twice.
