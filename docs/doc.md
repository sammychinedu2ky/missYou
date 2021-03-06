
# INTRODUCTION

API documentation for missYou project

**Allowed HTTPs requests:**

| `POST`:   | To create resource                  |
| --------- | ----------------------------------- |
| `PUT`:    | Update resource                     |
| `GET`:    | Get a resource or list of resources |
| `DELETE`: | To delete resource                  |


**Description Of Usual Server Responses:**

- 200 OK - the request was successful (some API calls may return 201 instead).
- 201 Created - the request was successful and a resource was created.
- 204 No Content - the request was successful but there is no representation to return (i.e. the response is empty).
- 400 Bad Request - the request could not be understood or was missing required parameters.
- 401 Unauthorized - authentication failed or user doesn't have permissions for requested operation.
- 403 Forbidden - access denied.
- 404 Not Found - resource was not found.
- 405 Method Not Allowed - requested method is not supported for resource.


**Base URL**

All URLs referenced in the documentation have the following base:

`https://missyou-api.azurewebsites.net` **Active ✅**

<!-- `https://missyou-api.herokuapp.com`  **Active ✅** -->


The missYou REST API is served over HTTPS To ensure data privacy, un-encrypted HTTP is not supported.

## REFERENCE

**User**

Represents user details.

**User attributes:**

- id (Number): unique identifier
- name (String): name
- email (String): email id of the user
- password (String): password of the user

**On Resource Failure**

*RESPONSE*

```bash
{
  "status": Number,
  "error": "error message",
}
```


## User Collection

**Create a User:**

`POST` `/api/v1/auth/signup`

**Request**

*HEADERS*

`Content-Type:` application/json

*BODY*

```bash
{
  "name": "Vincent Iroleh",
  "email": "missyou@gmail.com",
  "password": "~!@#$%^&*()_+?<>"
}
```

*RESPONSE*

```bash
{
  "status": 200,
  "message": "Account created successfully",
  "token": "String"
}
```

---------------------------------------------------------------------------------------


**Login a User:**

`POST` `/api/v1/auth/login`

**Request**

*HEADERS*

`Content-Type:` application/json

*BODY*

```bash
{
  "email": "missyou@gmail.com",
  "password": "~!@#$%^&*()_+?<>"
}
```

*RESPONSE*

```bash
{
  "status": 200,
  "message": "Authenticated",
  "token": "",
  "user": {
    "role": "Client",
    "_id": "5f16fb29219785620757a14a",
    "name": "Vincent Iroleh",
    "email": "missyou@gmail.com",
    "salt": "",
    "hash": "",
  }
}
```

------------------------------------------------------------------------------------------

## Memorial Collection

**Create a Memorial:**

`POST` `/api/v1/auth/create-memorial`

**Request**

*HEADERS*

`Authorization:` Token

`Content-Type:` multipart/form-data

*BODY*

```bash
{
    "userID": Number
    "firstname": "String",
    "lastname": "String",
    "gender": "String",
    "relationship": "String",
    "dateOfBirth": Date,
    "countryOfBirth": "String",
    "stateOfBirth": "String",
    "cityOfBirth": "String",
    "dateOfDeath": Date,
    "countryOfDeath": "String",
    "stateOfDeath": "String",
    "cityOfDeath": "String",
    "specialDesignation": "String",
    "webAddress": "String",
    "about": "String",
    "biography": "String",
    "image": File,
}
```

*RESPONSE*

```bash
{
  "status": 200,
  "message": "Roseline's memorial page created successfully",
  "data": {
    "_id": "5f1f046d65c44f93f2ba16b9",
    "firstname": "Roseline",
    "lastname": "Iroleh",
    "gender": "Female",
    "relationship": "Mother",
    "dateOfBirth": "1954-04-30T00:00:00.000Z",
    "countryOfBirth": "Nigeria",
    "stateOfBirth": "Abia",
    "cityOfBirth": "Umuahia",
    "dateOfDeath": "2006-04-29T00:00:00.000Z",
    "countryOfDeath": "Nigeria",
    "stateOfDeath": "Abia",
    "cityOfDeath": "Aba",
    "specialDesignation": "None",
    "webAddress": "iroleh-roseline",
    "about": "About the dead",
    "biography": "Bio of the dead",
    "user": "5f16fb29219785620757a14a",
    "image": "URL",
    "tributes": [String],
    "photos": [String],
    "videos": [String],
    "audios": [String],
  }
```

------------------------------------------------------------------------------------------

**Get all Memorials:**

`GET` `/api/v1/memorials`


*RESPONSE*

```bash
{
  "status": 200,
  "message": "Memorials retrieved successfully",
  "memorials": [
    { }
  ]
}

```

