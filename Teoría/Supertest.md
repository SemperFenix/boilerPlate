# Supertest

Supertest es un test de integración. Su perspectiva es la contraria al test unitario. Lo que queremos comprobar es que todo nuestro programa funciona correctamente en conjunto.

npm i supertest @types/supertest

Creamos la carpeta e2e (end to end) o lo guardamos donde consideremos (por ejemplo, la carpeta de los router es una buena opción).

Creamos un archivo de testeo del endpoint (el que corresponda) y le añadmos la extensión spect en vez de test para poder ignorarlos luego en el coverage.

Importamos requets from 'supertest' y app from '../app.ts

Este sistema nos va a permitir testear todos los métodos hacia la base de datos de forma realista, comprobando que realmente nos conectamos a la DB.

Comenzamos haciendo una función que mockee una colección

```typescript
/* Primero creamos una colección con los datos que nosotros decidimos en la DB,
sobre esta colección haremos las pruebas. De esta forma, tendremos control sobre los datos
disponibles y no correremos riesgo de modificar datos de uso real. */

const setCollection = async () =>{
const usersFake = [...]
await User.deleteMany();
await User.insertMany(usersFake);
const data = await User.find();
const testIds = [data[0].id, data[1].id];
return testIds
}

/* Devolvemos los id porque en el segundo modelo necesito que una de sus propiedades sea un objeto del otro modelo, de esa manera hacemos un fake de la relación entre ambas tablas */

let ids: Array<string>

const setCollectionTreatment = async ()=>{
const treatmentsFake = [...]
await Treatment.deleteMany();
await Treatment.insertMany(treatmentsFake)
const data = await Treatments.find()
const treatmentsIds = [data[0].id, data[1].id]
return treatmentsIds
}

/* Para darle a sonar las variables de entorno las guardaremos en Github/Secrets como variables de entorno.
En el archivo sonar.yml, en la secci'on de testing coverage, añadiremos un env: donde le daremos las variables:
env:
    USER: ${{secrets.USER}}
    PASSW: ${{secrets.PASSW}}
    CLUSTER: ${{secrets.CLUSTER}}
    SECRET: ${{secrets.SECRET}}

*/

describe
describe
beforeEach(() =>{
await dataBaseConnect();
ids = await setCollection()

treatmentsIds = await setConllectionTreatment()
const payload: TokenPayload = {
id: ids[0];
name: 'adri';
role: 'admin'
}

token = createToken(payload)
})

afterEach(async () =>
await mongoose.disconnect())

test('then the (GET ALL ok)... sends a 200 status', async () =>{
    await request(app).get('/users').set('Authorization', `Bearer ${token}`).expect(200)
// Request es un 'server de testing'
// Este expect es equivalente a hacer expense(response.status).toBe(200)
}

test...() =>{
const mockLogin ={
name: 'kdam'
password: 'askldnf'}
await request(app).post('/users/register').send(mockLogin)
const response = await request(app).post('/users/register').send(mockLogin)
expect(response.status).toBe(201)
}
// En los métodos post hay que enviarle el body, eso lo hacemos con post().send(contenidoDelBody)
)
```
