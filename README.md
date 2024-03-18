
# Websockets

Los Websockets son una tecnología que permite una comunicación bidireccional y en tiempo real entre un cliente (usualmente un navegador web) y un servidor. A diferencia de HTTP, que sigue un modelo de solicitud-respuesta, los Websockets permiten una conexión persistente entre el cliente y el servidor, lo que posibilita la transmisión de datos tanto desde el cliente hacia el servidor como desde el servidor hacia el cliente en cualquier momento.

## Funcionamiento

1. **Handshake inicial**: La comunicación comienza con un handshake (apretón de manos) HTTP, donde el cliente solicita una actualización del protocolo a Websockets.
2. **Conexión persistente**: Una vez establecida la conexión, se mantiene abierta para la transmisión bidireccional de datos.
3. **Mensajes**: Los mensajes se envían en forma de tramas, permitiendo tanto el envío de texto como de datos binarios.
4. **Cierre de la conexión**: La conexión puede cerrarse desde cualquier extremo, ya sea el cliente o el servidor.

## Ventajas

- **Bajo sobrecosto de comunicación**: La conexión persistente reduce la sobrecarga de la conexión inicial de HTTP para solicitudes repetidas.
- **Latencia reducida**: Al evitar la sobrecarga de la conexión inicial y permitir una comunicación bidireccional eficiente, los Websockets pueden reducir la latencia en comparación con las técnicas tradicionales basadas en HTTP.
- **Actualización en tiempo real**: Ideal para aplicaciones que requieren actualizaciones instantáneas, como chats, feeds de redes sociales en tiempo real, juegos en línea, etc.

## Desventajas

- **Mayor complejidad**: Implementar y mantener una infraestructura de Websockets puede ser más complejo que trabajar con HTTP debido a la necesidad de gestionar conexiones abiertas y cerradas.
- **Requerimientos adicionales**: El soporte para Websockets en el servidor y en el cliente es necesario, lo que puede no ser posible en todas las plataformas.
- **Escalabilidad**: Manejar grandes cantidades de conexiones simultáneas puede ser un desafío y requerir una planificación cuidadosa para escalar horizontalmente.

## Ejemplo Javascript

```javascript
// Servidor WebSocket usando Node.js y el módulo ws
const WebSocket = require('ws');
const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', function connection(ws) {
  console.log('Cliente conectado');

  ws.on('message', function incoming(message) {
    console.log('Mensaje recibido:', message);
  });

  ws.send('¡Conexión establecida!');
});

// Cliente WebSocket básico en el navegador
const ws = new WebSocket('ws://localhost:8080');

ws.onopen = function() {
  console.log('Conexión establecida');
  ws.send('¡Hola servidor, soy el cliente!');
};

ws.onmessage = function(event) {
  console.log('Mensaje recibido del servidor:', event.data);
};
