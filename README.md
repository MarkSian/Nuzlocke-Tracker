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


## Schema Draft:
### models/User.js

  username: {
    type: String,
    required: true,
    unique: true,
    trim: true,
    minlength: 3,
    maxlength: 30
  },
  email: {
    type: String,
    required: true,
    unique: true,
  },
  password: {
    type: String,
    required: true,
    minlength: 8
  },
  runs: [{
    type: Schema.Types.ObjectId,
    ref: 'Nuzlocke'
  }];

### models/Pokemon.js
  pokemonId: { 
    type: Number, 
    required: true,
    min: 1,
    max: 1025 
  },
  name: {
    type: String,
    required: true,
    lowercase: true
  },
  nickname: String,
  level: {
    type: Number,
    default: 5,
    min: 1,
    max: 100
  },
  metLocation: {
    type: String,
    required: true,
    enum: [
      'Route 101', 'Route 102', 'Dewford Town', 
      'Desert Underpass', 'Victory Road', // 
    ]
  },
  status: {
    type: String,
    required: true,
    enum: ['alive', 'dead', 'boxed'],
    default: 'alive'
  },
  sprite: {
    type: String,
    required: true,
  },
  types: {
    type: [String],
    required: true,
    enum: [
      'normal', 'fire', 'water', 'electric', 'grass',
      'ice', 'fighting', 'poison', 'ground', 'flying',
      'psychic', 'bug', 'rock', 'ghost', 'dragon',
      'dark', 'steel', 'fairy'
    ]
  },