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
```
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
``````
