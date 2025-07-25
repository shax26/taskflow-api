# TaskFlow - Developer API Documentation

Welcome to the **TaskFlow API** documentation. This guide provides all the information needed to interact with the backend services, covering authentication, user management, projects, tasks, comments, subtasks, and notifications.

---

## Base URL

```
http://localhost:5000/api
```

---

## Authentication & Authorization

### Register

**POST** `/auth/register`

- **Body:** `multipart/form-data`

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securePassword",
  "avatar": (image file)
}
```

- **Response:** Access token in body and Refresh token as httpOnly cookie

### Login

**POST** `/auth/login`

```json
{
  "email": "john@example.com",
  "password": "securePassword"
}
```

### Refresh Token

**POST** `/auth/refresh`

- Uses refresh token from cookie

### Logout

**POST** `/auth/logout`

- Clears refresh token cookie

---

## 👤 User Management

### Get All Users

**GET** `/users/`

- Protected: `admin`

### Get Single User

**GET** `/users/:id`

### Update User

**PUT** `/users/:id`

### Delete User

**DELETE** `/users/:id`

---

## Projects

### Create Project

**POST** `/projects/`

```json
{
  "name": "Project Alpha",              // Required: Project name
  "description": "Description...",      // Optional: Project description
  "owner": "userId",                    // Required: Owner user ID
  "team": ["userId1", "userId2"],      // Optional: Array of team member user IDs
  "color": "red",                      // Optional: Project color (default: "red")
  "status": "active",                  // Optional: Project status (default: "active")
  "priority": "medium",                // Optional: Project priority (default: "medium")
  "startDate": "2025-07-25T00:00:00.000Z", // Optional: Project start date (ISO string)
  "dueDate": "2025-08-25T00:00:00.000Z"    // Optional: Project due date (ISO string)
}
```

### Get User Projects

**GET** `/projects/`

### Get Single Project

**GET** `/projects/:id`

### Update Project

**PUT** `/projects/:id`

### Delete Project

**DELETE** `/projects/:id`

---

## Tasks

### Create Task

**POST** `/tasks/`

```json
{
  "title": "Create DB schema",
  "description": "...",
  "project": "projectId",
  "assignedTo": "userId",
  "dueDate": "2025-05-10"
}
```

### Get Project Tasks

**GET** `/tasks/project/:projectId`

### Update Task

**PUT** `/tasks/:id`

### Delete Task

**DELETE** `/tasks/:id`

---

## Subtasks

### Create Subtask

**POST** `/subtasks/`

```json
{
  "title": "Design schema",
  "task": "taskId",
  "createdBy": "userId"
}
```

### Get Subtasks by Task

**GET** `/subtasks/:taskId`

### Update Subtask

**PUT** `/subtasks/:id`

### Delete Subtask

**DELETE** `/subtasks/:id`

---

## Comments

### Create Comment

**POST** `/comments/`

```json
{
  "task": "taskId",
  "content": "This is a comment."
}
```

### Get Comments by Task

**GET** `/comments/task/:taskId`

### Delete Comment

**DELETE** `/comments/:id`

---

## Notifications

### Create Notification

**POST** `/notifications/`

```json
{
  "recipient": "userId",
  "message": "You have a new task."
}
```

### Get User Notifications

**GET** `/notifications/`

### Mark Notification as Read

**PATCH** `/notifications/:id/read`

### Delete Notification

**DELETE** `/notifications/:id`

---

## Middleware & Auth

- `protect`: Middleware to check authentication
- `restrictTo(...roles)`: Role-based access control
- `validateRequest`: Middleware to validate inputs via express-validator

---

## Testing

You can test endpoints using tools like:

- Postman
- Thunder Client (VSCode extension)
- cURL


## Final Note

This documentation will help you integrate or contribute to the Task Manager SaaS App API. For any issue, contact the maintainer or raise an issue in the repository.

Happy Coding!