------------------------------------------------------------------------------------------

**Get a Memorial:**

`GET` `/api/v1/memorial/:id`


*PARAMS*

```bash
{
    "id": Number    
}
```


*RESPONSE*

```bash
{
  "status": 200,
  "message": "Memorial retrieved successfully",
  "memorial": {
    "_id": String,
    "user": {
      "role": "Client",
      "_id": String,
      "name": "Vincent Iroleh",
      "email": "irolehiroleh@gmail.com",
    },
    "firstname": "Roseline",
    "lastname": "Iroleh",
    "gender": "Female",
    "relationship": "Mum",
    "dateOfBirth": "1945-06-28T00:00:00.000Z",
    "countryOfBirth": "Nigeria",
    "stateOfBirth": "Abia",
    "cityOfBirth": "Umuahia",
    "dateOfDeath": "2006-04-30T00:00:00.000Z",
    "countryOfDeath": "Nigeria",
    "stateOfDeath": "Abia",
    "cityOfDeath": "Aba",
    "specialDesignation": "None",
    "webAddress": "roseline-iroleh",
    "about": "About the dead",
    "biography": "Bio of the  dead",
    "image": "URL",
    "photos": [{
      "_id": String,
      "name": String,
      "photo": "URL",
    }],
    "tributes": [{
      "_id": "5f2eaa63fddbe393d96dfd64",
      "name": String,
      "title": String,
      "tribute": String
    }],
  }
}

```

------------------------------------------------------------------------------------------

**Get a Logged in User Memorials:**

`GET` `/api/v1/auth/user-memorials`

**Request**

*HEADERS*

`Authorization:` Token

*RESPONSE*

```bash
{
  "status": 200,
  "message": "Memorials retrieved successfully",
  "memorials": [
    { },
    { }
  ]
}

```


------------------------------------------------------------------------------------------

**Update a Memorial Details:**

`PUT` `/api/v1/auth/update-memorial/id`

**Request**

*HEADERS*

`Authorization:` Token

`Content-Type:` multipart/form-data

*PARAMS*

```bash
{
    "id": Number    
}
```

*BODY*

```bash

# optional
{
    "userID": Number
    "firstname": "String",
    "lastname": "String",
    "gender": "String",
    "relationship": "String",
    "dateOfBirth": Date,
    "countryOfBirth": "String",
    "stateOfBirth": "String",
    "cityOfBirth": "String",
    "dateOfDeath": Date,
    "countryOfDeath": "String",
    "stateOfDeath": "String",
    "cityOfDeath": "String",
    "specialDesignation": "String",
    "webAddress": "String",
    "about": "String",
    "biography": "String",
    "image": File,
}
```


*RESPONSE*

```bash
{
  "status": 200,
  "message": "Memorial Page updated successfully"
}

```



------------------------------------------------------------------------------------------

**Delete a Memorial:**

`DELETE` `/api/v1/auth/delete-memorial/id`

**Request**

*HEADERS*

`Authorization:` Token


*PARAMS*

```bash
{
    "id": Number    
}
```



*RESPONSE*

```bash
{
  "status": 200,
  "message": "Memorial page removed successfully"
}

```

**Add multiple photos to a Memorial:**

Doesn't need Authorization, because guests can perform this operation without logging in, for security checks, please enable to use [Google reCAPTCHA integration](https://developers.google.com/recaptcha/intro)

`PUT` `/api/v1/auth/update-photos/id`

`Content-Type:` multipart/form-data

**Request**


*PARAMS*

```bash
{
    "id": Number  # memorial id your wish to add photos
}
```

*BODY*

```bash
{
  "photo": File, # Single photo
  "name": String # name of guest adding photo
}

```


*RESPONSE*

```bash
{
  "status": 200,
  "message": "Photo added successfully",
  "photos": [ # returns an array of photos including the new added one
    {
      "_id": String,
      "name": String,
      "photo": String
    },
  ]
}

```

**Add tributes to a Memorial:**

Doesn't need Authorization, because guests can perform this operation, for security checks, please enable to use [Google reCAPTCHA integration](https://developers.google.com/recaptcha/intro)

`PUT` `/api/v1/auth/update-tributes/id`

`Content-Type:` multipart/form-data

**Request**


*PARAMS*

```bash
{
    "id": Number  # memorial id your wish to add tribute to
}
```

*BODY*

```bash
{
  "name": String,
  "title": String,
  "tribute": String
}

```


*RESPONSE*

```bash

{
  "status": 200,
  "message": "Tribute added successfully",
  "tributes": [
    {
      "_id": String,
      "name": String,
      "title": String,
      "tribute": String
    },
  ]
}

```

