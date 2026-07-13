# Sunshine Mental Health Counseling Portal

# Updated Database Design Analysis

**Database Type:** Relational Database (PostgreSQL)

This document explains the database schema, table purposes, relationships, primary keys, foreign keys, and authorization architecture.

---

# Overall Architecture

The database is divided into logical modules.

```
Authentication & Authorization
│
├── Users
├── Roles
├── User Roles
├── Staff Profiles
├── Patients
├── Doctors


Medical Module
│
├── Medical Reports
├── Appointments
├── Session Notes
├── Doctor Availability


E-Commerce Module
│
├── Products
├── Cart
├── Orders
├── Payments


Communication Module
│
├── Chat Rooms
├── Chat Messages
├── Notifications


System Management Module
│
├── Audit Logs
```

---

# Authorization Architecture

The system does not store roles directly inside the USERS table.

Instead, a separate role management system is used.

```
                 USERS
                    │
                    │
              USER ROLES
                    │
                    │
                  ROLES
```

This supports:

* Multiple roles for one user.
* Dynamic permission management.
* Future role expansion.

Example:

```
User A

Roles:
    Patient
    Staff
```

---

# Role Hierarchy

The system follows hierarchical authorization.

```
                 ADMIN
                   |
                   |
                 STAFF
                   |
        --------------------
        |                  |
     DOCTOR            PATIENT
```

## Admin

Highest-level authority.

Can:

* Create users.
* Delete users.
* Assign roles.
* Remove Staff accounts.
* Change permissions.
* Verify users manually.
* Access audit logs.
* Manage system settings.

---

## Staff

Administrative employee.

Can:

* Create users.
* Verify phone numbers.
* Verify emails.
* Approve doctors.
* Manage products.
* Manage orders.
* Assist administration.

Cannot:

* Remove Admin role.
* Modify Admin privileges.

---

## Doctor

Medical authority.

Can:

* Manage availability.
* Accept appointments.
* Write session notes.
* Communicate with patients.

---

## Patient

Normal user.

Can:

* Book appointments.
* Upload medical reports.
* Purchase products.
* Chat with doctors.

---

# Entity Descriptions

---

# 1. USERS

The USERS table is the central authentication entity.

Every person accessing the system has exactly one user account.

It stores login and account information.

## Primary Key

```
Id (UUID)
```

## Attributes

| Column         | Description            |
| -------------- | ---------------------- |
| Id             | Unique user identifier |
| Email          | Login email            |
| PhoneNumber    | User phone             |
| PasswordHash   | Encrypted password     |
| IsActive       | Account status         |
| IsDeleted      | Soft delete            |
| EmailConfirmed | Email verification     |
| PhoneConfirmed | Phone verification     |
| CreatedAt      | Creation date          |
| UpdatedAt      | Last modification      |

---

## Relationships

A User can have:

* Patient profile.
* Doctor profile.
* Staff profile.
* Multiple roles.

A User can also:

* Upload medical reports.
* Make payments.
* Send messages.
* Receive notifications.
* Create orders.
* Own a cart.

---

# 2. ROLES

Stores all available system roles.

Examples:

```
Admin
Staff
Doctor
Patient
```

---

## Primary Key

```
RoleId
```

---

## Attributes

| Column         | Description            |
| -------------- | ---------------------- |
| RoleId         | Unique role identifier |
| RoleName       | Name of role           |
| HierarchyLevel | Permission priority    |
| Description    | Role details           |

---

Example:

| Role    | Level |
| ------- | ----- |
| Patient | 1     |
| Doctor  | 20    |
| Staff   | 80    |
| Admin   | 100   |

Higher hierarchy means higher authority.

---

# 3. USER ROLES

Connects users with roles.

This creates a many-to-many relationship.

---

## Primary Key

```
Id
```

## Foreign Keys

```
UserId → Users(Id)

RoleId → Roles(RoleId)

AssignedBy → Users(Id)
```

---

Example:

```
User
 |
 +---- Patient

User
 |
 +---- Staff
```

---

Stores:

* Who received the role.
* Who assigned the role.
* Assignment date.
* Active status.

---

# 4. STAFF PROFILES

Stores additional information for administrative employees.

Only Staff and Admin users require this profile.

---

## Primary Key

```
Id
```

## Foreign Key

```
UserId → Users(Id)
```

---

Stores:

* Employee ID.
* Department.
* Position.
* Joining date.
* Super Admin status.

Example:

```
Employee ID:

ADM-0001

STF-0025
```

Admin accounts can use employee IDs for secure administrative login.

---

# 5. PATIENTS

Stores patient-specific information.

Every patient must have a User account.

---

## Foreign Key

```
UserId → Users(Id)
```

---

Stores:

* Name.
* Date of birth.
* Gender.
* Emergency contact.
* Address.
* Consent information.

---

Relationships:

One Patient:

```
    |
    |
    +---- Many Appointments

    |
    +---- Many Medical Reports
```

---

# 6. DOCTORS

Stores doctor information.

Every doctor must have a User account.

---

Stores:

* Specialization.
* Biography.
* Experience.
* Consultation fee.
* Verification status.

---

Relationships:

Doctor:

```
    |
    +---- Availability

    |
    +---- Appointments

    |
    +---- Session Notes
```

---

# 7. MEDICAL REPORTS

Stores uploaded medical documents.

Examples:

* Test reports.
* Prescriptions.
* Scan reports.

---

Foreign Keys:

