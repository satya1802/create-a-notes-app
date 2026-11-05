# Data Model

<!-- sdlc:auto:start entities -->
### users

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| email | citext | False | — | False |
| password_hash | text | False | — | False |
| email_verified | boolean | False | — | False |
| created_at | timestamptz | False | — | False |

### folders

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| user_id | uuid | False | users.id | False |
| name | text | False | — | False |
| created_at | timestamptz | False | — | False |

### notes

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| user_id | uuid | False | users.id | False |
| folder_id | uuid | False | folders.id | True |
| title | text | False | — | False |
| content | jsonb | False | — | False |
| content_text | text | False | — | False |
| search_vector | tsvector | False | — | True |
| version | integer | False | — | False |
| is_trashed | boolean | False | — | False |
| trashed_at | timestamptz | False | — | True |
| created_at | timestamptz | False | — | False |
| updated_at | timestamptz | False | — | False |

### password_reset_tokens

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| user_id | uuid | False | users.id | False |
| token_hash | text | False | — | False |
| expires_at | timestamptz | False | — | False |
| used_at | timestamptz | False | — | True |
<!-- sdlc:auto:end entities -->

<!-- sdlc:auto:start relationships -->
| Source | Target | Type |
|---|---|---|
| users | folders | one-to-many |
| users | notes | one-to-many |
| folders | notes | one-to-many |
| users | password_reset_tokens | one-to-many |
<!-- sdlc:auto:end relationships -->

<!-- sdlc:auto:start er-diagram -->
```mermaid
erDiagram
  users {
    uuid id PK
    citext email
    text password_hash
    boolean email_verified
    timestamptz created_at
  }
  folders {
    uuid id PK
    uuid user_id FK
    text name
    timestamptz created_at
  }
  notes {
    uuid id PK
    uuid user_id FK
    uuid folder_id FK
    text title
    jsonb content
    text content_text
    tsvector search_vector
    integer version
    boolean is_trashed
    timestamptz trashed_at
    timestamptz created_at
    timestamptz updated_at
  }
  password_reset_tokens {
    uuid id PK
    uuid user_id FK
    text token_hash
    timestamptz expires_at
    timestamptz used_at
  }
  users ||--o{ folders : "one-to-many"
  users ||--o{ notes : "one-to-many"
  folders ||--o{ notes : "one-to-many"
  users ||--o{ password_reset_tokens : "one-to-many"
```
<!-- sdlc:auto:end er-diagram -->
