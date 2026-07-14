# Costes y modelos de pago

## Introducción

Uno de los principales argumentos a favor de los servicios cloud es que permiten disponer de infraestructura informática sin realizar una gran inversión inicial.

Sin embargo, esto no significa que la nube sea siempre más barata.

En realidad, el modelo económico cambia por completo.

Mientras que en una infraestructura tradicional la mayor parte del gasto se realiza al principio mediante la compra de servidores, en la nube es habitual pagar únicamente por los recursos utilizados.

Comprender cómo funcionan estos modelos de pago resulta fundamental para tomar decisiones técnicas y económicas acertadas.

## Del modelo CAPEX al modelo OPEX

Tradicionalmente, las empresas adquirían sus propios servidores.

Esta inversión inicial recibe el nombre de **CAPEX** (*Capital Expenditure*).

Incluye gastos como:

- compra de servidores,
- sistemas de almacenamiento,
- redes,
- licencias,
- instalación del centro de datos.

Posteriormente aparecen los costes de mantenimiento.

En la nube, gran parte de esta inversión desaparece y se sustituye por un modelo de **OPEX** (*Operational Expenditure*), basado en gastos operativos periódicos.

La empresa paga por utilizar un servicio en lugar de comprar toda la infraestructura.

## ¿Por qué resulta atractivo este modelo?

Imaginemos que TechShop acaba de comenzar su actividad.

No sabe cuántos clientes tendrá durante el primer año.

Comprar un servidor muy potente puede resultar innecesario.

En cambio, mediante un servicio cloud puede contratar una pequeña instancia y aumentar su capacidad únicamente cuando sea necesario.

Esto reduce el riesgo asociado a la inversión inicial.

## ¿Qué factores influyen en el coste?

Aunque cada proveedor utiliza su propia política de precios, normalmente intervienen varios factores.

### Potencia de la instancia

Una máquina con:

- más memoria,
- más procesadores,
- mayor capacidad de cálculo,

tendrá un coste superior.

### Almacenamiento

El espacio ocupado por la base de datos también influye en el precio.

No cuesta lo mismo almacenar:

- 20 GB,
- 500 GB,
- 5 TB.

Además, algunos tipos de almacenamiento ofrecen mayor rendimiento y, por tanto, un precio más elevado.

### Copias de seguridad

Las copias automáticas suelen incluir un determinado espacio gratuito.

Superado ese límite, el almacenamiento adicional puede incrementar el coste.

### Transferencia de datos

En determinadas situaciones, especialmente cuando la información sale del proveedor cloud hacia Internet o hacia otras regiones, puede aplicarse un coste asociado al tráfico de datos.

### Alta disponibilidad

Mantener una segunda instancia preparada para asumir el servicio requiere recursos adicionales.

Por ello, las configuraciones con alta disponibilidad suelen ser más costosas que una única instancia.

## Pago por uso

Una característica muy habitual consiste en el denominado **pay-as-you-go**.

Este modelo significa que la empresa paga únicamente por los recursos realmente consumidos.

Si una aplicación pequeña utiliza pocos recursos, el coste también será reducido.

Si el sistema crece, el gasto aumentará proporcionalmente.

Este comportamiento aporta una gran flexibilidad.

## Ventajas económicas

El modelo cloud presenta diversas ventajas.

### Menor inversión inicial

No es necesario comprar servidores físicos.

### Crecimiento progresivo

La infraestructura puede ampliarse conforme aumenta la demanda.

### Costes previsibles

Los proveedores ofrecen herramientas para estimar el gasto mensual.

### Pago ajustado al consumo

No resulta necesario adquirir recursos muy superiores a los realmente utilizados.

## Posibles inconvenientes

El modelo cloud también presenta algunos riesgos.

### Crecimiento inesperado del gasto

Si la aplicación incrementa mucho su consumo y no se supervisa adecuadamente, la factura puede aumentar considerablemente.

### Recursos infrautilizados

Contratar una instancia mucho más potente de lo necesario supone pagar por capacidad que nunca llega a utilizarse.

### Dependencia del proveedor

Migrar una gran infraestructura hacia otro proveedor puede requerir tiempo y recursos.

Por ello conviene planificar cuidadosamente la arquitectura desde el principio.

## Ejemplo práctico

Supongamos que TechShop comienza con:

- una pequeña base de datos,
- pocos usuarios,
- tráfico reducido.

Inicialmente contrata una instancia modesta.

Durante el siguiente año el número de clientes se multiplica.

La empresa amplía gradualmente:

- memoria,
- almacenamiento,
- capacidad de procesamiento.

Gracias al modelo de pago por uso evita realizar una gran inversión inicial y adapta el coste al crecimiento real del negocio.

## ¿Cómo controlar los costes?

Las organizaciones suelen aplicar diversas estrategias.

Por ejemplo:

- revisar periódicamente el consumo,
- eliminar recursos que ya no se utilizan,
- elegir correctamente el tamaño de las instancias,
- automatizar el apagado de entornos de desarrollo cuando no son necesarios,
- utilizar herramientas de monitorización de costes.

La optimización económica forma parte de la administración de infraestructuras cloud.

## Buenas prácticas

- Dimensionar correctamente las instancias.
- Supervisar regularmente el gasto.
- Revisar el almacenamiento utilizado.
- Automatizar la eliminación de recursos temporales.
- Analizar periódicamente si la configuración continúa siendo adecuada para la carga real.

## Conclusiones

Los servicios cloud transforman el modelo económico de las bases de datos al sustituir grandes inversiones iniciales por pagos periódicos asociados al consumo. Esta flexibilidad facilita el crecimiento de las aplicaciones, aunque también exige una supervisión constante para evitar costes innecesarios y aprovechar eficientemente los recursos contratados.

## Ideas clave

- La nube sustituye gran parte del CAPEX por OPEX.
- El coste depende de los recursos utilizados.
- El modelo de pago por uso aporta flexibilidad.
- La alta disponibilidad y el almacenamiento adicional incrementan el precio.
- Supervisar el consumo resulta esencial para controlar el gasto.

