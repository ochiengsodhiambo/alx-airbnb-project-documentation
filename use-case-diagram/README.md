## Use Case Diagram of the Airbnb Booking System

<img width="968" height="810" alt="image" src="https://github.com/user-attachments/assets/0f71c1ae-151e-4052-b913-445d8f3c1a44" />


This use case diagram illustrates the interactions between different users and the core functionalities of the system. The system boundary ("Airbnb Clone System") encapsulates all key processes such as user management, property management, booking, payments, messaging, reviews, notifications, and administration.

---

## Users
- **Guest**  
  - Can register, log in, manage their profile, search properties, make bookings, pay for reservations, submit reviews, message hosts, and receive notifications.  

- **Host**  
  - Can register, manage their profile, list and update properties, manage availability, communicate with guests, respond to reviews, and receive payouts.  

- **Admin**  
  - Oversees the entire platform via the Admin Dashboard.  
  - Manages users, properties, bookings, payments, reviews, and ensures moderation of content/messages.  

---

## Core Use Cases
### 1. User Management
- **Registration & Login**: Guests, Hosts, and Admins create accounts and access the system.  
- **Profile Management**: Users update personal details and upload profile photos.  

### 2. Property Management
- **Listing & Updates**: Hosts create and modify property listings with details such as location, price, and amenities.  
- **Availability & Retrieval**: Hosts manage calendars while Guests search/filter properties by availability, price, and amenities.  

### 3. Booking System
- **Create & Manage Bookings**: Guests book properties with start/end dates; bookings can be confirmed, canceled, or marked as completed.  
- **Price Calculation & Status**: Costs are dynamically calculated, and booking status is tracked (pending, confirmed, canceled, completed).  

### 4. Payments
- **Processing & Verification**: Guests pay via credit card, PayPal, or Stripe. The system validates payments before confirming bookings.  
- **Tracking & Payouts**: The system records transactions and automatically pays out to Hosts.  

### 5. Messaging
- **Communication**: Guests and Hosts exchange messages through in-app chat.  
- **Moderation**: Admins monitor communication to enforce community guidelines.  

### 6. Reviews
- **Submission & Retrieval**: Guests leave reviews and ratings; others can view aggregated feedback.  
- **Responses & Moderation**: Hosts reply to reviews; Admins moderate inappropriate content.  

### 7. Notifications
- **Delivery**: Email and in-app alerts notify users about booking confirmations, cancellations, and payment updates.  
- **Tracking**: Notifications can be marked as read/unread.  

### 8. Admin Dashboard
- **User, Property, Booking, Payment, and Review Management**: Admins oversee all activities, ensuring security, compliance, and fair use.  

