# 브니엘 시스템 ER Diagram

## 자유게시판 게시글/댓글 추천 기능

- 게시글(post) 추천 종류
  - 추천해요(recommand)
  - 행복해요(happy)
  - 슬퍼요ㅠ(sad)
  - 화나요!!(angry)
- 댓글(reply) 추천 종류
  - 엄지척(thumb up)
  - 사랑해요(heart)

- 추천 종류는 DB Table로 연결 $\to$ Many to Many Relation
  - 한 명의 User는 여러 게시글을 추천할 수 있다. 대신 하나의 게시글에는 하나의 추천만 할 수 있다.
  - 하나의 게시글은 여러 명에게 추천 받을 수 있다. 대신 동일한 게시글은 여러개일 수 없다..

```mermaid
erDiagram
    %% 멤버(교사) Table
    Member{
        int id PK
        string user_id
        string user_name
        string mobile_phone
        string name
        string position
        string address
        datetime create_date
        datetime update_date
        bool is_pastor
        relationthsip questions
        relationthsip answers
        relationthsip notices
        relationthsip students
    }
    
    %% Question Class
    Question{
        int id PK
        string subject
        string content
        datetime create_date
        int user_id FK "Member.id"
        int user "Relation to Member with backref"
        int voter "Relation to Member with backref"
        int post_happy "Relation to Member with backref"
        int post_sad "Relation to Member with backref"
        int post_angry "Relation to Member with backref"
    }
    
    %% 게시글 - 추천해요 DB Table
    post_votes{
        int id PK 
        int user_id FK "Member.id"
        int post_id FK "Question.id"
    }
    

    %% 게시글 - 행복해요 DB Table
    post_happy{
        int id PK 
        int user_id FK "Member.id"
        int post_id FK "Question.id"
    }
    
    
    %% 게시글 - 슬퍼요ㅠ DB Table
    post_sad{
        int id PK 
        int user_id FK "Member.id"
        int post_id FK "Question.id"
    }
    
     
    %% 게시글 - 화나요!! DB Table
    post_angry{
        int id PK 
        int user_id FK "Member.id"
        int post_id FK "Question.id"
    }
    
    %% 댓글 - 엄지척 DB Table
    reply_votes{
        int id PK 
        int user_id FK "Member.id"
        int post_id FK "Answer.id"
    }
    
    %% 댓글 - 사랑해요 DB Table
    reply_heart{
        int id PK 
        int user_id FK "Member.id"
        int post_id FK "Answer.id"
    }

    Member }o--o{ post_votes:manyToMany
    Member }o--o{ post_happy:manyToMany
    Member }o--o{ post_sad:manyToMany
    Member }o--o{ post_angry:manyToMany
    
    
    Question }o--o{ post_votes:manyToMany
    Question }o--o{ post_happy:manyToMany
    Question }o--o{ post_sad:manyToMany
    Question }o--o{ post_angry:manyToMany

    Member }o--o{ reply_votes:manyToMany
    Member }o--o{ reply_heart:manyToMany

    Question }o--o{ reply_votes:manyToMany
    Question }o--o{ reply_heart:manyToMany
    
    
```

## Gallery ER Diagram

```mermaid
erDiagram
    Member{
        int id PK
        string user_id
        string user_name
        string mobile_phone
        string name
        string position
        string address
        datetime create_date
        datetime update_date
        bool is_pastor
        relationthsip questions
        relationthsip answers
        relationthsip notices
        relationthsip students
    }
    
    Gallery{
        int id PK
        string subject
        string content
        dateime create_date
        int user_id FK "Member id"
        
    }
    
    GalleryImage{
        int id PK
        int gallery_id FK "Gallery id"
        string img_path
    }

    Member ||--o{ Gallery: createGalleries
    Gallery ||--|{ GalleryImage: hasGalleryImages
```
