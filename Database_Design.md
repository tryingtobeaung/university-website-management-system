Database Design
University Website Management System
1. Overview
The database is designed to store and manage information related to students, faculty, courses, announcements, events, and website users. The design follows relational database principles to ensure data integrity, consistency, and scalability.

2. Database Management System
Database: MySQL

Version: MySQL 8.0+

Architecture: Relational Database Management System (RDBMS)

3. Entity Relationship Diagram (ERD)
USERS
│
├── STUDENTS
│
├── FACULTY
│
└── ADMINS

FACULTY
│
└── COURSES

STUDENTS
│
└── ENROLLMENTS
     │
     └── COURSES

ADMINS
│
├── NEWS
│
└── EVENTS

VISITORS
│
└── CONTACT_MESSAGES
4. Database Tables
USERS
Stores authentication and account information.

Column	Data Type	Constraint
user_id	INT	PK, AUTO_INCREMENT
full_name	VARCHAR(100)	NOT NULL
email	VARCHAR(100)	UNIQUE
password	VARCHAR(255)	NOT NULL
role	ENUM('Student','Faculty','Admin')	NOT NULL
created_at	TIMESTAMP	DEFAULT CURRENT_TIMESTAMP
Primary Key
user_id
STUDENTS
Stores student information.

Column	Data Type	Constraint
student_id	INT	PK, AUTO_INCREMENT
user_id	INT	FK
student_number	VARCHAR(20)	UNIQUE
department	VARCHAR(100)	NOT NULL
year_level	INT	NOT NULL
Foreign Keys
user_id REFERENCES users(user_id)
FACULTY
Stores faculty information.

Column	Data Type	Constraint
faculty_id	INT	PK, AUTO_INCREMENT
user_id	INT	FK
department	VARCHAR(100)	NOT NULL
designation	VARCHAR(100)	NOT NULL
Foreign Keys
user_id REFERENCES users(user_id)
COURSES
Stores academic course information.

Column	Data Type	Constraint
course_id	INT	PK, AUTO_INCREMENT
course_code	VARCHAR(20)	UNIQUE
course_name	VARCHAR(150)	NOT NULL
credit_hours	INT	NOT NULL
faculty_id	INT	FK
Foreign Keys
faculty_id REFERENCES faculty(faculty_id)
ENROLLMENTS
Stores student-course relationships.

Column	Data Type	Constraint
enrollment_id	INT	PK, AUTO_INCREMENT
student_id	INT	FK
course_id	INT	FK
semester	VARCHAR(20)	NOT NULL
academic_year	VARCHAR(20)	NOT NULL
Foreign Keys
student_id REFERENCES students(student_id)

course_id REFERENCES courses(course_id)
NEWS
Stores university announcements and news.

Column	Data Type	Constraint
news_id	INT	PK, AUTO_INCREMENT
title	VARCHAR(255)	NOT NULL
content	TEXT	NOT NULL
publish_date	DATE	NOT NULL
admin_id	INT	FK
Foreign Keys
admin_id REFERENCES users(user_id)
EVENTS
Stores university events.

Column	Data Type	Constraint
event_id	INT	PK, AUTO_INCREMENT
title	VARCHAR(255)	NOT NULL
description	TEXT	NOT NULL
event_date	DATE	NOT NULL
location	VARCHAR(255)	NOT NULL
admin_id	INT	FK
Foreign Keys
admin_id REFERENCES users(user_id)
CONTACT_MESSAGES
Stores inquiries submitted through the Contact Us page.

Column	Data Type	Constraint
message_id	INT	PK, AUTO_INCREMENT
name	VARCHAR(100)	NOT NULL
email	VARCHAR(100)	NOT NULL
subject	VARCHAR(255)	NOT NULL
message	TEXT	NOT NULL
submitted_at	TIMESTAMP	DEFAULT CURRENT_TIMESTAMP
5. Relationships
One-to-One Relationships
One User → One Student
One User → One Faculty Member
One-to-Many Relationships
One Faculty → Many Courses
One Admin → Many News Posts
One Admin → Many Events
Many-to-Many Relationships
Students ↔ Courses
Implemented using:

ENROLLMENTS TABLE
6. Normalization
The database follows Third Normal Form (3NF):

First Normal Form (1NF)
Atomic values only.
No repeating groups.
Second Normal Form (2NF)
Full dependency on primary keys.
Third Normal Form (3NF)
Elimination of transitive dependencies.
7. Security Considerations
Passwords stored using hashing algorithms.
Unique email validation.
Role-Based Access Control (RBAC).
Secure database connections.
8. Future Enhancements
Additional tables may include:

Admissions
Online Payments
Library Management
Student Results
Online Learning Resources
Database Summary
Table	Purpose
USERS	Authentication
STUDENTS	Student Records
FACULTY	Faculty Records
COURSES	Course Information
ENROLLMENTS	Student Enrollment
NEWS	Announcements
EVENTS	Event Management
CONTACT_MESSAGES	User Inquiries
Database Version: 1.0
Database Type: Relational Database (MySQL)
Project: University Website Management System