# Sunshine Mental Health Counseling Portal
# Database Design Analysis

**Database Type:** Relational Database (PostgreSQL)

This document explains the database schema, table purposes, relationships, primary keys, and foreign keys.

---

# Overall Architecture

The database is divided into several logical modules.

```
Authentication
│
├── Users
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

System Module
│
├── Audit Logs
```

---

# Entity Descriptions

---

# 1. USERS

The USERS table is the heart of the application.

Every person who logs into the website has exactly one record here.

It stores authentication and account information.

## Primary Key

```
Id (UUID)
```

## Attributes

| Column | Description |
|----------|-------------|
| Id | Unique user ID |
| Email | User email |
| PhoneNumber | Mobile number |
| PasswordHash | Encrypted password |
| Role | Admin / Doctor / Patient |
| IsActive | Account enabled |
| IsDeleted | Soft delete flag |
| EmailConfirmed | Email verified |
| PhoneConfirmed | Phone verified |
| CreatedAt | Account creation date |
| UpdatedAt | Last update |

---

## Relationships

Users can become

- Patient
- Doctor

Users also

- upload reports
- make payments
- send chat messages
- receive notifications
- own shopping carts
- place orders

---

# 2. PATIENTS

Contains patient-specific information.

Every patient **must first be a User**.

## Primary Key

```
Id
```

## Foreign Key

```
UserId → Users(Id)
```

Meaning:

One User
↓

One Patient Profile

---

## Stores

- Full name
- Gender
- Birth date
- Emergency contact
- Address
- Consent information

---

## Relationships

A patient

- books appointments
- owns medical reports

---

# 3. DOCTORS

Contains doctor-specific information.

Every doctor is also a User.

## Primary Key

```
Id
```

## Foreign Key

```
UserId → Users(Id)
```

---

Stores

- Specialization
- Biography
- Consultation Fee
- Experience
- Verification Status
- Accepting Patients

---

Doctors

- create appointments
- write session notes
- define availability

---

# 4. MEDICAL REPORTS

Stores uploaded medical documents.

Examples

- Blood Test
- MRI
- Prescription
- ECG

---

## Primary Key

```
Id
```

## Foreign Keys

```
PatientId → Patients(Id)

UploadedByUserId → Users(Id)
```

Meaning

A report belongs to

One Patient

and

was uploaded by

One User.

---

# 5. DOCTOR AVAILABILITY

Stores doctor's working schedule.

Example

Monday

09:00

to

12:00

---

## Primary Key

```
Id
```

## Foreign Key

```
DoctorId → Doctors(Id)
```

One doctor

↓

Many availability slots

---

# 6. APPOINTMENTS

Stores appointment bookings.

This is one of the central tables.

---

## Primary Key

```
Id
```

## Foreign Keys

```
PatientId → Patients(Id)

DoctorId → Doctors(Id)

PaymentId → Payments(Id)
```

Stores

- Appointment Date
- Duration
- Status
- Online Meeting Link

---

Relationship

One Patient

↓

Many Appointments

One Doctor

↓

Many Appointments

---

# 7. SESSION NOTES

After appointment completion,

doctor writes notes.

---

## Primary Key

```
Id
```

## Foreign Keys

```
AppointmentId

DoctorId
```

Stores

Private Notes

Shared Summary

---

Relationship

One Appointment

↓

One Session Note

---

# 8. PRODUCTS

E-commerce inventory.

Includes

Books

Medicines

Accessories

---

## Primary Key

```
Id
```

Stores

Name

Description

Price

Stock

Prescription Required

Image

---

Referenced by

Cart Items

Order Items

---

# 9. CARTS

Shopping cart.

Each user owns one cart.

---

## Primary Key

```
Id
```

## Foreign Key

```
UserId → Users(Id)
```

Relationship

One User

↓

One Cart

---

# 10. CART ITEMS

Stores products inside cart.

---

## Primary Key

```
Id
```

## Foreign Keys

```
CartId

ProductId
```

Relationship

One Cart

↓

Many Cart Items

---

# 11. ORDERS

Completed purchases.

---

## Primary Key

```
Id
```

## Foreign Keys

```
UserId

PaymentId
```

Stores

Order Date

Status

Shipping Address

Total Price

---

Relationship

One User

↓

Many Orders

---

# 12. ORDER ITEMS

Stores purchased products.

---

## Primary Key

```
Id
```

## Foreign Keys

```
OrderId

ProductId
```

Relationship

One Order

↓

Many Products

---

# 13. PAYMENTS

