# API de pruebas con My JSON Server

API REST ficticia para practicar peticiones desde Postman, curl, JavaScript o una integración que consuma APIs externas. Todos los datos son inventados.

[Abrir la API](https://my-json-server.typicode.com/JRLK0/api-pruebas-json)

My JSON Server convierte el fichero `db.json` de este repositorio público en endpoints HTTP. No necesitas instalar nada ni configurar un backend.

## URL base

```text
https://my-json-server.typicode.com/JRLK0/api-pruebas-json
```

## Datos y endpoints

| Ruta | Contenido |
| --- | --- |
| `/users` | Tres usuarios con nombre, email ficticio y estado activo |
| `/users/1` | Un usuario por ID |
| `/users?name=Ana Demo` | Usuario cuyo nombre coincide exactamente |
| `/users?q=ana` | Búsqueda de texto en los campos del usuario |
| `/users?active=true` | Usuarios activos |
| `/products` | Tres productos con categoría, precio y stock |
| `/products/1` | Un producto por ID |
| `/orders` | Tres pedidos en distintos estados |
| `/orders?userId=1` | Pedidos del usuario 1 |
| `/products?category=accesorios` | Productos filtrados por categoría |

Los pedidos referencian usuarios mediante `userId` y productos mediante `productId`. Los precios y totales del ejemplo están en EUR.

## Probar con curl

Define la URL base en tu terminal:

```bash
BASE='https://my-json-server.typicode.com/JRLK0/api-pruebas-json'
```

Leer una lista, un elemento y un filtro:

```bash
curl "$BASE/users"
curl "$BASE/users?q=ana"
curl "$BASE/users?name=Ana%20Demo"
curl "$BASE/products/1"
curl "$BASE/orders?userId=1"
```

Simular la creación de un usuario:

```bash
curl -X POST "$BASE/users" \
  -H 'Content-Type: application/json' \
  -d '{"name":"Pedro Demo","email":"pedro@example.com","active":true}'
```

Simular un cambio y una eliminación:

```bash
curl -X PATCH "$BASE/orders/2" \
  -H 'Content-Type: application/json' \
  -d '{"status":"delivered"}'

curl -X DELETE "$BASE/orders/3"
```

## Probar con JavaScript

```javascript
async function getProducts() {
  const response = await fetch(
    'https://my-json-server.typicode.com/JRLK0/api-pruebas-json/products'
  );
  if (!response.ok) throw new Error(`HTTP ${response.status}`);
  return response.json();
}

getProducts().then(console.log).catch(console.error);
```

En Postman utiliza las mismas URLs y métodos. Para POST o PATCH, selecciona **Body → raw → JSON** e introduce el cuerpo del ejemplo.

## Cambiar los datos

1. Edita `db.json` en la raíz del repositorio y conserva un JSON válido.
2. Haz commit y push a `main`.
3. Vuelve a consultar la API. El servicio mantiene una caché de aproximadamente un minuto.

## Limitaciones

- POST, PUT, PATCH y DELETE son simulados: **los cambios no se guardan**. Un GET posterior devuelve los datos del repositorio.
- La API y el repositorio son públicos. Usa únicamente datos ficticios.
- Es un servicio de pruebas en beta, con límites de tamaño y recursos; mantén `db.json` pequeño.

Documentación del servicio: [My JSON Server](https://my-json-server.typicode.com/).
