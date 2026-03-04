# Club-Collab Database Features

## Overview
Club-Collab is a centralized database system that solves resource booking conflicts and unverified volunteer tracking at BRAC University. This document outlines all functional features - what users can actually DO with the system.

---

## Core Features

### 1. Club Management
- Create and manage university clubs with department and office location
- Store multiple contact emails per club (multivalued attribute)
- View all clubs with their contact information
- Track club statistics (members, equipment owned, events organized)
- View club activity summaries and performance metrics

**Use Cases:**
- Register new clubs (BUCC, ROBU, IEEE, etc.)
- Update club contact information
- View club portfolios with all activities

---

### 2. Student Management
- Register students with complete profile (name, email, address, phone numbers)
- Store multiple phone numbers per student (multivalued attribute)
- Store composite address (Street, City, Zip)
- Classify students into two types using ISA relationship:
  - **General Students**: Track year of study (1-4) and major
  - **Club Executives**: Track position, term start/end dates
- View student engagement profiles and volunteer history

**Use Cases:**
- Onboard new students to the system
- Promote students to executive positions
- Track student academic information
- Maintain multiple contact methods per student

---

### 3. Club Membership
- Students can join multiple clubs (M:N relationship)
- Track membership roles (Member, Volunteer, Executive, Advisor)
- Record join dates for each membership
- View all members of a club
- View all clubs a student belongs to
- Prevent duplicate memberships (unique constraint)

**Use Cases:**
- Student joins BUCC as a member
- Track when students joined clubs
- View club rosters
- Identify students with multiple club affiliations

---

### 4. Event Management
- Create events with title, date, venue, and organizing club
- Support multi-club collaboration (M:N relationship)
  - One event can have multiple partner clubs
  - Track contribution type for each partner (Technical Support, Sponsorship, etc.)
- View upcoming events with resource requirements
- Track event success metrics (volunteers, equipment used, partners)
- View event history and past activities

**Use Cases:**
- BUCC organizes "Tech Fest 2024"
- ROBU and IEEE partner on the event
- View all collaborative events
- Analyze event success patterns

---

### 5. Equipment Management
- Register shared resources (cameras, projectors, microphones, laptops, speakers)
- Track equipment status in real-time:
  - Available
  - In-Use
  - Damaged
  - Maintenance
- Assign equipment ownership to clubs
- View equipment availability dashboard
- Track equipment utilization and ROI
- Filter equipment by status and type
- Record purchase dates

**Use Cases:**
- Photography Club registers Canon EOS camera
- Check which equipment is available for booking
- Identify underutilized equipment
- Track equipment ownership across clubs

---

### 6. Equipment Maintenance Tracking
- Log maintenance history for each equipment (weak entity with composite key)
- Record maintenance date, description, and cost
- Track total maintenance costs per equipment
- Calculate average cost per maintenance
- Identify high-maintenance equipment
- View days since last maintenance
- Generate maintenance reports

**Use Cases:**
- Camera sent for lens cleaning - log cost and description
- Track projector bulb replacements
- Identify equipment with high maintenance costs
- Plan maintenance budgets

---

### 7. Resource Booking System
- Book equipment for events with specific time slots (borrow/return times)
- **Prevent double-booking conflicts** (automatic validation via trigger)
- Track booking status:
  - Confirmed
  - Completed
  - Cancelled
- View upcoming bookings and next available time
- **Automatic cancellation when equipment is damaged** (trigger)
- **Automatic status updates** (Available ↔ In-Use) based on booking times
- Validate booking times (return must be after borrow)
- View booking history per equipment or event

**Use Cases:**
- BUCC books projector for Tech Fest (Dec 15, 8 AM - 8 PM)
- System prevents overlapping bookings automatically
- Camera breaks - all future bookings auto-cancelled
- View when equipment will be available next

---

