# Historia de las Bases de Datos

- **Años 60–70**: archivos planos, luego modelos jerárquicos (IMS) y de red (CODASYL).
- **Años 70–80**: nacimiento del modelo relacional (E.F. Codd, 1970).
- **Años 90–2000**: bases distribuidas, cliente-servidor, data warehouses.
- **Actualidad**: NoSQL, bases en la nube, Big Data, multimodelo.

La historia muestra la evolución desde el almacenamiento rudimentario hasta sistemas complejos para grandes volúmenes de datos.


1880 → Censo USA: 7 años de procesamiento
1884 → Hollerith inventa la máquina perforadora
1890 → Resultados en 2,5 años
1950 → Cintas magnéticas (procesos secuenciales)
1960 → Discos → acceso directo
1970 → Codd propone el modelo relacional
1980 → Tablas, filas, columnas → DB relacionales dominan
1990 → SQL y bases orientadas a objetos
2000 → Web, Big Data, bases distribuidas
2020 → NoSQL, NewSQL, bases en la nube

## Diagrama comparativo: Archivos planos vs Modelo relacional

```
Archivos planos                Modelo relacional
+-----------+                  +-------------------+
| Cliente   |                  |   Tabla CLIENTE   |
| Nombre    |                  | id_cliente (PK)   |
| Dirección |   ---> cambio    | nombre            |
| Teléfono  |                  | dirección         |
+-----------+                  | teléfono          |
                               +-------------------+
```
