# 🗂️ Airbnb Clone Backend – Use Case Diagram

## 📌 Overview
This folder contains the **Use Case Diagram** for the **Airbnb Clone Backend** project. It visualizes the main interactions between system users (actors) and the backend system functionalities.

The diagram was created using **Draw.io (diagrams.net)** and provides a high-level view of the system's behavior in terms of user goals.

---

## 👥 Actors

### 1. **Guest**
- Registers and logs in
- Searches for properties
- Books properties
- Makes payments
- Manages their profile
- Leaves reviews

### 2. **Host**
- Registers and logs in
- Creates and manages listings
- Manages bookings
- Responds to reviews
- Manages their profile

### 3. **Admin**
- Monitors the system
- Manages users
- Moderates content

---

## 🧩 Key Use Cases

| Use Case            | Description                                                  |
|---------------------|--------------------------------------------------------------|
| Register/Login      | Authenticates users (JWT, OAuth)                             |
| Manage Profile      | Users update personal information and preferences            |
| Search Listings     | Guests search properties using filters                       |
| Book Property       | Guests book listings for selected dates                      |
| Make Payment        | Handles payments via gateway integrations (Stripe, PayPal)   |
| Create Listing      | Hosts add properties with details and availability           |
| Manage Listings     | Hosts edit or delete their property listings                 |
| Manage Bookings     | Hosts and guests view or cancel bookings                     |
| Leave Review        | Guests review stays, hosts respond                           |
| System Monitoring   | Admin reviews system status and analytics                    |
| User Management     | Admin manages user accounts                                  |
| Content Moderation  | Admin oversees listing content and reviews                   |

---

## Use case diagram
[Use Case Diagram](./use-case-diagram.png)