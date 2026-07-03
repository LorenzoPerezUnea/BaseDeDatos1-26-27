# MySQL Workbench

Aunque MySQL puede administrarse completamente mediante comandos, hacerlo resulta incómodo cuando comenzamos a aprender.

MySQL Workbench proporciona una interfaz gráfica que facilita enormemente el trabajo.

No sustituye al lenguaje SQL.

Simplemente hace más sencillo interactuar con el servidor.

### ¿Qué permite hacer?

Entre otras muchas funciones, permite:

* Crear conexiones.
* Administrar servidores.
* Crear bases de datos.
* Diseñar diagramas.
* Escribir consultas SQL.
* Exportar e importar información.
* Administrar usuarios.

### El editor SQL

La parte más utilizada será el editor de consultas.

En él escribiremos instrucciones SQL como las siguientes:

```sql
SELECT *
FROM clientes;
```

Cada consulta será enviada posteriormente al servidor MySQL.

Workbench actúa como un cliente.

### Administrador gráfico

Además del editor SQL, Workbench incluye herramientas para administrar visualmente el servidor.

Por ejemplo:

* Ver tablas.
* Consultar índices.
* Crear usuarios.
* Gestionar permisos.
* Supervisar conexiones.

Esto facilita comprender la estructura interna del sistema sin necesidad de memorizar todos los comandos desde el primer día.

### Relación con MySQL

Es importante distinguir ambos conceptos.

MySQL es el servidor de bases de datos.

Workbench es únicamente un programa cliente.

Podemos cerrar Workbench sin apagar el servidor.

También podemos conectarnos al mismo servidor desde diferentes clientes.

### Ideas clave

* Workbench no es la base de datos.
* Es un cliente gráfico.
* Envía consultas SQL al servidor.
* Facilita la administración y el aprendizaje.

