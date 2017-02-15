# challenge
GPCDZ code challenge 

## The task
Design and implement a simple service provide REST API for **Entity**,

the service will have an endpoint for managing Entity(create, update, delete, list all entities, get entity).

The entity is described like this:

* socialMedia : string required
* dateCreation : date required
* dateUpdate : date required
* createdBy : user required
* latitud : long required
* longitud long required
* description : string
* type : string

for the **user** we need to use another service called userService, this service will be provided to you
the user service Expose endpoint to manage users.
the service is protected by a simple token to secure the endpoints just for the simplicity, to get a token you need just to 
use `GET /api/token`
## Example request:
```
GET /api/token
HTTP/1.1 200 OK
Content-Type: application/json

{
    "token":"wAUnAd9ZEhwbAfFX2n5b",
    "timestamp":1487176014645
}
```
the token expired after 10 minutes from the token creation.
the timestamp is the creation date of the token.

**To use the userService API you need to add token in the header for every request**
### Example Header 

key = Authorization, value = Bearer wAUnAd9ZEhwbAfFX2n5b

If the token is invalid or expired, or even if its not included in the header, you will get http status `401 unauthorized`.

# The userSerice API 

## Users endpoint

### Status codes:
* 200 No error
* 201 Created
* 400 Bad reaquest
* 401 unauthorized
* 204 No Content

## Create user 

`POST /api/users`

### Exemple

```
POST /api/users/
Content-Type: application/json
{
     "username": "gpcdz",
     "email":"contact@gpcdz.com",
     "firstName":"gpc",
     "lastName":"dz"
}
```

## Example result

```
HTTP/1.1 201 Created
  Content-Type: application/json

  {
  "id": "58a48a51ed187c0688694301",
  "username": "gpcdz",
  "firstName": "gpc",
  "lastName": "dz",
  "email": "contact@gpcdz.com"
 }
```

## Get User 
`GET /api/users/id or name`

### Exemple

```
GET /api/users/58a48a51ed187c0688694301

```

## Example result

```
HTTP/1.1 200 Ok
  Content-Type: application/json

  {
  "id": "58a48a51ed187c0688694301",
  "username": "gpcdz",
  "firstName": "gpc",
  "lastName": "dz",
  "email": "contact@gpcdz.com"
}
```

## list all the Users 

`GET /api/users`

### Exemple

```
GET /api/users

```

## Example result

```
HTTP/1.1 200 Ok
  Content-Type: application/json

 [
    {
        "id": "58a48a51ed187c0688694301",
        "username": "gpcdz",
        "firstName": "gpc",
        "lastName": "dz",
        "email": "contact@gpcdz.com"
    },
    {
        "id": "58a48c06ed187c0688694303",
        "username": "new",
        "firstName": "foo",
        "lastName": "bar",
        "email": "contact@me.com"
    }
  ]
```

## Delete User 
`DELETE /api/users/id`

### Exemple

```
DELETE /api/users/58a48a51ed187c0688694301

```

## Example result

```
HTTP/1.1 204 No Content
```


## Update user 
The username and the email they can not be updated

`PUT /api/users`

### Example

```
PUT /api/users
Content-Type: application/json
{
    "id": "58a48a51ed187c0688694301",
     "username": "gpcdz",
     "email":"contact@gpcdz.com",
     "firstName":"gpc",
     "lastName":"dz"
}
```

## Example result

```
HTTP/1.1 200 Ok
```

to use the api you run it locally using docker 

 ### First pull the Images 
**Pull mongodb image** 
 `docker pull mongo`

**Pull userservice image** 

 `docker pull smidaamine/userservice`

### Run the containers

**Run mongodb container** 
don't forget to change '/my/own/datadir'

`docker run --name db -v /my/own/datadir:/data/db -d mongo`

**Run userService container** 
dont forget to change '/my/own/datadir'

`docker run  --name userserice --link db:db -p 5999:5999 -d smidaamine/userservice`

now you can use userserice endpoints 


`localhost:5999/api/token`

`localhost:5999/api/users`

# extra infos 

Technologies we&#39;d like you to use:

- Spring (Boot), but you could use anything you want 
- Unit and integration testes
- Git - please create repo and do regular commits just like this was any other production project