Stores payment history.

Supports

Bkash

Nagad

Card

Bank

---

## Primary Key

```
Id
```

## Foreign Key

```
UserId
```

Stores

Amount

Provider

Transaction ID

Purpose

Status

---

Payments may belong to

Appointment

or

Order

---

# 14. CHAT ROOMS

Conversation container.

Supports

Doctor ↔ Patient

Support

Appointment Chat

---

## Primary Key

```
Id
```

## Foreign Keys

```
ParticipantAId

ParticipantBId

RelatedAppointmentId
```

Relationship

One chat room

↓

Many messages

---

# 15. CHAT MESSAGES

Actual chat messages.

---

## Primary Key

```
Id
```

## Foreign Keys

```
ChatRoomId

SenderId
```

Stores

Text

Attachment

Read Status

Flag

---

# 16. AUDIT LOGS

Tracks every important action.

Useful for

Security

Debugging

Compliance

---

## Primary Key

```
Id
```

## Foreign Key

```
UserId
```

Stores

Action

Entity

Old Value

New Value

Timestamp

---

# 17. NOTIFICATIONS

Stores notifications.

Examples

Appointment Confirmed

Payment Success

Doctor Accepted

Order Shipped

---

## Primary Key

```
Id
```

## Foreign Key

```
UserId
```

One user

↓

Many notifications

---

# Relationship Summary

## One-to-One Relationships

```
Users
    │
    ├── Patient

Users
    │
    └── Doctor

Appointment
    │
    └── Session Note

User
    │
    └── Cart
```

---

## One-to-Many Relationships

```
Patient
    ├── Appointments
    └── Medical Reports

Doctor
    ├── Availability
    ├── Appointments
    └── Session Notes

Cart
    └── Cart Items

Order
    └── Order Items

Chat Room
    └── Chat Messages

User
    ├── Orders
    ├── Payments
    ├── Notifications
    └── Audit Logs
```

---

## Many-to-One Relationships

Many Appointments

↓

One Doctor

Many Appointments

↓

One Patient

Many Cart Items

↓

One Product

Many Order Items

↓

One Product

Many Reports

↓

One Patient

Many Messages

↓

One Chat Room

---

# Primary Keys Summary

| Table | Primary Key |
|---------|-------------|
| Users | Id |
| Patients | Id |
| Doctors | Id |
| MedicalReports | Id |
| DoctorAvailability | Id |
| Appointments | Id |
| SessionNotes | Id |
| Products | Id |
| Carts | Id |
| CartItems | Id |
| Orders | Id |
| OrderItems | Id |
| Payments | Id |
| ChatRooms | Id |
| ChatMessages | Id |
| AuditLogs | Id |
| Notifications | Id |

---

# Foreign Keys Summary

| Table | Foreign Keys |
|---------|--------------|
| Patients | UserId |
| Doctors | UserId |
| MedicalReports | PatientId, UploadedByUserId |
| DoctorAvailability | DoctorId |
| Appointments | PatientId, DoctorId, PaymentId |
| SessionNotes | AppointmentId, DoctorId |
| Carts | UserId |
| CartItems | CartId, ProductId |
| Orders | UserId, PaymentId |
| OrderItems | OrderId, ProductId |
| Payments | UserId |
| ChatRooms | ParticipantAId, ParticipantBId, RelatedAppointmentId |
| ChatMessages | ChatRoomId, SenderId |
| AuditLogs | UserId |
| Notifications | UserId |

---

# Overall Database Flow

```
                 USERS
                   │
      ┌────────────┴────────────┐
      │                         │
  PATIENTS                  DOCTORS
      │                         │
      │                         │
      ├──── Appointments ───────┤
      │             │
      │             ▼
      │      Session Notes
      │
Medical Reports

Users
   │
   ├── Cart
   │      │
   │      ▼
   │   Cart Items
   │
   ├── Orders
   │      │
   │      ▼
   │  Order Items
   │
   └── Payments

Users
   │
   ├── Chat Rooms
   │      │
   │      ▼
   │ Chat Messages
   │
   ├── Notifications
   │
   └── Audit Logs
```

---

# Conclusion

This schema follows a modular relational design centered on the `Users` table. Domain-specific data (patients, doctors, appointments, commerce, chat, and auditing) is separated into dedicated tables and connected using foreign keys. This normalization reduces data duplication, improves consistency, and makes the database easier to maintain and extend. The design is well-suited for implementation in PostgreSQL and integrates cleanly with Entity Framework Core in an ASP.NET Core application.