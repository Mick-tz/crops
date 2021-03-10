# Documentacion

## Modelado

*Los campos que no permiten repeticiones son procedidos por la palabra "UNIQUE", todo campo de id no permite repeticiones dentro de su relación (documento)*

*Los campos que sirven *

*Los campos opcionales en los objetos se indican con la palabra "NULL"*

*Todo campo que no seguido por la palabra "NULL" es considerado obligatorio*

*Los campos que son procedidos por la palabra "AUTO" serán agregados de forma automática sin la participación del usuario, todo campo de id será de está forma

OBS: Dichos campos son agregados de forma automatica por el frontend o middleware, no por el sistema manejador de base de datos*

*Los campos que corresponden a un id de otro objeto se representan con las palabras "FOREIGN KEY"*

```
Forma: {
    """
    Representa un tipo de medición, debe ser generada por un admin y puede ser consultada
    por todo capturador, mismos que podrán agregar una medición a la forma.
    """

    id: uui  
    titulo: Str,
    descripcion: Str,
    fecha_creación: DateTime,                        "AUTO"
    fecha_ultima_modificacion: DateTime,             "AUTO"
    creador_forma: uuid,                             "FOREIGN KEY"
    campos: Array[CampoForma]                        "FOREIGN KEY"
}

CampoForma: {
    """
    Modelo genérico para los campos que deben ser incluidos en una forma
    (por ejemplo, si la forma modela una medición de la humedad de la tierra,
    uno de los campos puede ser peso antes de secado y otro campo peso después del secado).
    Opcionalmente se puede agregar unidades (para cuando el tipo de campo es numerico)
    y opciones (para cuando el tipo de campo es Select
    """

    id: uuid,   
    titulo: Str,  
    descripcion: Str,
    forma: uuid                                    "FOREIGN KEY"
    tipo: TipoForma(Str), 
    opciones: Array[Str],                          "NULL"
    unidades: Str                                  "NULL"
}

#El tipo de campo determina como se visualizará el campo de una forma

TipoCampo: Str -> [
  dateField,
  timeField,
  integerField,
  floatField,
  textField,
  selectField
]

Medicion: {
    """
    Modelo genérico de las mediciones que son tomadas con respecto a cada forma.
    """
    id: uuid,
    capturador: uuid,                              "AUTO"
    fecha_captura: Date,                              "AUTO"
    hora_captura: Time,                               "AUTO"
    forma: uuid,                                      "AUTO FOREIGN KEY"
    medición: Array[CampoForma]
}

Usuario: {
    """
    Modelo generico de usuario. Admin y capturador usan el mismo tipo de usuario pero
    los admin tiene permisos distintos.
    """

    id: uuid,                                         "AUTO"
    nombre_usuario: Str                               "UNIQUE PK"
    nombres: Str,
    apellidos: Str,
    telefono: Str,
    correo: Email,                                    #Requerido para el reset de password
    password: bycriptHash,
    tokens: Array[jwt]
}

Admin: {
    """
    Modelo de administrador, tiene todos los permisos sobre la página.
    """

    id: uuid, 
    usuario: uuid                                     "FOREIGN KEY"
    tokens: Array[jwt]
}
```
