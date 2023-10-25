# Backend

Configurar un proyecto backend en Node.

## Paso 1: Crear un directorio e inicializarlo
`mkdir backend` 
Una vez dentro del directorio/carpeta, ejecutar: 
`npm init`
Se completa el formulario según corresponda. En caso no se sepa qué poner, simplemente dejar en blanco.

## Paso 2: Instalar los paquetes necesarios
`npm install express nodemon`

## Paso 3: Añadir archivo al proyecto
Crear un nuevo archivo dentro del directorio (backend) del proyecto llamado `server.js` con el siguiente contenido:
```js
const express = require('express')
const bodyParser = require('body-parser')
const path = require('path')

const app = express()
const port = 3080

const users = ['John', 'Pepe']

app.use(express.static(path.join(__dirname, './static')));
app.use(bodyParser.json());

app.get('/api/users', (req, res) => {
    console.log('/api/users invocada!')
    res.json(users);
});

app.post('/api/user', (req, res) => {
    const user = req.body.user;
    console.log("Agregando user ::::::", user);
    users.push(user);
    res.json("user agregado");
});


app.get('/', (req, res) => {
    res.sendFile(path.join(__dirname, './static/index.html'));
})

app.listen(port, ()=>{
    console.log("Server escuchando en el puerto:::", port);
})
```

## Paso 4: Modificar el `package.json`
Finalmente, se debe modificar el `package json` para poder ejecutar los scripts necesarios para el proyecto. Se añade la línea `"dev":"node server.js"`

```json
{
  "name": "backend",
  "version": "1.0.0",
  "description": "Ejemplo de backend",
  "main": "index.js",
  "scripts": {
    "dev": "node server.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "progra",
    "web"
  ],
  "author": "edgar huaranga",
  "license": "ISC",
  "dependencies": {
    "express": "^4.18.2",
    "nodemon": "^3.0.1"
  }
}

```
----
# ¿Cómo funciona este backend?
El archivo `server.js` inicia un servicio a través del puerto 3080. 
```js
app.listen(port, ()=>{
    console.log("Server escuchando en el puerto:::", port);
})
```

Este servicio está listo para ejecutar dos tareas específicas:
1. Obtener (GET request) a todos los usuarios del sistema.
2. Registrar (POST request) un nuevo usuario. 

### GET request
Lectura de todos los usuarios a través de una consulta de tipo GET. 
```js
app.get('/api/users', (req, res) => {
    console.log('/api/users invocada!')
    res.json(users);
});
``` 
### POST request
Escritura de un nuevo usuario a través de una consulta tipo POST.
```js
app.post('/api/user', (req, res) => {
    const user = req.body.user;
    console.log("Agregando user ::::::", user);
    users.push(user);
    res.json("user agregado");
});
```

# Prueba
Se puede hacer la prueba de los servicios de distintas formas. Para el caso de las consultas de tipo GET, es posible hacer la prueba desde cualquier navegador solo copiando el URL de la consulta. Para el caso de consultas POST se puede utilizar algún terminal y ejecutar comandos o utilizar herramientas que faciliten ese tipo de interacción. 

Para el GET request se ejecuta el siguiente comando:
```
curl --location 'http://localhost:3080/api/users'
```
O también pegar el `http://localhost:3080/api/users` en el navegador.


En el caso del POST request se puede ejecutar el siguiente comando:
```bash
curl --location 'http://localhost:3080/api/user' \
--header 'Content-Type: application/json' \
--data '{"user": "edgar"}'
```

Se puede observar que dentro de `--data '{"user":"edgar"}'` debe mantener ese formato para que pueda ser leído como user en la línea `const user = req.body.user;`