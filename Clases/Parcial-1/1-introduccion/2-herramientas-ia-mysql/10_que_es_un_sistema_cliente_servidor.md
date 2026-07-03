# ¿Qué es un sistema Cliente-Servidor?

Cuando utilizamos una aplicación para consultar información, enviar un mensaje o realizar una compra por Internet, normalmente tenemos la sensación de que todo ocurre dentro del programa que vemos en la pantalla. Sin embargo, en la mayoría de los casos la información no se encuentra almacenada en nuestro ordenador, sino en otro equipo conectado a través de una red.

Este modelo de funcionamiento recibe el nombre de **arquitectura Cliente-Servidor** y constituye uno de los pilares de la informática moderna.

Las bases de datos relacionales, los servidores web, las aplicaciones móviles y la mayoría de los servicios de Internet utilizan esta arquitectura.

### La idea fundamental

La arquitectura Cliente-Servidor divide las responsabilidades entre dos tipos de programas.

El **cliente** es el programa con el que interactúa el usuario. Su función consiste en solicitar información, enviarla al servidor y mostrar los resultados.

El **servidor** es el programa encargado de atender esas solicitudes, procesarlas y devolver una respuesta.

Esta separación permite que muchos clientes puedan utilizar simultáneamente los mismos datos sin necesidad de mantener una copia en cada ordenador.

### Un ejemplo cotidiano

Podemos compararlo con un restaurante.

El cliente no entra directamente en la cocina para preparar su comida.

En su lugar:

1. Consulta el menú.
2. Hace un pedido al camarero.
3. La cocina prepara la comida.
4. El camarero entrega el resultado.

En este ejemplo:

| Restaurante | Informática         |
| ------------- | ---------------------- |
| Cliente     | Usuario              |
| Camarero    | Red de comunicación |
| Cocina      | Servidor             |
| Comida      | Datos solicitados    |

El cliente únicamente realiza una petición. Todo el trabajo ocurre en el servidor.

### Componentes básicos

Todo sistema Cliente-Servidor necesita al menos cuatro elementos.

```mermaid
flowchart LR

U[Usuario]
-->C[Cliente]

C
-->R[Red]

R
-->S[Servidor]
```

Cada componente tiene una responsabilidad específica.

* **Usuario:** interactúa con la aplicación.
* **Cliente:** envía las peticiones.
* **Red:** transporta la información.
* **Servidor:** procesa las solicitudes.

Aunque en ocasiones cliente y servidor pueden ejecutarse en el mismo ordenador, conceptualmente siguen siendo aplicaciones diferentes.

### Ventajas

La arquitectura Cliente-Servidor ofrece numerosas ventajas.

* Centraliza la información.
* Facilita las copias de seguridad.
* Permite controlar los permisos de acceso.
* Hace posible que muchos usuarios trabajen simultáneamente.
* Simplifica el mantenimiento del sistema.

Por este motivo se utiliza tanto en pequeñas empresas como en grandes plataformas con millones de usuarios.

### Caso práctico

Nuestra empresa comercial tendrá varios empleados.

* El departamento de ventas registrará pedidos.
* El almacén actualizará el inventario.
* Administración consultará las facturas.

Todos accederán a la misma base de datos.

Si cada ordenador almacenara una copia distinta de la información, sería prácticamente imposible mantener los datos sincronizados.

Gracias a la arquitectura Cliente-Servidor todos consultarán un único servidor MySQL.

### Ideas clave

* La arquitectura Cliente-Servidor separa las responsabilidades entre quien solicita información y quien la procesa.
* El cliente interactúa con el usuario.
* El servidor almacena y administra los datos.
* Varios clientes pueden compartir un mismo servidor.
* Este modelo constituye la base de la mayoría de aplicaciones actuales.

