Пример с сайта <https://dbdiagram.io/>
``` js
//// -- LEVEL 1
//// -- Tables and References

// Creating tables
Enum userStatus {
  approved  
  rejected 
  awaiting
  closed
}

Table User as U {
  id uuid [pk]
  surname varchar [null]
  firstName varchar [null]
  middleName varchar [null]
  username varchar [not null, unique]
  email varchar [not null, unique]
  passwordHash varchar [not null]
  imagePath varchar [null]
  location varchar [null]
  phone varchar [null]
  about varchar(6000) [null]
  role varchar [null]
  status userStatus [not null]
  createdAt timestamp [not null]
  updateAt timestamp [null]
}

Table Contact as C {
  id uuid [pk]
  title varchar [not null]
  url varchar [not null]
  ownerId uuid [not null]
  createdAt timestamp [not null]
  updateAt timestamp [null]
  deleteAt timestamp [null]
 }

// Creating references
// You can also define relaionship separately
// > many-to-one; < one-to-many; - one-to-one

Ref: C.ownerId > U.id


Table Project as P {
  id uuid [pk]
  title varchar [not null]
  description json [not null]
  ownerId uuid [not null]
  imagePath varchar [null]
  isPublished boolean [not null]
  createdAt timestamp [not null]
  updateAt timestamp [null]
  deleteAt timestamp [null]
}


Enum userType {
  admin
  participant
}

Table UserType as UT {
  id uuid [pk]
  title userType [not null]
}


Table UserProject as UP {
  id uuid [pk]
  userId uuid [not null]
  projectId uuid [not null]
  userTypeId uuid [not null]
}

Ref: U.id < UP.userId
Ref: P.id < UP.projectId
Ref: UT.id < UP.userTypeId


Table Link {
  id uuid [pk]
  title varchar [not null]
  url varchar [not null]
  projectId uuid [not null]
  createdAt timestamp [not null]
  updateAt timestamp [null]
  deleteAt timestamp [null]
}


Ref: P.id < Link.projectId


Table FavoriteProject {
  id uuid [pk]
  projectId uuid [not null]
  userId uuid [not null]
}
```