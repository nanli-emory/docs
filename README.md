# Study Management for CaMicroscope
## Entities Definition

### Study

**Definition:**
A study is a collection of slides or annotations, in which users/pathologists examine and analyze WSI or ROI to make annotations and/or evaluations for a medical specialty. The studies could be assigned to multiple users/pathologists. The studies could be a hierarchical structure.

**functionalities:**
1. create a studies
2. read studies
3. update studies
4. delete studies
5. update the type of studies
6. update the specialty of studies
7. add slides
8. remove slides
10. add annotations
11. remove annotations
12. add users
13. remove users
14. move studies to (hierarchical structure)
15. search studies based on some conditionals

Only a study that has slides or annotations could be assigned to users/pathologies

 
### Slide

**Definition:**
a slide is a whole-slide image (also known as a virtual slide).

Support format:
* Aperio (.svs, .tif) 
* DICOM (.dcm) 
* Hamamatsu (.vms, .vmu, .ndpi) 
* Leica (.scn) 
* MIRAX (.mrxs) 
* Philips (.tiff) 
* Sakura (.svslide) 
* Trestle (.tif) 
* Ventana (.bif, .tif)
* Generic tiled TIFF (.tif)

**Schema:**

**functionalities:**
1. upload a slide
2. upload a slide bundle
3. read the matedata of a slide
4. update the matedata of a slide
5. rename a slide
6. read a slide as tiles
7. remove a slide

### Annotation
    
**Definition:**
An annotation is a region of interest that is drawn by users/pathologists.
**Schema:**

**functionalities:**
1. add an annotation
2. read an annotation
3. update an annotation's shape
4. update an annotation's note
5. remove an annotation

### Evaluation

**Definition:**

**Schema:**

**functionalities:**
1. add an evaluation
2. read an evaluation
3. update an annotation
4. remove an annotation

### Specialty

**Definition:**
A medical specialty is a branch of medical practice that focuses on a specific group of patients, diseases, skills, or philosophy. 

**Schema:**

**functionalities:**
1. add a specialty
2. read a specialty
3. update a specialty
4. remove a specialty

### User
**Definition:** 
A user is an entity that can complete studies or manage studies. Usually, a user could be a pathologist or/and system administrator.

**Schema:**

**functionalities:**
1. register users
2. activate users
3. deactivate users
4. read user profile
5. update user profile
6. delete user

### ER Diagram
```mermaid
erDiagram
    Studies {
        ObjectId id PK
        ObjectId pid FK "Parent study Ids"
        ObjectId spec_id FK "Specialty Ids"
        ObjectId[] cids FK "children study Ids"
        ObjectId[] sids FK "slide Ids"
        Users[] uids FK  "User Ids"
        string name
        text description
        
        string creator
        string updater
        Date created_at
        Date updated_at
    }

    Slides {
        text name
        ObjectId id PK
        ObjectId spec_id FK "Specialty Ids"
        string slide_id "slide unique id such as token_id"
        
        string location 
        object matedata
        ObjectId[] studies
        string creator
        string updater
        Date created_at
        Date updated_at
        
    }

    Annotations {
        ObjectId id PK
        ObjectId slide_id FK
        ObjectId study_id FK 
        GeoJson polygon
        string creator
        string updater
        Date created_at
        Date updated_at  

    }

    Specialties {
        ObjectId id PK
        string name
        string description
        string creator
        string updater
        Date created_at
        Date updated_at
    }

    Users {
        ObjectId id PK
        string email
        string first_name
        string last_name
        Object user_info
    }

    Studies o|--o{ Studies: has
    Studies ||--o{ Slides: contains
    Studies ||--o{ Annotations: contains
    Studies o|--|{ Users: belong
    Specialties ||--|{Studies: in
    Specialties ||--|{Studies: in
    Slides ||--o{ Annotations: has
    Users  o|--o| Annotations: annotate
    Slides ||--o{ Evaluations: has
    Users  o|--o| Evaluations: evalute
```

## User Interfaces

### Study Management

## UI component

### Hier
Definition


