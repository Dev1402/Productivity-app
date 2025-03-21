Here's a **UML Data Model** for your matchmaking app, VibeMatch, structured to reflect the key entities and relationships in the system:

---

### 🔧 **Entities & Relationships**

```plaintext
+---------------------+
|      User           |
+---------------------+
| user_id : UUID      |
| name : String       |
| age : Integer       |
| gender : String     |
| location : String   |
| intent : Enum       |
| created_at : Date   |
| persona_id : UUID   |
+---------------------+
           |
           | 1
           |
           |------+
                  | N
           +----------------------+
           |     QuizResponse     |
           +----------------------+
           | response_id : UUID   |
           | user_id : UUID       |
           | question_id : UUID   |
           | answer : Text        |
           | timestamp : DateTime |
           +----------------------+

+----------------------+
|     QuizQuestion     |
+----------------------+
| question_id : UUID   |
| text : String        |
| type : Enum          |
| category : Enum      |
+----------------------+

+-------------------------+
|        Persona          |
+-------------------------+
| persona_id : UUID       |
| title : String          |
| description : Text      |
| vibe_score : Float      |
| vision_score : Float    |
| values_score : Float    |
| created_by_ai : Boolean |
+-------------------------+

+-----------------------+
|        Match          |
+-----------------------+
| match_id : UUID       |
| user_1_id : UUID      |
| user_2_id : UUID      |
| match_score : Float   |
| created_at : DateTime |
| status : Enum         | <-- ["Pending", "InGame", "Completed"]
+-----------------------+

+-------------------------+
|        GameSession      |
+-------------------------+
| session_id : UUID       |
| match_id : UUID         |
| game_id : UUID          |
| started_at : DateTime   |
| ended_at : DateTime     |
| score_user_1 : Float    |
| score_user_2 : Float    |
| outcome : String        |
+-------------------------+

+----------------------+
|        Game          |
+----------------------+
| game_id : UUID       |
| title : String       |
| description : Text   |
| type : Enum          | <-- ["ScenarioSwipe", "Alignment", "MemoryLane"]
+----------------------+

+--------------------------+
|     CompatibilityScore   |
+--------------------------+
| score_id : UUID          |
| session_id : UUID        |
| dimensions : JSON        | <-- {vibe: x, vision: y, values: z}
| insights : Text          |
+--------------------------+
```

---

### 🔁 **Relationships**

- `User` ⟶ `Persona` = Many-to-One
- `User` ⟶ `QuizResponse` = One-to-Many
- `QuizQuestion` ⟶ `QuizResponse` = One-to-Many
- `Match` ⟶ Two `User` references
- `Match` ⟶ `GameSession` = One-to-Many
- `GameSession` ⟶ `Game` = Many-to-One
- `GameSession` ⟶ `CompatibilityScore` = One-to-One

---

### 📦 Suggested PostgreSQL Enhancements
- Use `JSONB` for storing dynamic quiz answers or game result data.
- Add indexing on `user_id`, `match_score`, and `persona_id` for performance.
- Leverage triggers to recalculate match scores when new game sessions are completed.

---

Would you like this exported as an actual ER diagram image or schema.sql file for implementation?
