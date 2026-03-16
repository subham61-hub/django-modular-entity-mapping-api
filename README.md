# Django Modular Entity Mapping API

A modular Django REST Framework backend built with `APIView` only for managing master entities and their hierarchical mappings.

This repository demonstrates:

- Clean Django app modularization
- Manual DRF API implementation using `APIView`
- Serializer-based validation
- Foreign key mapping logic
- Swagger and ReDoc API documentation
- A protected web workspace on top of the APIs

---

## Features

### Master Entities

- Vendor
- Product
- Course
- Certification

Each master entity is implemented as a separate Django app.

### Mapping Relationships

- Vendor -> Product
- Product -> Course
- Course -> Certification

Each relationship is handled through its own mapping app.

### Bonus Features Included

- Soft delete using `is_active`
- Shared abstract base model
- Reusable object fetch utility
- Standardized API error responses
- Logging for API actions
- Seed data command
- Nested tree API
- Login-protected workspace UI
- Unit tests

---

## Project Architecture

```text
Vendor
   |
   v
Product
   |
   v
Course
   |
   v
Certification
```

Mappings enforce validation rules to maintain data integrity.

---

## Apps Structure

### Master Apps

```text
vendor
product
course
certification
```

### Mapping Apps

```text
vendor_product_mapping
product_course_mapping
course_certification_mapping
```

Each app contains:

```text
models.py
serializers.py
views.py
urls.py
admin.py
```

---

## Tech Stack

| Technology | Purpose |
| --- | --- |
| Django | Backend framework |
| Django REST Framework | API development |
| APIView | Manual API implementation |
| drf-yasg | Swagger/ReDoc documentation |
| SQLite | Development database |
| HTML/CSS/JavaScript | Workspace UI |

---

## Recommended Repository Name

```text
django-modular-entity-mapping-api
```

---

## Suggested Repository Structure

```text
django-modular-entity-mapping-api
|
|-- config
|-- vendor
|-- product
|-- course
|-- certification
|-- vendor_product_mapping
|-- product_course_mapping
|-- course_certification_mapping
|-- common
|-- templates
|-- static
|-- requirements.txt
|-- manage.py
|-- README.md
|-- .gitignore
```

---

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/django-modular-entity-mapping-api.git
cd django-modular-entity-mapping-api
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it:

Windows

```bash
venv\Scripts\activate
```

macOS/Linux

```bash
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### 5. Seed sample data

```bash
python manage.py seed_data
```

### 6. Create superuser

```bash
python manage.py createsuperuser
```

### 7. Run the server

```bash
python manage.py runserver
```

Server URL:

```text
http://127.0.0.1:8000/
```

---

## Login-Protected Workspace

- Login: `http://127.0.0.1:8000/login/`
- Workspace: `http://127.0.0.1:8000/workspace/`
- Demo user:
  - Username: `demo_admin`
  - Password: `demo12345`

The workspace includes:

- Search
- Pagination
- Modal-based editing
- Analytics cards
- CRUD management panels

---

## API Endpoints

### Vendor APIs

```text
GET    /api/vendors/
POST   /api/vendors/
GET    /api/vendors/<id>/
PUT    /api/vendors/<id>/
PATCH  /api/vendors/<id>/
DELETE /api/vendors/<id>/
```

### Product APIs

```text
GET    /api/products/
POST   /api/products/
GET    /api/products/<id>/
PUT    /api/products/<id>/
PATCH  /api/products/<id>/
DELETE /api/products/<id>/
```

### Course APIs

```text
GET    /api/courses/
POST   /api/courses/
GET    /api/courses/<id>/
PUT    /api/courses/<id>/
PATCH  /api/courses/<id>/
DELETE /api/courses/<id>/
```

### Certification APIs

```text
GET    /api/certifications/
POST   /api/certifications/
GET    /api/certifications/<id>/
PUT    /api/certifications/<id>/
PATCH  /api/certifications/<id>/
DELETE /api/certifications/<id>/
```

### Mapping APIs

```text
GET    /api/vendor-product-mappings/
POST   /api/vendor-product-mappings/
GET    /api/vendor-product-mappings/<id>/
PUT    /api/vendor-product-mappings/<id>/
PATCH  /api/vendor-product-mappings/<id>/
DELETE /api/vendor-product-mappings/<id>/
```

```text
GET    /api/product-course-mappings/
POST   /api/product-course-mappings/
GET    /api/product-course-mappings/<id>/
PUT    /api/product-course-mappings/<id>/
PATCH  /api/product-course-mappings/<id>/
DELETE /api/product-course-mappings/<id>/
```

```text
GET    /api/course-certification-mappings/
POST   /api/course-certification-mappings/
GET    /api/course-certification-mappings/<id>/
PUT    /api/course-certification-mappings/<id>/
PATCH  /api/course-certification-mappings/<id>/
DELETE /api/course-certification-mappings/<id>/
```

### Nested Tree API

```text
GET /api/vendor-products-tree/
GET /api/vendor-products-tree/?vendor_id=1
```

---

## Query Parameter Filtering

Examples:

```text
/api/products/?vendor_id=1
/api/courses/?product_id=2
/api/certifications/?course_id=3
```

---

## Validation Rules

The project enforces:

- Required field validation
- Unique `code` for master entities
- Duplicate mapping prevention
- Valid foreign key usage
- Only one `primary_mapping=True` per parent

Example:

A vendor cannot have multiple products marked as `primary_mapping=True`.

---

## Standard Error Response

Errors follow a consistent structure:

```json
{
  "success": false,
  "message": "Validation failed.",
  "errors": {
    "code": ["Vendor with this code already exists."]
  }
}
```

---

## API Documentation

- Swagger UI: `/swagger/`
- ReDoc: `/redoc/`

Documentation includes:

- Request body schemas
- Response schemas
- Query parameters
- Error responses

---

## Testing

Run the tests with:

```bash
python manage.py test vendor vendor_product_mapping
```

Covered examples:

- Create vendor
- Standard 404 error shape
- Soft delete behavior
- Nested tree API response
- Duplicate mapping validation
- Single primary mapping validation

---

## Learning Outcomes

This project demonstrates:

- Modular Django architecture
- DRF APIView implementation
- Serializer validation logic
- Complex entity relationships
- Manual API design without routers
- Professional project packaging for GitHub

---

## Author

Developed by **Subham Singh**
