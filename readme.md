# Tokopedia Play CLONE

---

## Mid Term Generasi Gigih

---

## Table of Contents

- [Introduction](#introduction)
- [Schema Database](#schema-database)
- [Installation](#installation)
- [API Documentation](#api-documentation)

## Introduction

This project is a Tokopedia Play Clone (Backend) Project.

## Schema Database

### Collection: Comment

- \_id: ObjectId (Primary Key)
- username: String (Username of the commenter)
- comment: String (Content of the comment)
- createdAt: Date (Timestamp of when the comment was created)
- video: ObjectId (Foreign Key referencing the Video collection)

### Collection: Product

- \_id: ObjectId (Primary Key)
- name: String (Name of the product)
- price: Number (Price of the product)
- image: String (URL of the product image)
- productUrl: String (URL of the product details page)
- createdAt: Date (Timestamp of when the product was created)
- updatedAt: Date (Timestamp of when the product was last updated)

### Collection: User

- \_id: ObjectId (Primary Key)
- username: String (Username of the user)
- email: String (Email address of the user)
- password: String (User's hashed password)

### Collection: Video

- \_id: ObjectId (Primary Key)
- title: String (Title of the video)
- videoUrl: String (URL of the video content)
- thumbnailUrl: String (URL of the video thumbnail)
- products: Array of ObjectId (Foreign Keys referencing the Product collection)
- comments: Array of ObjectId (Foreign Keys referencing the Comment collection)
- createdAt: Date (Timestamp of when the video was created)
- updatedAt: Date (Timestamp of when the video was last updated)

### Relationships:

- The Comment collection is related to the **_Video_** collection through the video field, which references the ObjectId of the corresponding video.
- The Product collection is not directly related to other collections, but it is referenced in the Video collection through the **_products_** field, which holds an array of ObjectIds referencing the products associated with the video.
- The User collection is not directly related to other collections in this schema, but it is expected to be associated with videos, comments, or products through their respective fields.

## Installation

Step-by-step instructions on how to set up the project on a local machine. Include any prerequisites, dependencies, and the commands needed to install them. Also, provide guidance on how to set up a virtual environment, if applicable.

- Clone repository

```bash
git clone https://github.com/anasamrullah/mid-term-gigih7.git

cd midterm-gigih7
```

- Install dependencies

```
npm install
```

- Set your environment

```
cp .env.example .env
```

- Setting Your environment in (.env) file

```
URL_DATABASE = YOUR_MONGO_DB_URL
JWT_SECRET = YOUR_JWT_SECRET_CODE
PORT = YOUR_PORT
```

- Start apps

```
npm start
```

## API Documentation

### Auth

## **POST /register**

Creates a new User and returns the new object.

- **URL Params**
  None
- **Headers**
  Content-Type: application/json
- **Data Params**

```
  {
    username: string,
    email: string,
    password: string
  }
```

**Response:**

- **Succes Code:** 200 (Success)
  **Example:**

```
{
    "statusCode": 200,
    "error": false,
    "data": {
        "username": string,
        "email": string,
    },
    "message": "success"
}
```

- **Failed Code:** 400 (Bad Request)
  **Example:**

```
{
    "statusCode": 400,
    "error": true,
    "data": "username, email, password is required",
    "message": "error"
}
```

## **POST /login**

Login User and returns the new object.

- **URL Params**
  None
- **Headers**
  Content-Type: application/json
- **Data Params**

```
{
    email: string,
    password: string
}
```

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": {
        "token": String,
        "expiresIn": "1h"
    },
    "message": "Login successful"
}
```

- **Code:** 401 (Invalid Creadentials)

```
{
    "statusCode": 401,
    "error": true,
    "data": "Invalid credentials",
    "message": "error"
}
```

- **Code:** 404 (Not Found)
  **Content:**

```
{
    "statusCode": 404,
    "error": true,
    "data": "User not found",
    "message": "error"
}
```

### VIDEO

## **GET /video**

Returns all video list in the system.

- **URL Params**
  None
- **Data Params**
  None
- **Headers**
  Content-Type: application/json

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": [
        {<video_object>},
        {<video_object>},
        {<video_object>},
    ],
    "message": "success"
}
```

## **GET DETAIL /video/detail/:id**

Returns all list video in the system.

- **URL Params**
  _Required:_ `id=[string]`
- **Data Params**
  None
- **Headers**
  Content-Type: application/json

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": [
        {
            <video_object>,
            product:[
                <product_object>,
                <product_object>,
            ],
            comments:[
                <comments_object>,
                <comments_object>,
            ]
        }

    ],
    "message": "success"
}
```

- **Code:** 404 (Not Found)

```
{
    "statusCode": 404,
    "error": true,
    "data": null,
    "message": "Cast to ObjectId failed for value \"64c2212fdbb1057e3f1f0d0\" (type string) at path \"_id\" for model \"Video\""
}
```

## **POST /video**

Input video and returns the new object video.

- **URL Params**
  None
- **Headers**
  Content-Type: application/json
- **Data Params**

```
{
    title: string,
    videoUrl: string,
    productId:Array
}
```

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": {
        "title": String,
        "videoUrl": String,
        "thumbnailUrl": String,
        "products": [
            String,
            String
        ],
        "comments": [],
        "_id": String,
        "__v": 0
    },
    "message": "success"
}
```

- **Code:** 400 (Bad Request)

```
{
    "statusCode": 400,
    "error": true,
    "data": "title or videoUrl is required",
    "message": "error"
}
```

## **PUT /video/:id**

Edit video and returns the new object video.

- **URL Params**
  None
- **Headers**
  Content-Type: application/json
- **Data Params**

```
{
    title: string,
    videoUrl: string,
}
```

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": {
        "title": String,
        "videoUrl": String,
        "thumbnailUrl": String,
        "products": [
            String,
            String
        ],
        "comments": [],
        "_id": String,
        "__v": 0
    },
    "message": "success"
}
```

## **DELETE /video/:id**

Delete video and returns the new object video.

- **URL Params**
  _Required:_ `id=[string]`
- **Headers**
  Content-Type: application/json

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": {
        "_id": String,
        "title": String,
        "videoUrl": String,
        "thumbnailUrl": String,
        "products": [],
        "comments": [],
        "__v": 0
    },
    "message": "success"
}
```

