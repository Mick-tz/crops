## endpoints

#### Usuarios

```
GET - api/usuarios
(ordenados alfabéticamente por apellido, 20 por página)

  response:
    {
      "usuarios": Array[Usuario],
      "pagintation_info": PaginationInfo,
    }

GET - api/usuario/:id
  response:
    {
      "usuario": Usuario,
    }

POST - api/usuario/
  response: 
    {
      "usuario": Usuario
    }

PUT - api/usuario/
  response: 
    {
      "usuario": Usuario
    }

DELETE - api/usuario/:id
  response:
    {
      "usuario": Usuario
    }

```


#### Login

```
POST - api/login
  response:
    {
      "usuario": Usuario
      "Bearer": Token
    }

POST - api/logout
    response:
      {
        "status": HTTPStatus
      }

POST - api/reset_password
  response
    {
      "status": HTTPStatus
    }
```


#### Formas

```
GET - api/formas?porPagina=int&pagina=int
  response:
    {
      "formas": Array[Forma],
      "pagintation_info": PaginationInfo,
    }

GET - api/forma/:id
  response:
    {
      "forma": Forma,
    }

POST - api/forma
  response:
    {
      "forma": Forma
    }

PATCH - api/forma/
  response:
    {
      "forma": Forma
    }

DELETE - api/forma/:id
response:
    {
      "forma": Forma
    }
```

#### Medición

GET - api/mediciones?forma=uuid&pagina=int&porPagina=int  response    {      "mediciones": Array[Medicion],    }
POST - api/medicion  response    {      "medicion": Medicion    }
