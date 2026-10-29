# VERSION 1

## Pasos comunes

**Paso 1.** Seleccionar los clientes de Madrid.

```text
ClientesMadrid ← σ_ciudad='Madrid'(CLIENTE)
```

**Paso 2.** Obtener los identificadores de los clientes de Madrid.

```text
IdsClientesMadrid ← π_id_cliente(ClientesMadrid)
```

**Paso 3.** Obtener las compras realizadas por clientes de Madrid, uniendo por el identificador del cliente.

```text
ComprasMadrid ← IdsClientesMadrid ⋈_{IdsClientesMadrid.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 4.** Obtener los identificadores de los productos comprados por clientes de Madrid.

```text
ProductosMadrid ← π_id_producto(ComprasMadrid)
```

**Paso 5.** Seleccionar los clientes de Valencia.

```text
ClientesValencia ← σ_ciudad='Valencia'(CLIENTE)
```

**Paso 6.** Obtener los identificadores de los clientes de Valencia.

```text
IdsClientesValencia ← π_id_cliente(ClientesValencia)
```

**Paso 7.** Obtener las compras realizadas por clientes de Valencia, uniendo por el identificador del cliente.

```text
ComprasValencia ← IdsClientesValencia ⋈_{IdsClientesValencia.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 8.** Obtener los identificadores de los productos comprados por clientes de Valencia.

```text
ProductosValencia ← π_id_producto(ComprasValencia)
```

## Ejercicio 1: Productos comprados por clientes de Madrid y Valencia

**Paso 9.** Obtener los identificadores de los productos comprados en ambas ciudades mediante la intersección.

```text
ProductosEnAmbasCiudades ← ProductosMadrid ∩ ProductosValencia
```

**Paso 10.** Obtener los datos de los productos comprados en ambas ciudades, uniendo por el identificador del producto.

```text
ProductosCompradosEnAmbasCiudades ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosEnAmbasCiudades.id_producto} ProductosEnAmbasCiudades
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio1 ← π_id_producto,nombre_producto(ProductosCompradosEnAmbasCiudades)
```

## Ejercicio 2: Productos comprados por clientes de Madrid, pero no de Valencia

**Paso 9.** Obtener los identificadores de los productos comprados en Madrid, pero no en Valencia, mediante la diferencia.

```text
ProductosSoloMadrid ← ProductosMadrid − ProductosValencia
```

**Paso 10.** Obtener los datos de los productos comprados exclusivamente en Madrid, uniendo por el identificador del producto.

```text
ProductosCompradosSoloMadrid ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosSoloMadrid.id_producto} ProductosSoloMadrid
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio2 ← π_id_producto,nombre_producto(ProductosCompradosSoloMadrid)
```

---

# VERSION 2

## Pasos comunes

**Paso 1.** Seleccionar los clientes de Sevilla.

```text
ClientesSevilla ← σ_ciudad='Sevilla'(CLIENTE)
```

**Paso 2.** Obtener los identificadores de los clientes de Sevilla.

```text
IdsClientesSevilla ← π_id_cliente(ClientesSevilla)
```

**Paso 3.** Obtener las compras realizadas por clientes de Sevilla, uniendo por el identificador del cliente.

```text
ComprasSevilla ← IdsClientesSevilla ⋈_{IdsClientesSevilla.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 4.** Obtener los identificadores de los productos comprados por clientes de Sevilla.

```text
ProductosSevilla ← π_id_producto(ComprasSevilla)
```

**Paso 5.** Seleccionar los clientes de Málaga.

```text
ClientesMalaga ← σ_ciudad='Málaga'(CLIENTE)
```

**Paso 6.** Obtener los identificadores de los clientes de Málaga.

```text
IdsClientesMalaga ← π_id_cliente(ClientesMalaga)
```

**Paso 7.** Obtener las compras realizadas por clientes de Málaga, uniendo por el identificador del cliente.

```text
ComprasMalaga ← IdsClientesMalaga ⋈_{IdsClientesMalaga.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 8.** Obtener los identificadores de los productos comprados por clientes de Málaga.

```text
ProductosMalaga ← π_id_producto(ComprasMalaga)
```

## Ejercicio 1: Productos comprados por clientes de Sevilla y Málaga

**Paso 9.** Obtener los identificadores de los productos comprados en ambas ciudades mediante la intersección.

```text
ProductosEnAmbasCiudades ← ProductosSevilla ∩ ProductosMalaga
```

**Paso 10.** Obtener los datos de los productos comprados en ambas ciudades, uniendo por el identificador del producto.

```text
ProductosCompradosEnAmbasCiudades ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosEnAmbasCiudades.id_producto} ProductosEnAmbasCiudades
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio1 ← π_id_producto,nombre_producto(ProductosCompradosEnAmbasCiudades)
```

## Ejercicio 2: Productos comprados por clientes de Sevilla, pero no de Málaga

**Paso 9.** Obtener los identificadores de los productos comprados en Sevilla, pero no en Málaga, mediante la diferencia.

```text
ProductosSoloSevilla ← ProductosSevilla − ProductosMalaga
```

**Paso 10.** Obtener los datos de los productos comprados exclusivamente en Sevilla, uniendo por el identificador del producto.

```text
ProductosCompradosSoloSevilla ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosSoloSevilla.id_producto} ProductosSoloSevilla
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio2 ← π_id_producto,nombre_producto(ProductosCompradosSoloSevilla)
```

---

# VERSION 3

## Pasos comunes

**Paso 1.** Seleccionar los clientes de Bilbao.

```text
ClientesBilbao ← σ_ciudad='Bilbao'(CLIENTE)
```

**Paso 2.** Obtener los identificadores de los clientes de Bilbao.

```text
IdsClientesBilbao ← π_id_cliente(ClientesBilbao)
```

**Paso 3.** Obtener las compras realizadas por clientes de Bilbao, uniendo por el identificador del cliente.

```text
ComprasBilbao ← IdsClientesBilbao ⋈_{IdsClientesBilbao.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 4.** Obtener los identificadores de los productos comprados por clientes de Bilbao.

```text
ProductosBilbao ← π_id_producto(ComprasBilbao)
```

**Paso 5.** Seleccionar los clientes de Zaragoza.

```text
ClientesZaragoza ← σ_ciudad='Zaragoza'(CLIENTE)
```

**Paso 6.** Obtener los identificadores de los clientes de Zaragoza.

```text
IdsClientesZaragoza ← π_id_cliente(ClientesZaragoza)
```

**Paso 7.** Obtener las compras realizadas por clientes de Zaragoza, uniendo por el identificador del cliente.

```text
ComprasZaragoza ← IdsClientesZaragoza ⋈_{IdsClientesZaragoza.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 8.** Obtener los identificadores de los productos comprados por clientes de Zaragoza.

```text
ProductosZaragoza ← π_id_producto(ComprasZaragoza)
```

## Ejercicio 1: Productos comprados por clientes de Bilbao y Zaragoza

**Paso 9.** Obtener los identificadores de los productos comprados en ambas ciudades mediante la intersección.

```text
ProductosEnAmbasCiudades ← ProductosBilbao ∩ ProductosZaragoza
```

**Paso 10.** Obtener los datos de los productos comprados en ambas ciudades, uniendo por el identificador del producto.

```text
ProductosCompradosEnAmbasCiudades ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosEnAmbasCiudades.id_producto} ProductosEnAmbasCiudades
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio1 ← π_id_producto,nombre_producto(ProductosCompradosEnAmbasCiudades)
```

## Ejercicio 2: Productos comprados por clientes de Bilbao, pero no de Zaragoza

**Paso 9.** Obtener los identificadores de los productos comprados en Bilbao, pero no en Zaragoza, mediante la diferencia.

```text
ProductosSoloBilbao ← ProductosBilbao − ProductosZaragoza
```

**Paso 10.** Obtener los datos de los productos comprados exclusivamente en Bilbao, uniendo por el identificador del producto.

```text
ProductosCompradosSoloBilbao ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosSoloBilbao.id_producto} ProductosSoloBilbao
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio2 ← π_id_producto,nombre_producto(ProductosCompradosSoloBilbao)
```

---

# VERSION 4

## Pasos comunes

**Paso 1.** Seleccionar los clientes de Barcelona.

```text
ClientesBarcelona ← σ_ciudad='Barcelona'(CLIENTE)
```

**Paso 2.** Obtener los identificadores de los clientes de Barcelona.

```text
IdsClientesBarcelona ← π_id_cliente(ClientesBarcelona)
```

**Paso 3.** Obtener las compras realizadas por clientes de Barcelona, uniendo por el identificador del cliente.

```text
ComprasBarcelona ← IdsClientesBarcelona ⋈_{IdsClientesBarcelona.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 4.** Obtener los identificadores de los productos comprados por clientes de Barcelona.

```text
ProductosBarcelona ← π_id_producto(ComprasBarcelona)
```

**Paso 5.** Seleccionar los clientes de Granada.

```text
ClientesGranada ← σ_ciudad='Granada'(CLIENTE)
```

**Paso 6.** Obtener los identificadores de los clientes de Granada.

```text
IdsClientesGranada ← π_id_cliente(ClientesGranada)
```

**Paso 7.** Obtener las compras realizadas por clientes de Granada, uniendo por el identificador del cliente.

```text
ComprasGranada ← IdsClientesGranada ⋈_{IdsClientesGranada.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 8.** Obtener los identificadores de los productos comprados por clientes de Granada.

```text
ProductosGranada ← π_id_producto(ComprasGranada)
```

## Ejercicio 1: Productos comprados por clientes de Barcelona y Granada

**Paso 9.** Obtener los identificadores de los productos comprados en ambas ciudades mediante la intersección.

```text
ProductosEnAmbasCiudades ← ProductosBarcelona ∩ ProductosGranada
```

**Paso 10.** Obtener los datos de los productos comprados en ambas ciudades, uniendo por el identificador del producto.

```text
ProductosCompradosEnAmbasCiudades ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosEnAmbasCiudades.id_producto} ProductosEnAmbasCiudades
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio1 ← π_id_producto,nombre_producto(ProductosCompradosEnAmbasCiudades)
```

## Ejercicio 2: Productos comprados por clientes de Barcelona, pero no de Granada

**Paso 9.** Obtener los identificadores de los productos comprados en Barcelona, pero no en Granada, mediante la diferencia.

```text
ProductosSoloBarcelona ← ProductosBarcelona − ProductosGranada
```

**Paso 10.** Obtener los datos de los productos comprados exclusivamente en Barcelona, uniendo por el identificador del producto.

```text
ProductosCompradosSoloBarcelona ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosSoloBarcelona.id_producto} ProductosSoloBarcelona
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio2 ← π_id_producto,nombre_producto(ProductosCompradosSoloBarcelona)
```

---

# VERSION 5

## Pasos comunes

**Paso 1.** Seleccionar los clientes de Salamanca.

```text
ClientesSalamanca ← σ_ciudad='Salamanca'(CLIENTE)
```

**Paso 2.** Obtener los identificadores de los clientes de Salamanca.

```text
IdsClientesSalamanca ← π_id_cliente(ClientesSalamanca)
```

**Paso 3.** Obtener las compras realizadas por clientes de Salamanca, uniendo por el identificador del cliente.

```text
ComprasSalamanca ← IdsClientesSalamanca ⋈_{IdsClientesSalamanca.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 4.** Obtener los identificadores de los productos comprados por clientes de Salamanca.

```text
ProductosSalamanca ← π_id_producto(ComprasSalamanca)
```

**Paso 5.** Seleccionar los clientes de Valladolid.

```text
ClientesValladolid ← σ_ciudad='Valladolid'(CLIENTE)
```

**Paso 6.** Obtener los identificadores de los clientes de Valladolid.

```text
IdsClientesValladolid ← π_id_cliente(ClientesValladolid)
```

**Paso 7.** Obtener las compras realizadas por clientes de Valladolid, uniendo por el identificador del cliente.

```text
ComprasValladolid ← IdsClientesValladolid ⋈_{IdsClientesValladolid.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 8.** Obtener los identificadores de los productos comprados por clientes de Valladolid.

```text
ProductosValladolid ← π_id_producto(ComprasValladolid)
```

## Ejercicio 1: Productos comprados por clientes de Salamanca y Valladolid

**Paso 9.** Obtener los identificadores de los productos comprados en ambas ciudades mediante la intersección.

```text
ProductosEnAmbasCiudades ← ProductosSalamanca ∩ ProductosValladolid
```

**Paso 10.** Obtener los datos de los productos comprados en ambas ciudades, uniendo por el identificador del producto.

```text
ProductosCompradosEnAmbasCiudades ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosEnAmbasCiudades.id_producto} ProductosEnAmbasCiudades
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio1 ← π_id_producto,nombre_producto(ProductosCompradosEnAmbasCiudades)
```

## Ejercicio 2: Productos comprados por clientes de Salamanca, pero no de Valladolid

**Paso 9.** Obtener los identificadores de los productos comprados en Salamanca, pero no en Valladolid, mediante la diferencia.

```text
ProductosSoloSalamanca ← ProductosSalamanca − ProductosValladolid
```

**Paso 10.** Obtener los datos de los productos comprados exclusivamente en Salamanca, uniendo por el identificador del producto.

```text
ProductosCompradosSoloSalamanca ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosSoloSalamanca.id_producto} ProductosSoloSalamanca
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio2 ← π_id_producto,nombre_producto(ProductosCompradosSoloSalamanca)
```

---

# VERSION 6

## Pasos comunes

**Paso 1.** Seleccionar los clientes de Córdoba.

```text
ClientesCordoba ← σ_ciudad='Córdoba'(CLIENTE)
```

**Paso 2.** Obtener los identificadores de los clientes de Córdoba.

```text
IdsClientesCordoba ← π_id_cliente(ClientesCordoba)
```

**Paso 3.** Obtener las compras realizadas por clientes de Córdoba, uniendo por el identificador del cliente.

```text
ComprasCordoba ← IdsClientesCordoba ⋈_{IdsClientesCordoba.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 4.** Obtener los identificadores de los productos comprados por clientes de Córdoba.

```text
ProductosCordoba ← π_id_producto(ComprasCordoba)
```

**Paso 5.** Seleccionar los clientes de Alicante.

```text
ClientesAlicante ← σ_ciudad='Alicante'(CLIENTE)
```

**Paso 6.** Obtener los identificadores de los clientes de Alicante.

```text
IdsClientesAlicante ← π_id_cliente(ClientesAlicante)
```

**Paso 7.** Obtener las compras realizadas por clientes de Alicante, uniendo por el identificador del cliente.

```text
ComprasAlicante ← IdsClientesAlicante ⋈_{IdsClientesAlicante.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 8.** Obtener los identificadores de los productos comprados por clientes de Alicante.

```text
ProductosAlicante ← π_id_producto(ComprasAlicante)
```

## Ejercicio 1: Productos comprados por clientes de Córdoba y Alicante

**Paso 9.** Obtener los identificadores de los productos comprados en ambas ciudades mediante la intersección.

```text
ProductosEnAmbasCiudades ← ProductosCordoba ∩ ProductosAlicante
```

**Paso 10.** Obtener los datos de los productos comprados en ambas ciudades, uniendo por el identificador del producto.

```text
ProductosCompradosEnAmbasCiudades ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosEnAmbasCiudades.id_producto} ProductosEnAmbasCiudades
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio1 ← π_id_producto,nombre_producto(ProductosCompradosEnAmbasCiudades)
```

## Ejercicio 2: Productos comprados por clientes de Córdoba, pero no de Alicante

**Paso 9.** Obtener los identificadores de los productos comprados en Córdoba, pero no en Alicante, mediante la diferencia.

```text
ProductosSoloCordoba ← ProductosCordoba − ProductosAlicante
```

**Paso 10.** Obtener los datos de los productos comprados exclusivamente en Córdoba, uniendo por el identificador del producto.

```text
ProductosCompradosSoloCordoba ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosSoloCordoba.id_producto} ProductosSoloCordoba
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio2 ← π_id_producto,nombre_producto(ProductosCompradosSoloCordoba)
```

---

# VERSION 7

## Pasos comunes

**Paso 1.** Seleccionar los clientes de Murcia.

```text
ClientesMurcia ← σ_ciudad='Murcia'(CLIENTE)
```

**Paso 2.** Obtener los identificadores de los clientes de Murcia.

```text
IdsClientesMurcia ← π_id_cliente(ClientesMurcia)
```

**Paso 3.** Obtener las compras realizadas por clientes de Murcia, uniendo por el identificador del cliente.

```text
ComprasMurcia ← IdsClientesMurcia ⋈_{IdsClientesMurcia.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 4.** Obtener los identificadores de los productos comprados por clientes de Murcia.

```text
ProductosMurcia ← π_id_producto(ComprasMurcia)
```

**Paso 5.** Seleccionar los clientes de Oviedo.

```text
ClientesOviedo ← σ_ciudad='Oviedo'(CLIENTE)
```

**Paso 6.** Obtener los identificadores de los clientes de Oviedo.

```text
IdsClientesOviedo ← π_id_cliente(ClientesOviedo)
```

**Paso 7.** Obtener las compras realizadas por clientes de Oviedo, uniendo por el identificador del cliente.

```text
ComprasOviedo ← IdsClientesOviedo ⋈_{IdsClientesOviedo.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 8.** Obtener los identificadores de los productos comprados por clientes de Oviedo.

```text
ProductosOviedo ← π_id_producto(ComprasOviedo)
```

## Ejercicio 1: Productos comprados por clientes de Murcia y Oviedo

**Paso 9.** Obtener los identificadores de los productos comprados en ambas ciudades mediante la intersección.

```text
ProductosEnAmbasCiudades ← ProductosMurcia ∩ ProductosOviedo
```

**Paso 10.** Obtener los datos de los productos comprados en ambas ciudades, uniendo por el identificador del producto.

```text
ProductosCompradosEnAmbasCiudades ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosEnAmbasCiudades.id_producto} ProductosEnAmbasCiudades
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio1 ← π_id_producto,nombre_producto(ProductosCompradosEnAmbasCiudades)
```

## Ejercicio 2: Productos comprados por clientes de Murcia, pero no de Oviedo

**Paso 9.** Obtener los identificadores de los productos comprados en Murcia, pero no en Oviedo, mediante la diferencia.

```text
ProductosSoloMurcia ← ProductosMurcia − ProductosOviedo
```

**Paso 10.** Obtener los datos de los productos comprados exclusivamente en Murcia, uniendo por el identificador del producto.

```text
ProductosCompradosSoloMurcia ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosSoloMurcia.id_producto} ProductosSoloMurcia
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio2 ← π_id_producto,nombre_producto(ProductosCompradosSoloMurcia)
```

---

# VERSION 8

## Pasos comunes

**Paso 1.** Seleccionar los clientes de Vigo.

```text
ClientesVigo ← σ_ciudad='Vigo'(CLIENTE)
```

**Paso 2.** Obtener los identificadores de los clientes de Vigo.

```text
IdsClientesVigo ← π_id_cliente(ClientesVigo)
```

**Paso 3.** Obtener las compras realizadas por clientes de Vigo, uniendo por el identificador del cliente.

```text
ComprasVigo ← IdsClientesVigo ⋈_{IdsClientesVigo.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 4.** Obtener los identificadores de los productos comprados por clientes de Vigo.

```text
ProductosVigo ← π_id_producto(ComprasVigo)
```

**Paso 5.** Seleccionar los clientes de Cádiz.

```text
ClientesCadiz ← σ_ciudad='Cádiz'(CLIENTE)
```

**Paso 6.** Obtener los identificadores de los clientes de Cádiz.

```text
IdsClientesCadiz ← π_id_cliente(ClientesCadiz)
```

**Paso 7.** Obtener las compras realizadas por clientes de Cádiz, uniendo por el identificador del cliente.

```text
ComprasCadiz ← IdsClientesCadiz ⋈_{IdsClientesCadiz.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 8.** Obtener los identificadores de los productos comprados por clientes de Cádiz.

```text
ProductosCadiz ← π_id_producto(ComprasCadiz)
```

## Ejercicio 1: Productos comprados por clientes de Vigo y Cádiz

**Paso 9.** Obtener los identificadores de los productos comprados en ambas ciudades mediante la intersección.

```text
ProductosEnAmbasCiudades ← ProductosVigo ∩ ProductosCadiz
```

**Paso 10.** Obtener los datos de los productos comprados en ambas ciudades, uniendo por el identificador del producto.

```text
ProductosCompradosEnAmbasCiudades ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosEnAmbasCiudades.id_producto} ProductosEnAmbasCiudades
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio1 ← π_id_producto,nombre_producto(ProductosCompradosEnAmbasCiudades)
```

## Ejercicio 2: Productos comprados por clientes de Vigo, pero no de Cádiz

**Paso 9.** Obtener los identificadores de los productos comprados en Vigo, pero no en Cádiz, mediante la diferencia.

```text
ProductosSoloVigo ← ProductosVigo − ProductosCadiz
```

**Paso 10.** Obtener los datos de los productos comprados exclusivamente en Vigo, uniendo por el identificador del producto.

```text
ProductosCompradosSoloVigo ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosSoloVigo.id_producto} ProductosSoloVigo
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio2 ← π_id_producto,nombre_producto(ProductosCompradosSoloVigo)
```

---

# VERSION 9

## Pasos comunes

**Paso 1.** Seleccionar los clientes de Toledo.

```text
ClientesToledo ← σ_ciudad='Toledo'(CLIENTE)
```

**Paso 2.** Obtener los identificadores de los clientes de Toledo.

```text
IdsClientesToledo ← π_id_cliente(ClientesToledo)
```

**Paso 3.** Obtener las compras realizadas por clientes de Toledo, uniendo por el identificador del cliente.

```text
ComprasToledo ← IdsClientesToledo ⋈_{IdsClientesToledo.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 4.** Obtener los identificadores de los productos comprados por clientes de Toledo.

```text
ProductosToledo ← π_id_producto(ComprasToledo)
```

**Paso 5.** Seleccionar los clientes de Burgos.

```text
ClientesBurgos ← σ_ciudad='Burgos'(CLIENTE)
```

**Paso 6.** Obtener los identificadores de los clientes de Burgos.

```text
IdsClientesBurgos ← π_id_cliente(ClientesBurgos)
```

**Paso 7.** Obtener las compras realizadas por clientes de Burgos, uniendo por el identificador del cliente.

```text
ComprasBurgos ← IdsClientesBurgos ⋈_{IdsClientesBurgos.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 8.** Obtener los identificadores de los productos comprados por clientes de Burgos.

```text
ProductosBurgos ← π_id_producto(ComprasBurgos)
```

## Ejercicio 1: Productos comprados por clientes de Toledo y Burgos

**Paso 9.** Obtener los identificadores de los productos comprados en ambas ciudades mediante la intersección.

```text
ProductosEnAmbasCiudades ← ProductosToledo ∩ ProductosBurgos
```

**Paso 10.** Obtener los datos de los productos comprados en ambas ciudades, uniendo por el identificador del producto.

```text
ProductosCompradosEnAmbasCiudades ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosEnAmbasCiudades.id_producto} ProductosEnAmbasCiudades
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio1 ← π_id_producto,nombre_producto(ProductosCompradosEnAmbasCiudades)
```

## Ejercicio 2: Productos comprados por clientes de Toledo, pero no de Burgos

**Paso 9.** Obtener los identificadores de los productos comprados en Toledo, pero no en Burgos, mediante la diferencia.

```text
ProductosSoloToledo ← ProductosToledo − ProductosBurgos
```

**Paso 10.** Obtener los datos de los productos comprados exclusivamente en Toledo, uniendo por el identificador del producto.

```text
ProductosCompradosSoloToledo ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosSoloToledo.id_producto} ProductosSoloToledo
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio2 ← π_id_producto,nombre_producto(ProductosCompradosSoloToledo)
```

---

# VERSION 10

## Pasos comunes

**Paso 1.** Seleccionar los clientes de Logroño.

```text
ClientesLogrono ← σ_ciudad='Logroño'(CLIENTE)
```

**Paso 2.** Obtener los identificadores de los clientes de Logroño.

```text
IdsClientesLogrono ← π_id_cliente(ClientesLogrono)
```

**Paso 3.** Obtener las compras realizadas por clientes de Logroño, uniendo por el identificador del cliente.

```text
ComprasLogrono ← IdsClientesLogrono ⋈_{IdsClientesLogrono.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 4.** Obtener los identificadores de los productos comprados por clientes de Logroño.

```text
ProductosLogrono ← π_id_producto(ComprasLogrono)
```

**Paso 5.** Seleccionar los clientes de Pamplona.

```text
ClientesPamplona ← σ_ciudad='Pamplona'(CLIENTE)
```

**Paso 6.** Obtener los identificadores de los clientes de Pamplona.

```text
IdsClientesPamplona ← π_id_cliente(ClientesPamplona)
```

**Paso 7.** Obtener las compras realizadas por clientes de Pamplona, uniendo por el identificador del cliente.

```text
ComprasPamplona ← IdsClientesPamplona ⋈_{IdsClientesPamplona.id_cliente = COMPRA.id_cliente} COMPRA
```

**Paso 8.** Obtener los identificadores de los productos comprados por clientes de Pamplona.

```text
ProductosPamplona ← π_id_producto(ComprasPamplona)
```

## Ejercicio 1: Productos comprados por clientes de Logroño y Pamplona

**Paso 9.** Obtener los identificadores de los productos comprados en ambas ciudades mediante la intersección.

```text
ProductosEnAmbasCiudades ← ProductosLogrono ∩ ProductosPamplona
```

**Paso 10.** Obtener los datos de los productos comprados en ambas ciudades, uniendo por el identificador del producto.

```text
ProductosCompradosEnAmbasCiudades ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosEnAmbasCiudades.id_producto} ProductosEnAmbasCiudades
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio1 ← π_id_producto,nombre_producto(ProductosCompradosEnAmbasCiudades)
```

## Ejercicio 2: Productos comprados por clientes de Logroño, pero no de Pamplona

**Paso 9.** Obtener los identificadores de los productos comprados en Logroño, pero no en Pamplona, mediante la diferencia.

```text
ProductosSoloLogrono ← ProductosLogrono − ProductosPamplona
```

**Paso 10.** Obtener los datos de los productos comprados exclusivamente en Logroño, uniendo por el identificador del producto.

```text
ProductosCompradosSoloLogrono ← PRODUCTO ⋈_{PRODUCTO.id_producto = ProductosSoloLogrono.id_producto} ProductosSoloLogrono
```

**Paso 11.** Proyectar el identificador y el nombre de los productos resultantes.

```text
ResultadoEjercicio2 ← π_id_producto,nombre_producto(ProductosCompradosSoloLogrono)
```

## Nota de notación

Las condiciones de unión se han explicitado para evitar ambigüedades. Se presupone que `CLIENTE` contiene `id_cliente` y `ciudad`, que `COMPRA` contiene `id_cliente` e `id_producto`, y que `PRODUCTO` contiene `id_producto` y `nombre_producto`. Las intersecciones y diferencias se aplican sobre relaciones unarias compatibles que contienen únicamente `id_producto`.


