# wp-socialize

Agrega características de red social a WordPress

## Like Post

Permite indicar la valoracion de un artículo desde el punto de vista de un usuario registrado
Los usuarios registrados de cierto nivel pueden indicar cuando les gusta un artículo
Las valoraciones se acumulan también a nivel Autor.

### Implementacion

Al CPT Artículo se agregan los CF:
+ Cantidad de Likes
+ Cantidad de Dislikes

Al template del CPT Artículo se agregan:
+ Un boton que permite valorar positivo
+ Un boton que permite valorar negativo
+ Etiqueta counter con la cantidad de positivos
+ Etiqueta counter con la cantidad de negativos

A la pagina del Autor se agregan:
+ Etiquetas counter con acumulador de valoraciones del Autor

### Consideraciones

+ La cantidad de valoraciones debe poder consultarse en la dimension tiempo. Por ej: el ultimo mes

# Rest

Namespace: ```questionar-social/v1```

### Obtener Valoraciones

```GET /artículo-valoraciones/(?P<id>\d+)```

Obtiene la cantidad de Likes y Dislikes del artículo indicado como parámetro

### Agregar Valoracion

```POST /artículo-valoraciones/(?P<id>\d+)```

```json
body: {
    value: ['like'|'dislike']
}
```
Agrega la valoracion indicada en ```value``` al artículo indicado como parámetro.
Para cualquier caso se verifica si ya existía una valoración. En caso de existir, se elimina la anterior y se recalculan los acumuladores del artículo.