## Data Flow Diagram (DFD) for the Features and Functionalities

This document describes the data flow between external entities, backend processes, and data stores for the core operations of the platform.  

---

## External Entities
- **Guest**: A user who books properties, makes payments, and leaves reviews.  
- **Host**: A user who lists and manages properties.  
- **Admin**: A user who oversees the platform, manages users, and ensures system integrity.  

---

## Core Processes
1. **User Management**  
   - Handles secure registration, authentication, and profile management.  
   - Allows Guests, Hosts, and Admins to access and manage their accounts.  
   - Stores user data in the **User Database**.  

2. **Property Management**  
   - Allows Hosts to create, update, and retrieve property listings.  
   - Stores property details in the **Property Database**.  
   - Provides searchable listings for Guests.  

3. **Booking System**  
   - Enables Guests to make property reservations by specifying dates and booking details.  
   - Updates **Booking Records** to ensure availability and prevent conflicts.  
   - Sends booking-related payment requests to **Payment Processing**.  

4. **Payment Processing**  
   - Handles secure transactions using methods such as credit card or PayPal/Stripe.  
   - Stores payment confirmations and history in the **Payment Records** database.  
   - Ensures accountability and trust in the platform.  

5. **Review System**  
   - Allows Guests to submit reviews and ratings for properties.  
   - Stores feedback in the **Review Records** database.  
   - Links reviews to properties in the **Property Database** to inform future Guests.  

---

## Data Stores
- **User Database**: Contains registration details, authentication credentials, and user profiles.  
- **Property Database**: Stores property listings with descriptions, pricing, and availability.  
- **Booking Records**: Keeps reservation data to manage scheduling and avoid conflicts.  
- **Payment Records**: Tracks all payment transactions for accountability and reporting.  
- **Review Records**: Holds property feedback and ratings from Guests.  

---

## Data Flows
- Guests and Hosts interact with **User Management** for login and profile updates.  
- Hosts manage listings through **Property Management**, which updates the **Property Database**.  
- Guests book properties via the **Booking System**, which writes to **Booking Records** and requests payments.  
- The **Payment Processing** system updates **Payment Records** after successful transactions.  
- Guests submit reviews through the **Review System**, which stores them in **Review Records** and links to **Property Database** for visibility.  
- Admins manage user accounts through **User Management** to maintain platform integrity.  

