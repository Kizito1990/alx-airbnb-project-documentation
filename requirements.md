

 1. User Authentication
Description
Manages registration, login, profile update, and secure session management for users (guests or hosts).

API Endpoints
Method	Endpoint	Description
POST	/api/register/	Register a new user
POST	/api/login/	Authenticate user
GET	/api/profile/	Get logged-in user profile
PUT	/api/profile/	Update user profile

Input/Output Specs
Register:

Input: email, password, full_name, user_type (guest/host)

Output: access_token, user_id

Login:

Input: email, password

Output: access_token, user_id, profile

Validation Rules
Email must be unique and in valid format

Password must be at least 8 characters

User type must be either guest or host

Performance Criteria
Token generation must take less than 300ms

Rate limiting: Max 5 login attempts per minute per IP

 2. Property Management
Description
Hosts can add, edit, delete, or retrieve listings. Guests can search and view property details.

API Endpoints
Method	Endpoint	Description
POST	/api/properties/	Add new property
GET	/api/properties/	List all properties
GET	/api/properties/<id>	View a single property
PUT	/api/properties/<id>	Edit property details
DELETE	/api/properties/<id>	Remove property (host only)

Input/Output Specs
Add Property:

Input: title, description, location, price, images[], amenities[], available_from, available_to

Output: property_id, status

Retrieve Property:

Output: JSON object of property details

Validation Rules
Title must be between 5–100 characters

Price must be a positive float

Images must be under 2MB each (JPG/PNG)

Dates must be future dates and logically valid

Performance Criteria
Property listing must return within 700ms

API should support pagination and filtering (by location, price, amenities) 
3. Booking System Description

Allows guests to book properties, manage bookings, and view booking history.

API Endpoints
Method	Endpoint	Description
POST	/api/bookings/	Create a new booking
GET	/api/bookings/	Get user’s bookings
GET	/api/bookings/<id>	Booking detail
DELETE	/api/bookings/<id>	Cancel booking (if allowed)

Input/Output Specs
Create Booking:

Input: property_id, start_date, end_date, guest_count

Output: booking_id, status, payment_link

Cancel Booking:

Input: booking_id

Output: status, message

Validation Rules
Booking dates must not overlap existing bookings

Guests cannot book their own property

Cannot cancel booking less than 24hrs before check-in

Performance Criteria
Booking confirmation must complete in < 500ms

System must prevent double bookings via locking or validation
