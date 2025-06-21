---
tags:
  - api
parent: "[[Application Programming Interface]]"
type: Permanent Note
deeper: 
against:
---
### ✅ **1. GET**
- **Purpose:** Retrieve data from the server.
- **Example:** `GET /users/123`
- **Safe:** ✅ (doesn’t change anything)
- **Idempotent:** ✅ (multiple calls = same result)
---
### ✅ **2. POST**
- **Purpose:** Submit data to the server to create a new resource.
- **Example:** `POST /users` (with user data in the body)
- **Safe:** ❌
- **Idempotent:** ❌ (calling it twice may create two users)
---
### ✅ **3. PUT**
- **Purpose:** Update an existing resource or create it if it doesn’t exist (replace).
- **Example:** `PUT /users/123` (with updated data)
- **Safe:** ❌
- **Idempotent:** ✅ (same request = same result)
---
### ✅ **4. PATCH**
- **Purpose:** Partially update a resource.
- **Example:** `PATCH /users/123` (update only email or name)
- **Safe:** ❌
- **Idempotent:** ✅ (usually) 
---
### ✅ **5. DELETE**
- **Purpose:** Delete a resource from the server.
- **Example:** `DELETE /users/123`
- **Safe:** ❌
- **Idempotent:** ✅ (deleting twice = still deleted)
___
### CRUD OPERATIONS:
| HTTP Method | CRUD Equivalent | Typical SQL |
| ----------- | --------------- | ----------- |
| `POST`      | Create          | `INSERT`    |
| `GET`       | Read            | `SELECT`    |
| `PUT/PATCH` | Update          | `UPDATE`    |
| `DELETE`    | Delete          | `DELETE`    |
___
## 🔒 What does **safe** mean?

> A request is **safe** if it **doesn’t change any data** on the server — it's read-only.
