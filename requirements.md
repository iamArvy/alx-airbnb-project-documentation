# 📄 Backend Feature Requirements – Airbnb Clone

This document outlines the detailed backend requirements for three core features of the Airbnb Clone project: **User Authentication**, **Property Management**, and **Booking System**.

Each feature includes API endpoint details, request/response formats, validation rules, and performance expectations.

---

## 🔐 1. User Authentication

### ✅ Functional Requirements
- Users (Guests/Hosts) must be able to register, log in, and retrieve/update their profile.
- JWT-based token authentication.
- OAuth (Google, Facebook) is optional.

### 📌 Endpoints

#### `POST /api/auth/register`
Registers a new user.

**Request Body:**
```json
{
  "full_name": "Jane Doe",
  "email": "jane@example.com",
  "password": "securePassword123",
  "role": "guest" // or "host"
}
```

**Validation Rules:**
- `email`: must be unique, valid format.
- `password`: minimum 8 characters.
- `role`: must be one of `guest`, `host`.

**Response:**
```json
{
  "message": "User registered successfully",
  "token": "jwt_token_here"
}
```

#### `POST /api/auth/login`
Authenticates a user.

**Request Body:**
```json
{
  "email": "jane@example.com",
  "password": "securePassword123"
}
```

**Response:**
```json
{
  "message": "Login successful",
  "token": "jwt_token_here",
  "user": {
    "id": "uuid",
    "full_name": "Jane Doe",
    "role": "guest"
  }
}
```

### ⚙️ Performance Criteria
- Authentication requests must be processed in <500ms.
- Passwords must be hashed using bcrypt or Argon2.

---

## 🏠 2. Property Management

### ✅ Functional Requirements
- Hosts must be able to create, update, delete, and view property listings.
- Listings include title, description, location, images, amenities, price, and availability.

### 📌 Endpoints

#### `POST /api/properties`
Create a new property (host only, auth required).

**Request Body:**
```json
{
  "title": "Cozy Apartment",
  "description": "Modern space with city view",
  "location": "Lagos, Nigeria",
  "price_per_night": 45000,
  "amenities": ["WiFi", "Air Conditioning"],
  "availability": {
    "start_date": "2025-07-01",
    "end_date": "2025-12-31"
  },
  "images": ["image1.jpg", "image2.jpg"]
}
```

**Validation Rules:**
- `price_per_night`: must be a positive number.
- `availability`: valid date range.
- `images`: must be valid image file references.

**Response:**
```json
{
  "message": "Property created",
  "property_id": "uuid"
}
```

#### `PUT /api/properties/:id`
Update a property (host only).

#### `GET /api/properties`
List all properties (search & filter supported).

### ⚙️ Performance Criteria
- Property listing search must support pagination and return in <700ms.
- File storage for images must use asynchronous uploads.

---

## 📅 3. Booking System

### ✅ Functional Requirements
- Guests can book properties based on availability.
- Hosts can view/manage incoming bookings.
- System must prevent double bookings.

### 📌 Endpoints

#### `POST /api/bookings`
Create a new booking (guest only).

**Request Body:**
```json
{
  "property_id": "uuid",
  "check_in": "2025-08-10",
  "check_out": "2025-08-15",
  "guests": 2
}
```

**Validation Rules:**
- `check_in < check_out`
- Dates must fall within property availability.
- Prevent overlap with existing bookings.

**Response:**
```json
{
  "message": "Booking successful",
  "booking_id": "uuid",
  "status": "pending"
}
```

#### `GET /api/bookings`
- Authenticated users retrieve their bookings.

#### `DELETE /api/bookings/:id`
- Allow cancelation within allowed policy.

### ⚙️ Performance Criteria
- Booking overlap check must complete within <300ms.
- Caching frequently accessed availability using Redis.

---

## 📦 General Notes

- All endpoints return standard error format:
```json
{
  "error": "Validation failed",
  "details": ["password is too short", "email already exists"]
}
```

- All protected routes require Bearer Token authentication.

- Logging and monitoring via centralized middleware for:
  - User login attempts
  - Booking errors
  - Payment failures

---
