# Club-Collab - Project Overview

## Project Idea

**Club-Collab** is a centralized database system solving resource booking conflicts and unverified volunteer tracking at BRAC University. It manages clubs with multivalued contact emails, students with composite addresses using ISA relationships (General Students vs Club Executives), and events with M:N club collaborations. The equipment module uses weak entity maintenance logs with composite keys and triggers that auto-cancel bookings when equipment is damaged. Resource booking prevents double-booking through constraints, while volunteer tracking logs verified hours with CHECK constraints (0-24 hours). All six features integrate through a fully normalized schema, enabling conflict-free resource sharing and verified volunteer portfolios.

---

## Top 6 Features

### 1. Club Management
Manage university clubs with their information, departments, office locations, and multivalued contact emails. Supports multiple email addresses per club stored in a separate table following normalization principles.

### 2. Student Management
Comprehensive student database with composite addresses (Street, City, Zip) and multiple phone numbers. Implements ISA relationships to classify students into General Students (with year and major) and Club Executives (with position and term details).

### 3. Event Management
Create and manage club events with venue, date, and description. Supports M:N relationships for club collaborations, allowing multiple clubs to partner on events with specific contribution types tracked for each partner.

### 4. Equipment Management
Track shared resources (cameras, projectors, microphones) owned by clubs. Features weak entity maintenance logs with composite keys (Equip_ID, Log_ID) and intelligent triggers that automatically cancel future bookings when equipment status changes to "Damaged".

### 5. Resource Booking
Complete booking system for equipment reservations with time validation (return time must be after borrow time). Prevents double-booking conflicts through database constraints and maintains full transaction history with booking status tracking (Confirmed, Completed, Cancelled).

### 6. Volunteer Tracking
Log and verify student volunteer hours across different clubs and events. Includes CHECK constraints ensuring realistic hour entries (0-24 hours per event), verified by club executives, creating a reliable portfolio of student contributions and cross-club volunteering.

---

## Technical Highlights

- **Normalized 3NF Schema** - No data redundancy, efficient storage
- **ISA Relationships** - Student specialization (General/Executive)
- **Weak Entities** - Maintenance logs dependent on equipment
- **M:N Relationships** - Event-Club collaborations via junction tables
- **Database Triggers** - Auto-cancel bookings, prevent conflicts
- **Complex Attributes** - Composite addresses, multivalued emails/phones
- **CHECK Constraints** - Data validation (hours, dates, status)
- **Referential Integrity** - CASCADE and RESTRICT actions

---

**Course**: CSE370 (Database Systems) - BRAC University  
**Status**: Production Ready