```
PatientId

UploadedByUserId
```

---

Relationship:

```
Patient
   |
   |
Many Reports
```

---

# 8. DOCTOR AVAILABILITY

Stores doctor's available time slots.

Example:

```
Monday

09:00 - 12:00
```

---

Relationship:

```
Doctor

   |

Many Availability Slots
```

---

# 9. APPOINTMENTS

Core medical transaction table.

Stores:

* Appointment time.
* Duration.
* Status.
* Session type.
* Payment information.

---

Foreign Keys:

```
PatientId

DoctorId

PaymentId
```

---

Relationships:

```
Patient
   |
Many Appointments
   |
Doctor
```

---

# 10. SESSION NOTES

Doctor notes after consultation.

---

Foreign Keys:

```
AppointmentId

DoctorId
```

---

Relationship:

```
One Appointment

       |

One Session Note
```

---

# 11-17. Remaining Modules

The following modules remain unchanged:

## E-Commerce

```
Products
    |
Cart Items
    |
Orders
    |
Payments
```

Supports:

* Books.
* Medicines.
* Accessories.
* Checkout.

---

## Communication

```
Chat Room

     |

Chat Messages
```

Supports:

* Doctor-patient communication.
* Appointment-based chat.

---

## Notifications

Stores:

* Appointment updates.
* Payment updates.
* Verification status.

---

## Audit Logs

Tracks important actions.

Examples:

```
Admin removed Staff role

Staff verified Doctor

User deleted account
```

Stores:

* User.
* Action.
* Entity.
* Previous value.
* New value.
* Timestamp.

---

# Relationship Summary

## One-to-One

```
User
 |
 +---- Patient

User
 |
 +---- Doctor

User
 |
 +---- Staff Profile

Appointment
 |
 +---- Session Note

User
 |
 +---- Cart
```

---

## One-to-Many

```
Patient
 |
 +---- Appointments
 |
 +---- Medical Reports


Doctor
 |
 +---- Availability
 |
 +---- Appointments
 |
 +---- Session Notes


User
 |
 +---- Orders
 |
 +---- Payments
 |
 +---- Notifications
 |
 +---- Audit Logs


Chat Room
 |
 +---- Messages
```

---

## Many-to-Many

```
Users

 |

User Roles

 |

Roles
```

---

# Updated Primary Key Summary

| Table              | Primary Key |
| ------------------ | ----------- |
| Users              | Id          |
| Roles              | RoleId      |
| UserRoles          | Id          |
| StaffProfiles      | Id          |
| Patients           | Id          |
| Doctors            | Id          |
| MedicalReports     | Id          |
| DoctorAvailability | Id          |
| Appointments       | Id          |
| SessionNotes       | Id          |
| Products           | Id          |
| Carts              | Id          |
| CartItems          | Id          |
| Orders             | Id          |
| OrderItems         | Id          |
| Payments           | Id          |
| ChatRooms          | Id          |
| ChatMessages       | Id          |
| AuditLogs          | Id          |
| Notifications      | Id          |

---

# Updated Foreign Key Summary

| Table              | Foreign Keys                                         |
| ------------------ | ---------------------------------------------------- |
| UserRoles          | UserId, RoleId, AssignedBy                           |
| StaffProfiles      | UserId                                               |
| Patients           | UserId                                               |
| Doctors            | UserId                                               |
| MedicalReports     | PatientId, UploadedByUserId                          |
| DoctorAvailability | DoctorId                                             |
| Appointments       | PatientId, DoctorId, PaymentId                       |
| SessionNotes       | AppointmentId, DoctorId                              |
| Carts              | UserId                                               |
| CartItems          | CartId, ProductId                                    |
| Orders             | UserId, PaymentId                                    |
| OrderItems         | OrderId, ProductId                                   |
| Payments           | UserId                                               |
| ChatRooms          | ParticipantAId, ParticipantBId, RelatedAppointmentId |
| ChatMessages       | ChatRoomId, SenderId                                 |
| AuditLogs          | UserId                                               |
| Notifications      | UserId                                               |

---

# Final Database Flow

```
                         USERS
                            |
          ┌─────────────────┼─────────────────┐
          |                 |                 |
      PATIENTS          DOCTORS        STAFF PROFILE
          |                 |                 |
          |                 |                 |
          └────── APPOINTMENTS ──────────────┘
                         |
                         |
                  SESSION NOTES


                         USERS
                           |
                     USER ROLES
                           |
                         ROLES
                           |
                  ADMIN / STAFF CONTROL


                         USERS
                           |
          ┌────────────────┼────────────────┐
          |                |                |
        CARTS           ORDERS          PAYMENTS
          |                |
      CART ITEMS      ORDER ITEMS


                         USERS
                           |
                  CHAT ROOMS
                           |
                  CHAT MESSAGES


                         USERS
                           |
                 NOTIFICATIONS
                           |
                  AUDIT LOGS
```

---

# Conclusion

The updated database design follows a modular relational architecture centered around the `Users` entity. Authentication, authorization, medical services, e-commerce, communication, and system monitoring are separated into independent modules.

The addition of the **Role Management System** improves security and scalability by replacing fixed roles with a hierarchical authorization model. The system can now support Admin, Staff, Doctor, Patient, and future roles without modifying the database structure.

The design follows normalization principles, maintains data integrity through primary and foreign keys, and is suitable for implementation using **PostgreSQL with ASP.NET Core Entity Framework**.