### PRODUCT

## **GET /product**

Returns all product list in the system.

- **URL Params**
  None
- **Data Params**
  None
- **Headers**
  Content-Type: application/json

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": [
        {<video_object>},
        {<video_object>},
        {<video_object>},
    ],
    "message": "success"
}
```

## **POST /product**

Input product and returns the new object product.

- **URL Params**
  None
- **Headers**
  Content-Type: application/json
- **Data Params**

```
{
    name: string,
    price: string,
    image:String,
    productUrl:String
}
```

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": {
        "name": String,
        "price": Int,
        "image": String,
        "productUrl": String,
        "_id": String,
        "__v": 0
    },
    "message": "success"
}
```

## **PUT /product/:id**

Edit product and returns the new object product.

- **URL Params**
  None
- **Headers**
  Content-Type: application/json
- **Data Params**

```
{
    name: string,
    price: string,
    image: string,
    productUrl: string,
}
```

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": {
        "name": String,
        "price": Int,
        "image": String,
        "productUrl": String,
        "_id": String,
        "__v": 0
    },
    "message": "success"
}
```

## **DELETE /product/:id**

Delete product and returns the new object product.

- **URL Params**
  _Required:_ `id=[string]`
- **Headers**
  Content-Type: application/json

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": {
        "_id": String,
        "name": String,
        "price": Int,
        "image": String,
        "productUrl": String,
        "__v": 0
    },
    "message": "success"
}
```

### COMMENT

## **GET /comment**

Returns all comment list in the system.

- **URL Params**
  None
- **Data Params**
  None
- **Headers**
  Content-Type: application/json

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": [
        {<video_object>},
        {<video_object>},
        {<video_object>},
    ],
    "message": "success"
}
```

## **GET /comment/:videoId**

Returns all comment list in the system.

- **URL Params**
  _Required:_ `videoId=[string]`
- **Data Params**
  None
- **Headers**
  Content-Type: application/json

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": [
        {<video_object>},
        {<video_object>},
        {<video_object>},
    ],
    "message": "success"
}
```

## **POST /comment**

Input comment and returns the new object comment.

- **URL Params**
  None
- **Headers**
  Content-Type: application/json
  Authorization: Bearer `<OAuth Token>`
- **Data Params**

```
{
    "comment":String,
    "videoId":String
}
```

**Response:**

- **Code:** 200

```
{
    "statusCode": 200,
    "error": false,
    "data": {
        "username": String,
        "comment": String,
        "createdAt": String,
        "video": String,
        "_id": String,
        "__v": 0
    },
    "message": "success"
}
```
