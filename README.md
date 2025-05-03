# airbnb-clone-project


## 📄 Description
The backend for the Airbnb Clone project provides a robust and scalable foundation for managing user interactions, property listings, bookings, and payments. It supports the essential functionalities required to replicate the core features of Airbnb, ensuring a smooth experience for both users and hosts.

---

## 🎯 Project Goals
- **User Management**  
  Implement a secure system for user registration, authentication, and profile management.

- **Property Management**  
  Develop features for property listing creation, updates, and retrieval.

- **Booking System**  
  Create a booking mechanism for users to reserve properties and manage booking details.

- **Payment Processing**  
  Integrate a payment system to handle transactions and record payment details.

- **Review System**  
  Allow users to leave reviews and ratings for properties.

- **Data Optimization**  
  Ensure efficient data retrieval and storage through database optimizations.

---

## 🛠️ Technology Stack

- **Backend Framework**
  - Django

- **API Development**
  - Django REST Framework (DRF).
  - GraphQL.

- **Database**
  - PostgreSQL.

- **Asynchronous Task Handling**
  - Celery.
  - Redis.

- **Containerization**
  - Docker.

- **DevOps**
  - CI/CD Pipelines.

---


## 👥 Team Roles
- **Backend Developer**  
  Responsible for implementing API endpoints, database schemas, and business logic.

- **Database Administrator**  
  Manages database design, indexing, and optimizations.

- **DevOps Engineer**  
  Handles deployment, monitoring, and scaling of the backend services.

- **QA Engineer**  
  Ensures the backend functionalities are thoroughly tested and meet quality standards.

---

## 🛠️ Technology Stack Overview
- **Backend Framework**
  - Django: High-level Python web framework for building RESTful APIs.

- **API Development**
  - Django REST Framework: Tools for creating and managing APIs.
  - GraphQL: Enables flexible and efficient data queries.

- **Database**
  - PostgreSQL: Relational database for reliable data storage.

- **Asynchronous Task Handling**
  - Celery: For managing background tasks like notifications and payment processing.
  - Redis: Used for caching and session management.

- **Containerization**
  - Docker: Provides a consistent development and production environment.

- **DevOps**
  - CI/CD Pipelines: Automated pipelines for testing and deploying code changes.
 
## 🗃️ Database Design

This document outlines the database schema for the Airbnb Clone project, detailing the key entities, their fields, and relationships.

### 🔑 Key Entities

### 1. 👥 Users
**Fields:**
- `id` (Primary Key) - *Unique identifier*
- `username` (Unique) - *User's handle*
- `email` (Unique) - *User's email*
- `password` (Hashed) - *Securely stored*
- `first_name` - *User's first name*
- `last_name` - *User's last name*
- `phone_number` - *Contact number*
- `profile_picture` - *URL to image*
- `is_host` (Boolean) - *Host status flag*
- `created_at` - *Account creation timestamp*
- `updated_at` - *Last update timestamp*

**Relationships:**
- 🏠 One-to-Many with Properties (A user can list multiple properties)
- 📅 One-to-Many with Bookings (A user can have multiple bookings)
- ⭐ One-to-Many with Reviews (A user can write multiple reviews)
- 💳 One-to-Many with Payments (A user can have multiple payment transactions)

### 2. 🏠 Properties
**Fields:**
- `id` (Primary Key)
- `host_id` (Foreign Key → Users)
- `title` - *Property name*
- `description` - *Detailed description*
- `property_type` (e.g., apartment, house, villa)
- `price_per_night` - *Nightly rate*
- `bedrooms` - *Number of bedrooms*
- `bathrooms` - *Number of bathrooms*
- `max_guests` - *Maximum occupancy*
- `country` - *Country location*
- `city` - *City location*
- `address` - *Full address*
- `latitude` - *GPS coordinate*
- `longitude` - *GPS coordinate*
- `amenities` (JSON array) - *["WiFi", "Pool", "Kitchen"]*
- `is_available` (Boolean) - *Listing status*
- `created_at` - *Listing creation time*
- `updated_at` - *Last update time*

**Relationships:**
- 👥 Many-to-One with Users (A property belongs to one host)
- 📅 One-to-Many with Bookings (A property can have multiple bookings)
- ⭐ One-to-Many with Reviews (A property can have multiple reviews)
- 🖼️ One-to-Many with PropertyImages (A property can have multiple images)

### 3. 🖼️ PropertyImages
**Fields:**
- `id` (Primary Key)
- `property_id` (Foreign Key → Properties)
- `image_url` - *URL of the image*
- `is_primary` (Boolean) - *Main image flag*
- `created_at` - *Upload timestamp*

**Relationships:**
- 🏠 Many-to-One with Properties (Images belong to a single property)

### 4. 📅 Bookings
**Fields:**
- `id` (Primary Key)
- `guest_id` (Foreign Key → Users)
- `property_id` (Foreign Key → Properties)
- `check_in_date` - *Start date*
- `check_out_date` - *End date*
- `total_price` - *Calculated booking cost*
- `status` (e.g., "pending", "confirmed", "cancelled")
- `num_guests` - *Number of guests*
- `special_requests` (Optional) - *Guest notes*
- `created_at` - *Booking creation time*
- `updated_at` - *Last update time*

**Relationships:**
- 👥 Many-to-One with Users (A booking belongs to a guest)
- 🏠 Many-to-One with Properties (A booking is for one property)
- 💳 One-to-One with Payments (Each booking has one payment)

### 5. 💳 Payments
**Fields:**
- `id` (Primary Key)
- `booking_id` (Foreign Key → Bookings)
- `user_id` (Foreign Key → Users)
- `amount` - *Payment amount*
- `payment_method` (e.g., "credit_card", "paypal")
- `transaction_id` (Unique) - *Payment processor reference*
- `status` (e.g., "pending", "completed", "failed")
- `payment_date` - *When payment occurred*
- `created_at` - *Record creation time*

**Relationships:**
- 📅 Many-to-One with Bookings (A payment is linked to one booking)
- 👥 Many-to-One with Users (A payment is made by one user)

### 6. ⭐ Reviews
**Fields:**
- `id` (Primary Key)
- `guest_id` (Foreign Key → Users)
- `property_id` (Foreign Key → Properties)
- `booking_id` (Foreign Key → Bookings)
- `rating` (1-5) - *Star rating*
- `comment` - *Written review*
- `created_at` - *Review submission time*
- `updated_at` - *Last edit time*

**Relationships:**
- 👥 Many-to-One with Users (A review is written by one user)
- 🏠 Many-to-One with Properties (A review is for one property)
- 📅 Many-to-One with Bookings (A review is linked to one booking)



## 🚀 Getting Started

### Prerequisites
- Python 3.9+
- Docker and Docker Compose
- PostgreSQL
- Redis

### Setup Instructions

1. Clone the repository:
   ```bash
   https://github.com/Muse-Semu/airbnb-clone-project.git
   cd airbnb-clone-backend

