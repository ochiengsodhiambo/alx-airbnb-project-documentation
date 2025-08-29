## Key features and functionalities png
features and functionalities of the Airbnb Clone the backend needs to support
<img width="1786" height="918" alt="airbnb_backend_features_ _functionalities(1)" src="https://github.com/user-attachments/assets/c9d189c7-6239-4216-a740-5f4d89aeba7d" />

---
This document summarizes the **key functional modules** of the Airbnb Clone backend in a DBML-style diagram.  
Each module (shown as a table in DBML) represents a **core feature group** of the system, with sub-features listed as fields.  
References (arrows) describe how modules interact with each other.

---

## 1. User Management
Handles user accounts and authentication.
- **Registration**: Users sign up with email, password, and role (Guest, Host, or Admin).
- **Login**: Authentication via email/password or OAuth (Google, Facebook).
- **Roles**: Defines access levels (Guest, Host, Admin).
- **Profile Management**: Update personal information and upload profile photos.

---

## 2. Property Management
Hosts manage rental listings.
- **Listing**: Create new properties with title, description, location, price, and amenities.
- **Updates**: Modify listing details (tracked with timestamps).
- **Retrieval**: Search and filter by location, price, number of guests, or amenities.
- **Availability**: Manage calendars to prevent double bookings.

---

## 3. Booking System
Guests book properties and manage reservations.
- **Create Booking**: Select property and dates.
- **Manage Booking**: View, confirm, or cancel reservations.
- **Price Calculation**: Dynamic calculation: `(end_date - start_date) * price_per_night`.
- **Status**: Track booking as pending, confirmed, canceled, or completed.

---

## 4. Payments
Handles transactions between guests and hosts.
- **Processing**: Secure payments via credit card, PayPal, or Stripe.
- **Tracking**: Store details like amount, date, method, and currency.
- **Verification**: Confirm payments before booking approval.
- **Payouts**: Automatic transfers to hosts after booking completion.

---

## 5. Reviews
Guests and hosts exchange feedback.
- **Submission**: Guests leave ratings (1–5 stars) and comments.
- **Retrieval**: Display reviews and calculate average ratings.
- **Moderation**: Admins remove inappropriate reviews.
- **Responses**: Hosts can reply to guest reviews.

---

## 6. Messaging
Direct communication between guests and hosts.
- **Communication**: Send and receive messages.
- **Tracking**: Save message content and timestamps.
- **Moderation**: Admins monitor messages for abuse.

---

## 7. Notifications
Keeps users updated with system events.
- **Delivery**: Email and in-app notifications.
- **Types**: Booking confirmations, cancellations, and payment updates.
- **Tracking**: Notifications marked as read or unread.

---

## 8. Admin Dashboard
Admin-level control and monitoring.
- **User Management**: Oversee and manage user accounts.
- **Property Management**: Review and remove listings.
- **Booking Management**: Track and manage reservations.
- **Payment Management**: Monitor transactions.
- **Review Management**: Moderate reviews and messages.

---

## 9. Interactions (References)
Arrows in DBML describe relationships:
- A registered **User** can **book properties** and **send messages**.
- **Bookings** require **payments** and can generate **reviews**.
- **Property listings** are tied to **bookings** and **reviews**.
- **Payments** and **Bookings** trigger **notifications**.
- The **Admin Dashboard** oversees all modules (users, properties, bookings, payments, and reviews).
