# Booking Application Project

This is a clone of a booking platform like Airbnb to learn more about full-stack development, focusing on backend systems, database design, API development, and application security under the context of ALX ProDev Backend program.

The main goal is to understand complex architectures and workflows.

## Team Roles

**Backend Developer**  

- Builds APIs with Django/DRF  
- Handles authentication  
- Integrates payment/maps APIs  

**Database Admin**  

- Designs PostgreSQL schema  
- Optimizes queries  
- Manages migrations  

**DevOps Engineer**  

- Sets up CI/CD (GitHub Actions)  
- Manages Docker containers  
- Monitors performance  

**QA Tester**  

- Writes automated tests  
- Checks security vulnerabilities  
- Ensures code quality  

## Technology Stack

This project will be using:

**Backend**  

- Django + DRF (REST APIs)  
- PostgreSQL (database)  
- Redis (caching)  

**Services**  

- Stripe (payments)  
- Google Maps (locations)  
- SendGrid (emails)

## Database Design

The database follows a relational model with these core entities:

### 1. Users

**Fields:**

- `id` (Primary Key)
- `email` (Unique)
- `password_hash`
- `first_name`
- `last_name`
- `role` (Host/Guest/Admin)

**Relationships:**

- One-to-Many with Properties (A user can list multiple properties)
- One-to-Many with Bookings (A user can make multiple bookings)
- One-to-Many with Reviews (A user can write multiple reviews)

### 2. Properties

**Fields:**

- `id` (Primary Key)
- `title`
- `description`
- `price_per_night`
- `bedrooms`
- `bathrooms`
- `host_id` (Foreign Key → Users)

**Relationships:**

- Many-to-One with Users (Each property belongs to one host)
- One-to-Many with Bookings (A property can have multiple bookings)
- One-to-Many with Reviews (A property can receive multiple reviews)
- Many-to-Many with Amenities (Through a junction table)

### 3. Bookings

**Fields:**

- `id` (Primary Key)
- `start_date`
- `end_date`
- `total_price`
- `status` (Confirmed/Pending/Cancelled)
- `guest_id` (Foreign Key → Users)
- `property_id` (Foreign Key → Properties)

**Relationships:**

- Many-to-One with Users (Each booking belongs to one guest)
- Many-to-One with Properties (Each booking is for one property)
- One-to-One with Payments (Each booking has one payment record)

### 4. Reviews

**Fields:**

- `id` (Primary Key)
- `rating` (1-5)
- `comment`
- `created_at`
- `guest_id` (Foreign Key → Users)
- `property_id` (Foreign Key → Properties)

**Relationships:**

- Many-to-One with Users (Each review is written by one user)
- Many-to-One with Properties (Each review is for one property)

### 5. Payments

**Fields:**

- `id` (Primary Key)
- `amount`
- `payment_method`
- `transaction_id`
- `status`
- `booking_id` (Foreign Key → Bookings)

**Relationships:**

- One-to-One with Bookings (Each payment processes one booking)

### 6. Amenities

**Fields:**

- `id` (Primary Key)
- `name` (WiFi, Pool, Kitchen etc.)
- `icon`

**Relationships:**

- Many-to-Many with Properties (Through PropertyAmenities junction table)

### 7. PropertyImages

**Fields:**

- `id` (Primary Key)
- `image_url`
- `is_primary`
- `property_id` (Foreign Key → Properties)

**Relationships:**

- Many-to-One with Properties (A property can have multiple images)

## Feature Breakdown

1. **User Accounts**  
   - Signup/login  
   - Host/guest roles  

2. **Property Listings**  
   - Add/edit listings  
   - Search/filter  

3. **Bookings**  
   - Date selection  
   - Payment processing  

4. **Reviews**  
   - Ratings system  
   - Host responses  

## API Security

- JWT authentication  
- Rate limiting  
- Data encryption  
- Regular audits  

## CI/CD Pipeline

### Overview

Our CI/CD (Continuous Integration/Continuous Deployment) pipeline automates testing and deployment to ensure:  

- Faster release cycles with fewer bugs  
- Consistent environments from development to production  
- Quick rollback capabilities if issues arise  

### Implementation

#### Tools & Services

- **GitHub Actions**: Primary CI/CD orchestration  
- **Docker**: Containerization for reproducible builds  
- **AWS CodeDeploy**/**Heroku**: Deployment targets  
- **Sentry**: Error monitoring in production  
