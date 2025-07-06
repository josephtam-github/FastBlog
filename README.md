# FastBlog

A RESTful API for a simple blog application with features like creating, updating, deleting, and fetching blog posts. FastBlog adheres to REST principles, uses proper HTTP methods, and implements robust error handling.

---

## Features

- User registration, login, logout, and JWT authentication  
- User profile with avatar upload and bio  
- Create, update, delete, and view blog posts  
- Post categories and comments  
- Like functionality for posts  
- Permissions for post authorship  
- Built with Django, Django REST Framework, and JWT  

---

## Table of Contents

- [Project Structure](#project-structure)
- [Installation](#installation)
- [Configuration](#configuration)
- [API Endpoints](#api-endpoints)
- [Authentication](#authentication)
- [Usage Examples](#usage-examples)
- [Contributing](#contributing)
- [License](#license)

---

## Project Structure

```
FastBlog/
├── config/              # Django project settings, URLs, entrypoints (ASGI/WSGI)
├── users/               # User management: models, views, serializers, forms, URLs
├── posts/               # Blog post logic: models, views, serializers, permissions, URLs
├── manage.py            # Django project manager
```

### Key Files and Their Roles

- **config/settings.py:** Project settings (apps, middleware, database, JWT, CORS, etc.)
- **config/urls.py:** Root URL configuration, includes users and posts app URLs
- **users/models.py:** Custom user and profile models (using email for login)
- **users/views.py:** Registration, login, logout, user info/profile/avatar endpoints
- **users/urls.py:** User-related API endpoints (register, login, profile, etc.)
- **users/forms.py:** User creation/change forms for Django admin
- **posts/serializers.py:** Serializers for categories, posts, comments (read/write)
- **posts/permissions.py:** Custom permissions to restrict post editing to authors
- **posts/apps.py:** AppConfig for posts app
- **posts/urls.py:** Post-related API endpoints (CRUD, like, categories, comments)

---

## Installation

1. **Clone the repository:**
   ```sh
   git clone https://github.com/josephtam-github/FastBlog.git
   cd FastBlog
   ```

2. **Create a virtual environment and activate it:**
   ```sh
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```sh
   pip install -r requirements.txt
   ```

4. **Set up the database:**
   - By default, uses PostgreSQL. Update `DATABASES` in `config/settings.py` if needed.

5. **Run migrations:**
   ```sh
   python manage.py migrate
   ```

6. **Create a superuser (admin):**
   ```sh
   python manage.py createsuperuser
   ```

7. **Run the development server:**
   ```sh
   python manage.py runserver
   ```

---

## Configuration

- **Environment Variables:** (optional, for production)
  - `SECRET_KEY`: Django secret key
  - `DATABASE_URL`: Database connection string
  - `ALLOWED_HOSTS`: List of allowed hosts
- **CORS:** CORS middleware is enabled for API access.
- **JWT:** Uses SimpleJWT for authentication (`rest_framework_simplejwt`).

---

## API Endpoints

### User Endpoints

| Method | Endpoint                    | Description                   |
|--------|-----------------------------|-------------------------------|
| POST   | `/register/`                | Register a new user           |
| POST   | `/login/`                   | Obtain JWT tokens             |
| POST   | `/logout/`                  | Logout user                   |
| POST   | `/token/refresh/`           | Refresh JWT access token      |
| GET/PUT| `/profile/`                 | User profile info/update      |
| GET/PUT| `/profile/avatar/`          | User avatar upload/update     |
| GET/PUT| `/`                         | Get/update user info          |

### Post & Category Endpoints

| Method | Endpoint                          | Description                   |
|--------|-----------------------------------|-------------------------------|
| GET    | `/post/`                          | List all posts                |
| POST   | `/post/`                          | Create a new post             |
| GET    | `/post/<id>/`                     | Retrieve a post               |
| PUT    | `/post/<id>/`                     | Update a post (author only)   |
| DELETE | `/post/<id>/`                     | Delete a post (author only)   |
| POST   | `/post/like/<id>/`                | Like/unlike a post            |
| GET    | `/post/categories/`               | List all categories           |
| GET    | `/post/<post_id>/comment/`        | List comments for a post      |
| POST   | `/post/<post_id>/comment/`        | Add a comment                 |

> For a complete set, see the [users/urls.py](https://github.com/josephtam-github/FastBlog/blob/master/users/urls.py) and [posts/urls.py](https://github.com/josephtam-github/FastBlog/blob/master/posts/urls.py).

---

## Authentication

- JWT-based authentication via SimpleJWT.
- Register, then login to receive `access` and `refresh` tokens.
- Add `Authorization: Bearer <access_token>` header to authorize requests.

---

## Usage Examples

**Register:**
```http
POST /register/
{
  "email": "user@example.com",
  "username": "myuser",
  "password": "password123"
}
```

**Login:**
```http
POST /login/
{
  "email": "user@example.com",
  "password": "password123"
}
```

**Get Posts:**
```http
GET /post/
Authorization: Bearer <access_token>
```

---

## Contributing

1. Fork this repository  
2. Create a feature branch (`git checkout -b feature/your-feature`)  
3. Commit your changes (`git commit -am 'Add some feature'`)  
4. Push to the branch (`git push origin feature/your-feature`)  
5. Open a Pull Request  

---

## License

MIT

---

**Note:** This README is based on available repository files and may be incomplete. For the full file structure and latest updates, visit the [FastBlog repository](https://github.com/josephtam-github/FastBlog).