# Ejercicios guiados

## Introducción

Ha llegado el momento de practicar.

Los siguientes ejercicios están diseñados para realizarse durante la clase con la ayuda del profesor. Cada uno se apoya en el anterior, de manera que al finalizar habremos construido una pequeña base de datos completamente funcional.

En todos los casos se recomienda seguir la siguiente metodología:

1. Leer cuidadosamente el enunciado.
2. Escribir primero la sentencia SQL.
3. Ejecutarla.
4. Verificar el resultado mediante un `SELECT`.

---

## Ejercicio 1. Registrar una categoría

Inserta una nueva categoría denominada **Impresoras** con la descripción ​**Equipos de impresión**​.

Al finalizar, muestra el contenido completo de la tabla `Categoria`.

---

## Ejercicio 2. Registrar dos clientes

Inserta dos nuevos clientes utilizando una única sentencia `INSERT`.

Datos sugeridos:

* Javier Torres — Burgos
* Elena Sánchez — León

Utiliza la fecha actual como fecha de registro.

Comprueba el resultado.

---

## Ejercicio 3. Registrar productos

Inserta tres productos pertenecientes a distintas categorías.

Cada producto debe incluir:

* nombre;
* precio;
* stock;
* estado activo;
* categoría correspondiente.

Comprueba que las claves foráneas sean válidas.

---

## Ejercicio 4. Actualizar información

Actualiza el precio de uno de los productos registrados anteriormente.

Posteriormente aumenta el stock de otro producto.

Verifica ambas modificaciones mediante un `SELECT`.

---

## Ejercicio 5. Desactivar productos sin stock

Supón que algunos productos tienen un stock igual a cero.

Escribe una sentencia `UPDATE` que marque dichos productos como inactivos.

---

## Ejercicio 6. Eliminar registros

Elimina uno de los clientes insertados anteriormente utilizando su identificador.

Comprueba que únicamente ese cliente ha desaparecido.

---

## Ejercicio 7. Analizando errores

Responde brevemente a las siguientes preguntas:

1. ¿Qué ocurre si intentas insertar un producto con una categoría inexistente?
2. ¿Qué sucede si repites un correo electrónico protegido por `UNIQUE`?
3. ¿Qué ocurre al ejecutar un `UPDATE` sin `WHERE`?
4. ¿Qué diferencia existe entre `DELETE` y `TRUNCATE`?

Comenta las respuestas con el resto de la clase.

---

## Ejercicio integrador

Trabajando en parejas:

* inserta nuevos clientes;
* crea varias categorías;
* registra productos;
* modifica algunos precios;
* elimina un registro incorrecto.

Finalmente intercambia la base de datos con otra pareja y comprueba que toda la información cumple las restricciones definidas.

---

## Objetivos alcanzados

Al completar estos ejercicios el estudiante habrá practicado:

* inserciones simples;
* inserciones múltiples;
* modificaciones;
* eliminaciones;
* verificación mediante consultas;
* interpretación de errores de integridad.

Con estos conocimientos estará preparado para comenzar el estudio de `SELECT` en la siguiente clase.

