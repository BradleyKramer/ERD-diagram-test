```mermaid
erDiagram

    profiles {
        int id PK
        string full_name
        string email
        datetime created_at
        datetime updated_at
    }

    user_roles {
        int id PK
        int user_id FK
        string role
        datetime created_at
    }

    destinations {
        int id PK
        string name
        string country
        string region
        string image_url
        datetime created_at
        datetime updated_at
    }

    template_event {
        int id PK
        string name
        string description
        string type
        int duration
        int destination_id FK
        string default_time
        datetime created_at
        datetime updated_at
    }

    trips {
        int id PK
        int user_id FK
        string destination
        string itinerary_title
        string trip_dates
        string status
        datetime created_at
        datetime updated_at
        date start_date
        int num_days
        string itinerary_type
        json itinerary_data
    }

    events {
        int id PK
        int trip_id FK
        string title
        date date
        string location
        int capacity
        string description
        datetime created_at
        datetime updated_at
    }

    %% RELATIONSHIPS
    profiles ||--o{ user_roles : has
    profiles ||--o{ trips : has
    destinations ||--o{ template_event : has
    trips ||--o{ events : has
```


### Admin CRUD Matrix

| Entity          | Create | Read | Update | Delete |
|-----------------|:------:|:----:|:------:|:------:|
| profiles        |   ✖    |  ✔   |   ✔    |   ✖    |
| user_roles      |   ✔    |  ✔   |   ✔    |   ✔    |
| destinations    |   ✔    |  ✔   |   ✔    |   ✔    |
| template_event  |   ✔    |  ✔   |   ✔    |   ✔    |
| trips           |   ✔    |  ✔   |   ✔    |   ✔    |
| events          |   ✔    |  ✔   |   ✔    |   ✔    |

### User CRUD Matrix

| Entity          | Create | Read | Update | Delete |
|-----------------|:------:|:----:|:------:|:------:|
| profiles        |   ✖    |  ✔   |   ✔    |   ✖    |
| user_roles      |   ✖    |  ✖   |   ✖    |   ✖    |
| destinations    |   ✖    |  ✔   |   ✖    |   ✖    |
| template_event  |   ✖    |  ✔   |   ✖    |   ✖    |
| trips           |   ✔    |  ✔   |   ✔    |   ✔    |
| events          |   ✔    |  ✔   |   ✔    |   ✔    |


```mermaid
flowchart TD

    %% --- ROLES ---
    A[Admin]:::role
    U[User]:::role

    %% --- ENTITIES ---
    P[profiles]:::entity
    R[user_roles]:::entity
    D[destinations]:::entity
    T[template_event]:::entity
    TR[trips]:::entity
    E[events]:::entity

    %% --- ADMIN CRUD ---
    A -->|C✖ R✔ U✔ D✖| P
    A -->|C✔ R✔ U✔ D✔| R
    A -->|C✔ R✔ U✔ D✔| D
    A -->|C✔ R✔ U✔ D✔| T
    A -->|C✔ R✔ U✔ D✔| TR
    A -->|C✔ R✔ U✔ D✔| E

    %% --- USER CRUD ---
    U -->|C✖ R✔ U✔ D✖| P
    U -->|C✖ R✖ U✖ D✖| R
    U -->|C✖ R✔ U✖ D✖| D
    U -->|C✖ R✔ U✖ D✖| T
    U -->|C✔ R✔ U✔ D✔| TR
    U -->|C✔ R✔ U✔ D✔| E

    %% --- STYLES ---
    classDef role fill:#5DADE2,stroke:#1B4F72,stroke-width:2px,color:white;
    classDef entity fill:#FDEBD0,stroke:#B7950B,stroke-width:2px;
```


### App Screen Matrix — CRUD Operations Mapped to Screens

| Entity          | Create (C)                         | Read (R)                                  | Update (U)                                | Delete (D)                                |
|-----------------|------------------------------------|--------------------------------------------|--------------------------------------------|--------------------------------------------|
| **profiles**    | —                                  | Profile Page                               | Profile Edit Page                          | —                                          |
| **user_roles**  | Admin Panel → Manage Roles          | Admin Panel → Manage Roles                 | Admin Panel → Manage Roles                 | Admin Panel → Manage Roles                 |
| **destinations**| Admin Panel → Add Destination       | Home Page / Explore Destinations Page      | Admin Panel → Edit Destination             | Admin Panel → Manage Destinations          |
| **template_event** | Admin Panel → Add Template Event | Admin Panel → Template Event Library       | Admin Panel → Edit Template Event          | Admin Panel → Template Event Library       |
| **trips**       | Create Trip Screen                 | Trips List → Trip Detail Page              | Trip Edit Page                             | Trip Settings → Delete Trip                |
| **events**      | Trip Itinerary Page → Add Event    | Trip Itinerary Page                        | Event Edit Modal / Edit Event Page         | Trip Itinerary Page → Remove Event         |

