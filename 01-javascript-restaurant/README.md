# Diagnóstico: el restaurante

## Contexto

Un restaurante recibe órdenes a lo largo del tiempo. Cada orden indica qué platillos se pidieron y cuántas piezas de cada uno.

Cada platillo pertenece a una cocina: **Parrilla**, **Freidora** o **Bebidas**. Cada cocina prepara **una pieza a la vez**, en el orden en que le llegan, y las tres cocinas trabajan al mismo tiempo. Una orden está lista cuando todas sus piezas están terminadas.

Por eso, una orden que llega antes no necesariamente está lista antes: depende de qué pidió y de qué tan ocupadas estén las cocinas.

## Datos iniciales

Los tiempos están en milisegundos. `arrival` indica cuánto tiempo después de abrir el restaurante llega cada orden.

```js
const MENU = {
  'Hamburguesa': { kitchen: 'Parrilla', time: 3000 },
  'Hot dog': { kitchen: 'Parrilla', time: 2000 },
  'Papas fritas': { kitchen: 'Freidora', time: 1500 },
  'Pollo frito': { kitchen: 'Freidora', time: 4000 },
  'Refresco': { kitchen: 'Bebidas', time: 400 },
};

const ORDERS = [
  {
    id: 1,
    arrival: 0,
    dishes: [
      { name: 'Hamburguesa', quantity: 1 },
      { name: 'Pollo frito', quantity: 1 },
      { name: 'Refresco', quantity: 1 },
    ],
  },
  {
    id: 2,
    arrival: 1000,
    dishes: [
      { name: 'Hot dog', quantity: 3 },
      { name: 'Refresco', quantity: 1 },
    ],
  },
  {
    id: 3,
    arrival: 4500,
    dishes: [
      { name: 'Papas fritas', quantity: 2 },
      { name: 'Refresco', quantity: 1 },
    ],
  },
];
```

## Parte 1: fundamentos

Usa los datos iniciales. No necesitas asincronía en esta parte.

### Funciones con los datos

1. `getTotalPieces(order)`: cuántas piezas tiene una orden en total.
2. `getPiecesByKitchen(orders)`: un objeto con cuántas piezas le tocan a cada cocina, sumando todas las órdenes.
3. `sortOrdersByTime(orders)`: las órdenes ordenadas de menor a mayor tiempo total de preparación (la suma de los tiempos de todas sus piezas), **sin modificar el arreglo original**.
4. `splitOrder(order)`: un arreglo con cada pieza de la orden por separado, con su número y su cocina. Por ejemplo, para la orden 2:

```js
[
  { name: 'Hot dog', number: 1, quantity: 3, kitchen: 'Parrilla' },
  { name: 'Hot dog', number: 2, quantity: 3, kitchen: 'Parrilla' },
  { name: 'Hot dog', number: 3, quantity: 3, kitchen: 'Parrilla' },
  { name: 'Refresco', number: 1, quantity: 1, kitchen: 'Bebidas' },
]
```

## Parte 2: el restaurante

### Requisitos

- Cada orden llega en su tiempo de `arrival`. Simula los tiempos con `setTimeout`.
- Al llegar una orden, cada pieza se envía a su cocina, en el orden en que aparece en la orden. Por ejemplo, 3 hot dogs son 3 piezas: `1/3`, `2/3` y `3/3`.
- Cada cocina prepara una pieza a la vez, en el orden en que le llegan. Las tres cocinas trabajan al mismo tiempo.
- Una orden está lista cuando todas sus piezas están terminadas.

### Salida

Imprime cada evento con el tiempo transcurrido desde que abrió el restaurante, con este formato exacto:

```
[0.0s] Orden 1 recibida
[0.0s] Parrilla: inicia Hamburguesa 1/1 (orden 1)
[3.0s] Parrilla: termina Hamburguesa 1/1 (orden 1)
[x.xs] Orden 1 lista
```

## Reglas y entrega

- **Tecnología:** JavaScript o TypeScript con Node.js, sin librerías externas. Todo se ejecuta en consola. Nombra variables y funciones en inglés; los mensajes que se imprimen van en español.
- **Puedes consultar** documentación (MDN, javascript.info) y buscadores. No uses herramientas de IA.
- **Entrega:** un solo archivo, `restaurant.js`, en esta carpeta, con las dos partes. Debe ejecutarse con `node restaurant.js`. Indica en un comentario al inicio hasta dónde llegaste.
- En la revisión presentarás tu solución: cómo la resolviste y, si algo no lo lograste, por qué y hasta qué punto llegaste.

Importa más que entiendas lo que hiciste que resolverlo todo. Si no terminas, entrega hasta donde llegaste.
