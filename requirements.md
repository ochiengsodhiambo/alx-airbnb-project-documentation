## Airbnb Clone – Backend Requirement Specifications

This document details the backend requirements for three core features: **User Authentication**, **Property Management**, and **Booking System**. 
It defines API endpoints, request/response contracts, validation rules, security and authorization, error handling, and performance criteria. 
The APIs follow REST principles under the base path **`/api/v1`** and exchange **JSON** unless noted.

---

##1) User Authentication

### 1.1 Goals
- Securely register, authenticate, and manage user sessions.
- Support roles: **guest**, **host**, **admin** (RBAC enforced via JWT claims).
- Provide password reset, email verification, OAuth login, and session refresh.

### 1.2 Data Model (minimum)
- **User**: `id (uuid)`, `email (unique)`, `password_hash`, `first_name`, `last_name`, `phone` (nullable), `role` (enum: guest|host|admin), `avatar_url` (nullable), `email_verified_at` (timestamp, nullable), `created_at`, `updated_at`.
- **Session/Token** (optional table if storing refresh tokens): `id`, `user_id`, `refresh_token_hash`, `expires_at`, `revoked_at`, `user_agent`, `ip`.
- **EmailVerification**: `user_id`, `token_hash`, `expires_at`, `consumed_at`.
- **PasswordReset**: `user_id`, `token_hash`, `expires_at`, `consumed_at`.

### 1.3 Security & AuthN/Z
- **JWT** access tokens (short-lived, e.g., 15 min), signed with RS256. Claims: `sub`, `role`, `iat`, `exp`.
- **Refresh tokens** (httpOnly, Secure cookies where feasible; otherwise in response body) with rotation and revocation.
- **Password hashing**: Argon2id (preferred) or bcrypt (min cost 12).
- **Rate limits**: Login/Register/Reset endpoints: **10 req/min/IP**; overall API: **100 req/min/IP** (tunable).
- **OAuth** (optional): Google & Facebook via `/auth/oauth/:provider`.
- **RBAC**: Middleware checks `role` for protected routes.
- **Brute-force protection**: Incremental backoff and account lock after N failed attempts (e.g., 5 failed in 15 min → 15-min lock).

### 1.4 Endpoints and Contracts

#### POST `/auth/register`
Registers a new user (guest by default, host if specified).
- **Body**
```json
{
  "email": "jane@example.com",
  "password": "P@ssw0rd!",
  "first_name": "Jane",
  "last_name": "Doe",
  "phone": "+254712345678",
  "role": "guest"  
}
```
- **Validation**
  - `email`: RFC 5322, unique, lowercase store.
  - `password`: ≥ 8 chars, 1 upper, 1 lower, 1 digit, 1 symbol.
  - `first_name`/`last_name`: 1–100 chars; letters, hyphen, space.
  - `role`: one of guest|host (admin creation via admin-only).
- **Responses**
  - `201 Created`
```json
{
  "user": {"id": "uuid", "email": "jane@example.com", "first_name": "Jane", "last_name": "Doe", "role": "guest", "email_verified": false},
  "tokens": {"access": "<jwt>", "refresh": "<token>"}
}
```

#### POST `/auth/login`
```json
{"email": "jane@example.com", "password": "P@ssw0rd!"}
```

#### POST `/auth/refresh`
Rotates refresh token.

#### POST `/auth/logout`
Revokes refresh token.

#### POST `/auth/password/forgot`
Request password reset.

#### POST `/auth/password/reset`
Reset password with token.

#### POST `/auth/verify-email`
Verify email with token.

#### GET `/me`
Get current user profile.

#### PATCH `/me`
Update user profile.

#### PATCH `/me/password`
Change password.

#### POST `/auth/oauth/:provider`
OAuth login.

---

## 2) Property Management

### 2.1 Goals
- CRUD for property listings by hosts; public retrieval and search.
- Image upload & management; amenities and availability.

### 2.2 Data Model (minimum)
- **Property**: `id (uuid)`, `host_id`, `title`, `description`, `type`, `address`, `lat`, `lng`, `city`, `country`, `nightly_price`, `currency`, `max_guests`, `bedrooms`, `beds`, `baths`, `amenities`, `rules`, `status`.
- **PropertyImage**: `id`, `property_id`, `url`, `position`, `is_cover`.
- **AvailabilityBlock**: `id`, `property_id`, `start_date`, `end_date`, `reason`.

### 2.3 Endpoints
- `POST /properties`
- `GET /properties/:id`
- `PATCH /properties/:id`
- `DELETE /properties/:id`
- `GET /properties` (filters & pagination)
- `POST /properties/:id/images`
- `DELETE /properties/:id/images/:imageId`
- `PUT /properties/:id/availability-blocks`

---

## 3) Booking System

### 3.1 Goals
- Allow guests to request and confirm bookings; prevent double-booking.
- Support quoting, pricing, taxes/fees, cancellation, and status transitions.

### 3.2 Data Model (minimum)
- **Booking**: `id`, `property_id`, `guest_id`, `host_id`, `check_in`, `check_out`, `nights`, `guests`, `currency`, `subtotal`, `fees`, `total`, `status`.
- **Payment**: `booking_id`, `provider`, `charge_id`, `amount`, `currency`, `status`.
- **Calendar**: derived from bookings + availability blocks.

### 3.3 Endpoints
- `POST /bookings/quote`
- `POST /bookings`
- `GET /bookings/:id`
- `GET /bookings`
- `PATCH /bookings/:id/cancel`
- `POST /bookings/:id/complete`

---

## 4) Performance & Non-Functional Requirements
- **Auth latency:** ≤ 150 ms p95.
- **Properties search latency:** ≤ 200 ms (cached), ≤ 350 ms (uncached).
- **Booking create latency:** ≤ 400 ms excluding external payment.
- **Throughput:** ≥ 20 bookings/sec sustained.
- **Availability:** 99.9% monthly uptime.
- **Security:** OWASP ASVS L2 compliance, TLS 1.2+, GDPR-ready.
