# Problemas tipo examen II

## Introducción

Los ejercicios de este bloque representan el nivel de dificultad esperado al finalizar el tema de Álgebra Relacional.

A diferencia del bloque anterior, estos problemas requieren analizar cuidadosamente el enunciado antes de comenzar a escribir la expresión algebraica.

En muchos casos existirán varias formas correctas de resolver el problema.

No obstante, algunas expresiones serán más sencillas, más elegantes o más eficientes que otras.

Durante la corrección en clase no solo se valorará que el resultado sea correcto, sino también la calidad del razonamiento seguido para llegar a la solución.

Se recomienda dedicar entre **5 y 7 minutos** a cada ejercicio.

---

## Problema 1

La dirección comercial desea obtener el nombre de los clientes de **Santander** que hayan comprado al menos un producto de la categoría ​**Periféricos**​.

El resultado no debe contener nombres repetidos.

Espacio para la solución:

............................................................................

............................................................................

............................................................................

............................................................................

............................................................................

---

## Problema 2

Mostrar el nombre de todos los productos vendidos a clientes de **Bilbao** cuyo precio sea superior a **50 €** e inferior a ​**200 €**​.

Espacio para la solución:

............................................................................

............................................................................

............................................................................

............................................................................

............................................................................

---

## Problema 3

La empresa quiere conocer qué clientes han comprado simultáneamente un **Ratón Inalámbrico** y un ​**SSD 1 TB**​.

No deben mostrarse otros atributos.

Espacio para la solución:

............................................................................

............................................................................

............................................................................

............................................................................

............................................................................

---

## Problema 4

Obtener el nombre de los productos que nunca han sido vendidos.

### Ayuda

No existe una relación que almacene directamente esa información.

Será necesario deducirla a partir del modelo de datos.

Espacio para la solución:

............................................................................

............................................................................

............................................................................

............................................................................

............................................................................

---

## Problema 5

Mostrar los nombres de los clientes que hayan comprado exclusivamente productos pertenecientes a la categoría ​**Periféricos**​.

### Observación

Este problema requiere un razonamiento más elaborado que los anteriores.

Antes de escribir la expresión, explica brevemente la estrategia que seguirías.

Espacio para la solución:

............................................................................

............................................................................

............................................................................

............................................................................

............................................................................

............................................................................

---

## Problema 6

La dirección desea identificar todos los productos comprados por clientes que hayan realizado más de un pedido.

### Nota

Con las herramientas estudiadas hasta este momento no es posible expresar completamente el concepto "más de un pedido".

Explica qué limitación del Álgebra Relacional clásica impide resolver el problema y qué característica adicional será necesaria estudiar más adelante para hacerlo.

Espacio para la respuesta:

............................................................................

............................................................................

............................................................................

............................................................................

---

## Problema 7

Diseña una expresión algebraica que obtenga:

* nombre del cliente;
* nombre del producto;
* precio.

Únicamente para pedidos realizados durante marzo de 2025.

Espacio para la solución:

............................................................................

............................................................................

............................................................................

............................................................................

............................................................................

---

## Problema 8

La empresa desea conocer los clientes que todavía no han realizado pedidos y que además residen en Santander.

Espacio para la solución:

............................................................................

............................................................................

............................................................................

............................................................................

............................................................................

---

## Problema 9

Explica cuál de las siguientes estrategias consideras más adecuada.

### Estrategia A

1. Realizar todos los JOIN.
2. Aplicar todas las selecciones.
3. Realizar la proyección final.

### Estrategia B

1. Aplicar primero las selecciones posibles.
2. Realizar posteriormente los JOIN necesarios.
3. Finalizar con la proyección.

Justifica tu respuesta utilizando los conceptos estudiados durante el tema.

Espacio para la respuesta:

............................................................................

............................................................................

............................................................................

............................................................................

............................................................................

---

## Problema 10

Observa la siguiente expresión algebraica.

```text
π NombreCliente
(
    σ Categoria='Periféricos'
    (
        Cliente
        ⋈
        Pedido
        ⋈
        LineaPedido
        ⋈
        Producto
    )
)
```

Sin resolverla completamente, responde:

* ¿Qué información intenta obtener?
* ¿Qué relaciones intervienen?
* ¿Qué operadores aparecen?
* ¿En qué orden conceptual se ejecutan?

Espacio para la respuesta:

............................................................................

............................................................................

............................................................................

............................................................................

............................................................................

---

## Preparación para el reto final

Si has llegado hasta este punto sin grandes dificultades, significa que ya dominas los fundamentos del Álgebra Relacional.

Solo queda enfrentarse a un problema integrador que combinará prácticamente todos los conceptos estudiados durante las dos últimas clases y este taller.

Ese reto será muy similar al tipo de ejercicio de desarrollo que podría aparecer como pregunta principal del examen.

---

## Ideas clave

* Los problemas reales rara vez se resuelven mediante un único operador.
* Antes de escribir una expresión conviene diseñar una estrategia de resolución.
* Existen varias soluciones correctas para una misma consulta, aunque algunas resultan más eficientes o más claras.
* Analizar el recorrido de la información entre las relaciones es una habilidad fundamental.
* Comprender las limitaciones del Álgebra Relacional prepara el camino para el estudio de SQL y de operadores más avanzados como la agregación y el agrupamiento.

