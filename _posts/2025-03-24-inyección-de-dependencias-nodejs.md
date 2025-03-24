---
layout: post
title:  "TDD con React y Vite"
date:   2025-03-17 17:00:00 -0600
categories: React Vite
---

# Inyección de dependencias con Node.js


## Hacer una clase con construtores

```javascript
export class MovieController {
  constructor ({ movieModel }) {
    this.movieModel = movieModel
  }
}
```

## Inyección de dependencias

Movemos la creación de la dependencia de modelo lo más arriba posible. En este caso lo movemos a `server-with-mysql.js`

```javascript
import { createApp } from './app.js'
import { MovieModel } from './models/mysql/movie.js'

createApp({ movieModel: new MovieModel() })
```

Es aquí donde instanciamos nuestro modelo. No se utilizó ninguna biblioteca es específico pero debe de existir.

También se creo el comando

```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "node --watch app.js",
    "start:mysql": "node --watch server-with-mysql.js",
    "start:local": "node --watch server-with-local.js"
  }
```

Para ejecutar directamente el archivo que queramos. También se podría hacer con variables de entorno.



