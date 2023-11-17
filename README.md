# Cloud Computing

Es la entrega de recursos tecnológicos bajo demanda (aplicaciones, servidores, redes, hasta centros de datos completos) a través de Internet y con la filosofía de pagar por uso de los recursos.

Es un modelo que permite un acceso a través de la red a un conjunto de recursos informáticos configurables que se pueden aprovisionar rápidamente y liberar con un mínimo esfuerzo de administración o interacción con el proveedor de servicios.

Se pueden contratar: Redes, servidores, almacenamiento, aplicaciones y servicios. Las características es que es un servicio propio bajo demanda, tiene acceso a través de Internet, recursos compartidos, gran escalabilidad y tiene un control total sobre los gastos en servicios.


## Modos de despliegue

- **Pública:** Se aprovechan los servicios de Cloud a través de Internet de un determinado proveedor de la nube, pero su uso es compartido por otras empresas.
- **Híbrida:** Mezcla Clouds privadas y públicas, trabajando de forma conjunta.
- **Privada:** La infraestructura de la nube se aprovisiona para uso exclusivo de una sola organización. Puede ser on-premise o podría ser administrada y operada por un proveedor de servicios.


## ¿Por qué seleccionar una determinada región?

Existen 4 motivos principales para seleccionar una región:

1. **Legales:** Privacidad de datos sensibles, datos religiosos ya que algunas leyes exigen que estos datos no salgan de dicha región.
2. **Precio:** El precio varía dependiendo de la región, influye el país, los impuestos, entre otras cosas.
3. **Cercanía al usuario final:** La latencia puede afectar dependiendo de la lejanía de nuestros usuarios finales respecto a la región que seleccionamos.
4. **Disponibilidad de servicios:** Algunos servicios no están disponibles en algunas regiones, debemos tener esto en cuenta cuando seleccionemos una.


## Trucos para gastar lo menos posible

- Utilizar la capa gratuita - servidores, BBDD, etc.
- Borrar o parar los componentes una vez hayas terminado.
- Utiliza instancias de tipo SPOT.
- Selecciona las opciones más económicas.


# Billing

Aquí podemos controlar todos los gastos que hemos generado consumiendo los recursos de AWS, aparecen gráficas que resumen los gastos por cada uno de los servicios.


# CloudWatch

Podemos llevar un control de los gastos que tenemos, generar notificaciones con un tope de gasto para que AWS nos informe una vez este límite sea excedido.


# Networking (VPC)

Toda la parte de redes se basa en las regiones, aquí usaremos los VPC (Virtual Private Cloud) que son básicamente una zona aislada donde puedo desplegar mis componentes, lo primero para trabajar con **AWS** sería ajustar estas redes privadas para nuestros componentes.

Estas VPC tendrán Bloques CIDR las cuales son un conjunto de direcciones IP (privadas) que se le asignan a dicha VPC.

Cada región está compuesta de AZ (zonas de disponibilidad), pueden tener de 2 a n zonas de disponibilidad. Aquí también podremos crear las subredes bien sean públicas o privadas.


## ACLs

Permiten dar acceso por redes de Amazon a nuestro VPC, podemos configurar reglas para habilitar o bloquear el acceso, además Amazon nos provee numerosas opciones para configurar nuestras reglas de entrada y salida.


## Gateway

Para que una subred tenga acceso a internet podemos usar Internet Gateway, la cual es un puente hacia internet. Aquellas redes que yo quiera que sean públicas (que puedan acceder a internet tanto de salida como de entrada).

Para que una subred sea pública se configura el Internet Gateway, esta provee una IP elástica (nos permite tener una IP fija por si la máquina se reinicia) y permitirá la conexión a internet desde nuestra VPC bien sea de entrada o salida. Para hacer esto es indispensable configurar una tabla de rutas ya que las VPCs heredan la Main Route Table, es necesario modificar esta Routes Table para que el Gateway apunte a ellas.