# Nuzlocke-Tracker
This is an application where users can create an account to track Pokemon Nuzlocke runs

## CRUD Operations

### CREATE Operations

| **Component**     | **Backend (Express)**                | **Frontend (React)**                | **MongoDB Action**                                 |
|-------------------|-------------------------------------|------------------------------------|----------------------------------------------------|
| New Nuzlocke Run  | `POST /api/nuzlockes`               | Form submission → `axios.post()`   | `db.nuzlockes.insertOne()`                         |
| Add Pokémon       | `POST /api/nuzlockes/:id/pokemon`   | "Form with Pokémon select + nickname input → axios.post()` | `db.nuzlockes.updateOne()`   |
| User Registration | `POST /api/auth/register`           | Signup form → `axios.post()`       | `db.users.insertOne()`                             |

---

### READ Operations

| **Component**            | **Backend (Express)**               | **Frontend (React)**                 | **MongoDB Action**                       |
|--------------------------|------------------------------------|-------------------------------------|------------------------------------------|
| List Nuzlocke Runs       | `GET /api/nuzlockes`               | `useEffect` → `axios.get()`         | `db.nuzlockes.find()`                     |
| View Single Run          | `GET /api/nuzlockes/:id`           | Route params → `axios.get()`        | `db.nuzlockes.findOne()`                   |
| Fetch Pokémon (PokeAPI)  | `GET` PokeAPI endpoints            | Search → `axios.get()`              | N/A (External API)                        |

---

### UPDATE Operations

| **Component**            | **Backend (Express)**                       | **Frontend (React)**                    | **MongoDB Action**                                                 |
|--------------------------|--------------------------------------------|----------------------------------------|--------------------------------------------------------------------|
| Edit Run Details         | `PUT /api/nuzlockes/:id`                    | Form → `axios.put()`                    | `db.nuzlockes.updateOne()`                                          |
| Update Pokémon Status    | `PUT /api/nuzlockes/:id/pokemon/:pid`       | Click handler → `axios.put()`           | `db.nuzlockes.updateOne()` |
| Mark Badge Earned        | `PATCH /api/nuzlockes/:id/badges`           | Button → `axios.patch()`                | `db.nuzlockes.updateOne()`                   |

---

### DELETE Operations

| **Component**          | **Backend (Express)**                          | **Frontend (React)**                | **MongoDB Action**                                                  |
|------------------------|-----------------------------------------------|------------------------------------|--------------------------------------------------------------------|
| Delete Nuzlocke Run    | `DELETE /api/nuzlockes/:id`                    | Button → `axios.delete()`          | `db.nuzlockes.deleteOne()`                                         |
| Release Pokémon        | `DELETE /api/nuzlockes/:id/pokemon/:pid`       | Click → `axios.delete()`           | `db.nuzlockes.updateOne()`     |

id: is the specific nuzlocke run as we assume there will be many runs
pid: is the Pokemon's unique ID. This is in the case there will be duplicates of the same pokemon. 