### 8. Volunteer Tracking & Verification
- Log volunteer hours for each event
- Record volunteer roles (Registration, Logistics, Technical Assistant, Setup Crew, Media Team)
- Verify hours worked by club executives
- Track cross-club volunteering (students helping clubs they're not members of)
- **Validate hours** (0-24 hours per event with CHECK constraint)
- Build verified volunteer portfolios for students
- Prevent logging hours for future events (trigger validation)
- Track verification status and verifier

**Use Cases:**
- Ahmed volunteers 5 hours at IEEE event (he's a BUCC member)
- Executive verifies volunteer hours
- Students build portfolio of verified contributions
- Identify top cross-club volunteers

---

### 9. Volunteer Badge System (Gamification)
- Award achievement badges based on volunteer hours (M:N relationship)
- Track badge progression across 5 tiers:
  - **Bronze**: Entry-level (1-10 hours) - Newcomer, Helper, Contributor
  - **Silver**: Intermediate (10-50 hours) - Dedicated, Committed
  - **Gold**: Advanced (50-100 hours) - Champion, Legend
  - **Platinum**: Expert (100-200 hours) - Hero
  - **Diamond**: Master (500+ hours) - Master
- **Automatic badge awarding** when volunteer hours are logged (trigger)
- View all available badges with requirements, descriptions, icons, and colors
- Track earned badges with date and total hours at time of earning
- View volunteer statistics dashboard (total hours, events, badges earned, highest tier)
- View leaderboard ranking volunteers by total hours with medal indicators
- Track progress to next badge milestone
- View badge distribution statistics across all volunteers
- Prevent duplicate badge awards (unique constraint)
- Special badges for cross-club volunteering and event organizing

**Use Cases:**
- Ahmed logs 5 volunteer hours - automatically earns "Helper" badge
- View all badges Ahmed has earned with dates and progression
- Check leaderboard to see top 10 volunteers with rankings
- View badge statistics showing 45% of volunteers have Bronze tier
- Track progress: "15 hours logged, 5 more hours until Dedicated badge"
- View volunteer profile with complete badge showcase and achievements
- Earn "Cross-Club Volunteer" badge for helping 3 different clubs

---

### 10. Analytics & Reports

#### Complex Queries Available:

**A. Top Cross-Club Volunteer**
- Find student with most volunteer hours in clubs they're NOT a member of
- Encourages inter-club collaboration
- Shows home club vs clubs helped

**B. Equipment Utilization Analysis**
- Most and least used equipment
- Total bookings and hours booked
- Maintenance cost vs usage (ROI rating)
- Bookings per month since purchase
- Identify equipment to purchase or retire

**C. Club Collaboration Network**
- Which clubs collaborate most frequently
- Shared equipment usage between clubs
- Collaboration strength scores
- Partnership patterns

**D. Event Success Metrics**
- Rank events by success score
- Factors: volunteers, partners, equipment used
- Event scale classification (Small/Medium/Large)
- Cross-club participation rates

**E. Student Engagement Ranking**
- Comprehensive scoring system:
  - Total volunteer hours (weight: 2)
  - Events volunteered (weight: 5)
  - Cross-club events (weight: 10)
  - Clubs joined (weight: 3)
  - Executive status (weight: 20)
  - Different roles performed (weight: 5)
- Engagement categories: Champion, Active, Engaged, Participant, Inactive
- Overall ranking across all students

**F. Booking Pattern Analysis**
- Peak times by day of week and hour
- Average booking duration by equipment type
- Demand level predictions
- Optimize scheduling based on patterns

---

### 11. Database Views (Pre-built Reports)

**A. Available Volunteers**
- Students NOT assigned to today's events
- Shows total volunteer hours and club memberships
- Helps find volunteers quickly

**B. Equipment Dashboard**
- Real-time equipment status
- Upcoming bookings count
- Next available time
- Total maintenance costs
- Owner club information

**C. Club Activity Summary**
- Total members per club
- Equipment owned
- Events organized and collaborated
- Total volunteer hours generated
- Performance ranking

**D. Student Volunteer Profile**
- Clubs joined
- Events volunteered
- Total and average hours
- Last volunteer date
- Executive status
- Engagement metrics

**E. Volunteer Stats (with Badge Progress)**
- Total volunteer hours and events participated
- Clubs helped and cross-club hours
- Badges earned count and highest tier achieved
- Next badge name and hours needed
- Progress percentage to next badge

**F. Volunteer Leaderboard**
- Rank position for each volunteer
- Total hours and events count
- Badges earned and highest tier
- Sortable by hours or badges

**G. Badge Statistics**
- Badge name, tier, and hours required
- Total students who earned each badge
- Percentage distribution across all volunteers
- Identify most and least common badges

**H. Upcoming Events Resources**
- Future events with dates
- Equipment booked for each event
- Partner clubs count
- Volunteers assigned
- Complete equipment list

**I. Equipment Maintenance History**
- Maintenance count per equipment
- Total and average costs
- Last maintenance date
- Days since last maintenance
- Identify high-maintenance items

**J. Cross-Club Volunteers**
- Students volunteering outside home clubs
- Cross-club hours and events
- List of clubs helped
- Encourages collaboration

**K. Booking Conflicts Report**
- Detect any scheduling conflicts
- Shows overlapping bookings
- Proactive conflict detection

---

### 12. Data Integrity & Automation

**Automatic Triggers:**
1. **Auto-cancel bookings on equipment damage** - When equipment status changes to "Damaged", all future confirmed bookings are automatically cancelled
2. **Prevent double-booking** - System blocks overlapping bookings for same equipment
3. **Validate equipment availability** - Cannot book damaged or maintenance equipment
4. **Auto-update equipment status** - Changes to "In-Use" when booking starts, back to "Available" when completed
5. **Validate volunteer hours** - Cannot log hours for future events, max 24 hours per event
6. **Executive membership validation** - Ensures data consistency for leadership roles
7. **Auto-award badges** - Automatically awards eligible badges when volunteer logs are created or updated

**Constraints:**
- Primary keys on all tables (unique identification)
- Foreign keys with CASCADE/RESTRICT (referential integrity)
- Unique constraints (no duplicate club names, emails, memberships, badge awards)
- Check constraints (valid year 1-4, hours 0-24, valid status values, valid badge tiers)
- Not null constraints (required fields)

**Automatic ID Generation:**
- Club_ID, Student_ID, Event_ID, Equip_ID, Badge_ID auto-generated
- Ensures no ID conflicts

---

### 13. Search & Filter Capabilities

**Equipment Filters:**
- By status (Available, In-Use, Damaged, Maintenance)
- By type (Camera, Projector, Microphone, Laptop, Speaker)
- By owner club

**Volunteer Log Filters:**
- By student (view all volunteer activities)
- By event (view all volunteers for an event)
- By date range

**Event Filters:**
- By date (past, current, upcoming)
- By organizing club
- By partner clubs

**Badge Filters:**
- By tier (Bronze, Silver, Gold, Platinum, Diamond)
- By hours required
- By earned status (for specific student)

**General Features:**
- Pagination support for large datasets
- Sorting by multiple fields
- Search by name, email, title

---

## Technical Highlights

### Database Design Excellence
- ✅ **Fully Normalized (3NF/BCNF)** - No data redundancy, optimal storage
- ✅ **ISA Relationships** - Student specialization (General/Executive)
- ✅ **Weak Entities** - Maintenance logs dependent on equipment
- ✅ **M:N Relationships** - Event-Club collaborations, Student-Club memberships, Student-Badge awards
- ✅ **Composite Attributes** - Address decomposed into Street, City, Zip
- ✅ **Multivalued Attributes** - Multiple emails per club, phones per student
- ✅ **8 Database Triggers** - Automated business logic including badge awarding
- ✅ **11 Database Views** - Pre-built reports and dashboards
- ✅ **13 Indexes** - Optimized query performance

### Scalability
- Supports 10,000+ students
- Handles 500+ events per year
- Manages 100-200 equipment items
- Tracks 5,000+ volunteer logs annually
- 1,000+ bookings per semester
- Unlimited badge awards and tracking


---

## Use Case Scenarios

### Scenario 1: Event Planning
1. BUCC creates "Tech Fest 2024" event
2. Adds ROBU and IEEE as partner clubs
3. Books projector and microphones for the event
4. System validates no conflicts exist
5. Assigns volunteers from multiple clubs
6. Tracks all volunteer hours with verification
7. Volunteers automatically earn badges based on hours

### Scenario 2: Equipment Management
1. Photography Club registers new Canon camera
2. BUCC wants to borrow it for their event
3. System shows camera is available
4. BUCC books camera for specific time slot
5. Camera status automatically changes to "In-Use"
6. After event, status returns to "Available"
7. If camera breaks, all future bookings auto-cancelled

### Scenario 3: Student Engagement & Badges
1. Ahmed joins BUCC as a member
2. Volunteers 5 hours at IEEE event (cross-club)
3. System automatically awards "Helper" badge (Bronze tier)
4. Volunteers 8 hours at BUCC event (home club)
5. Executive verifies all hours
6. Ahmed earns "Contributor" badge automatically
7. System calculates engagement score
8. Ahmed ranks as "Active" volunteer on leaderboard
9. Portfolio shows verified contributions and badge collection
10. Progress tracker shows 3 more hours until "Dedicated" badge

### Scenario 4: Analytics & Recognition
1. Admin runs "Top Cross-Club Volunteer" query
2. Identifies Ahmed with 15 hours in non-home clubs
3. Runs equipment utilization report
4. Finds projector has high usage, low maintenance cost
5. Identifies underutilized laptop
6. Views badge statistics showing engagement trends
7. Makes data-driven purchasing decisions
8. Recognizes top volunteers with most badges earned

---

## Summary

The Club-Collab database provides a comprehensive solution for managing university club activities, resources, and volunteer contributions. With 13 major feature categories, automated conflict prevention, real-time tracking, powerful analytics, and gamified volunteer recognition, it transforms chaotic manual processes into an efficient, data-driven system.


---

**Course**: CSE370 (Database Systems) - BRAC University  
**Status**: Production Ready  
**Version**: 1.0
