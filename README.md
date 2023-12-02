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


# EC2

Es el entorno de máquinas virtuales que podemos usar en **AWS**. Se utiliza para bases de datos, inteligencia artificial, entre otras cosas.


## Tipos de instancias

Hay varias opciones para crear nuestras máquinas virtuales, a su vez estas tienen variaciones en el tamaño de la instancia, lo que nos permite modificar la cantidad de CPUs, la memoria RAM, la instancia de almacenamiento, la bandaancha (Gbps) y la EBS. Para más información podemos ver detalladamente cada tipo de instancia [aquí](https://aws.amazon.com/es/ec2/instance-types/?gclid=CjwKCAiAu9yqBhBmEiwAHTx5pxVFUVVFN4Ji9m18oWHk70m35lU0HDkhqMLjsg4cp56B1SNvRQ4DixoC58IQAvD_BwE&trk=47bc9fe4-4562-4b29-8c2d-b78e700efe22&sc_channel=ps&ef_id=CjwKCAiAu9yqBhBmEiwAHTx5pxVFUVVFN4Ji9m18oWHk70m35lU0HDkhqMLjsg4cp56B1SNvRQ4DixoC58IQAvD_BwE:G:s&s_kwcid=AL!4422!3!647999771943!e!!g!!aws%20ec2%20instance%20types!19685310464!143348646222).


## Nitro System

Es la plataforma en la que se ejecutan las instancias EC2 de Amazon, es una combinación de hardware dedicado y también hypervisors para que funcionen las máquinas virtuales correctamente, es decir que es algo similar a VMware.


## Launch Instance

Cuando estamos creando una instancia EC2 tendremos que seleccionar varias cosas:

### Nombre y tags
Asignar un nombre y también tags a los que podemos colocar unos resource types para que el tag sea visible en todos ellos.

### AMIs
Seleccionar una AMI (sistema operativo de la máquina virtual), cada una tiene unos beneficios y ejecutará mejor algunas tareas, importante tenerlo en cuenta. Amazon tiene su propia AMI (Amazon Linux), esta fue desarrollada para aprovechar al máximo el potencial de EC2.

### Tipo de instancia
Seleccionar el tipo de máquina, aquí se muestran todas las opciones que aparecen en el link de los tipos de instancias

### Key Pair
Configurar Key Pair, ya que con estas claves nos podremos conectar en remoto. Esto genera un archivo que podremos usar para conectarnos al servidor, por lo tanto, si perdemos el archivo no nos podremos conectar al servidor, por lo que es importante guardar una copia en un lugar seguro.

AWS nos genera un archivo .pem o .ppk, podemos descargar el .pem y luego si requerimos conectarnos con PuTTY se puede convertir este archivo a .ppk.

### Configuración de red
Debemos configurar la red de nuestra instancia, asociar una VPC, si queremos subredes asignarlas también. Si deseamos que nuestra máquina permita el acceso desde internet tendremos que habilitar la opción de auto asignar una IP pública.

También está la opción grupos de seguridad, los cuales son unos firewall (componentes que tienen una serie de reglas para permitir o impedir el acceso a nuestra instancia). Podemos crear uno nuevo o seleccionar uno existente.

Cada grupo puede tener varias reglas por si necesitamos customizar varios tipos de acceso.

### Almacenamiento
AWS nos brinda opciones con SSD, HDD y magnetic storage, es importante tener claro lo que requerimos hacer para seleccionar la mejor opción. Aquí también podremos configurar instancias EBS para almacenamiento de ficheros directamente en nuestra máquina virtual.

### Opciones avanzadas
Se pueden asignar instancias de tipo Spot, podemos configurar cómo debe comportarse la instancia cuando se apaga o la ponemos en modo hibernar.

## Conexiones

### Linux
```bash
ssh -i "nuestroArchivo.pem" aws-user@aws-route.compute-1.amazonaws.com

yum update o apt update
```

### Windows
Con la aplicación de conexión a un escritorio remoto lo podemos hacer fácilmente.


## NAT Gateway

Una subred pública puede usar un Internet Gateway para salir a internet, sin embargo una red privada no tendrá acceso a internet, por lo que se configura un NAT Gateway para poder llegar a internet o VPNs, etc. Una vez configurado el NAT se conecta al Internet Gateway para completar la configuración.


## IPs elásticas

Es una IP pública fija, en cambio las IP públicas normales son dinámicas. Son útiles para que una máquina o componente no cambie de IP cada que se apague y encienda. Una IP elástica siempre será necesaria para poder crear el NAT Gateway.


## Network interfaces

Son tarjetas de red virtuales, normalmente cuando creamos una instancia EC2 estas ya traen una tarjeta de red. Cada tipo de instancia tiene un máximo de interfaces de redes, es importante tenerlo en cuenta. Esto nos permite tener más de una dirección IP.


## EC2 Templates

Son plantillas que podemos crear para crear rápidamente instancias en el futuro. tendremos que colocar un nombre base, una AMI, un tipo de instancia y todo lo que se nos pide como si estuviéramos creando una instancia desde 0, pero ya luego teniendo esta base podremos crear las instancias basadas en esta plantilla para ahorrarnos hacer la configuración nuevamente.

No es necesario diligenciar toda la información, por ejemplo podemos dejar el Key Pair vacío y luego cuando creemos una instancia con nuestra plantilla nos pedirá la información aún faltante.

### Versiones
AWS nos guarda las versiones que generamos de nuestra plantilla, esto nos permite poner una versión como default para usarla y si requerimos hacer ajustes setear una versión distinta como default.


## Instancias SPOT

Básicamente son máquinas que entre comillas le sobran a Amazon y las ofrecen a un precio mucho más económico. En algunas zonas nos ahorra hasta un 70% del valor de una instancia normal. Es importante tener en cuenta que si el algún momento Amazon requiere de este recurso SPOT para utilizarlo como una instancia normal nos darán de baja la máquina.


## Saving Plans

### Compute
Son de procesamiento, y nos dan la mayor flexibilidad para reducir el coste ya que se van a aplicar de forma automática.

### EC2 Instance
Los planes de ahorro de las instancias EC2 proveen precios más bajos, ofreciendo ahorris de hasta el 72%.

### SageMaker
Son una serie de productos que se usan para Machine Learning y nos permite tener hasta un 64% de ahorro en estos productos.


## Instancias reservadas

Nos sirven si necesitamos una máquina durante X período de tiempo y una cantidad de tiempo al día Amazon nos hará también una especie de ahorro comparado a si fuera una On Demand. Es un precio fijo por mes independientemente de si la instancia es apagada o encendida.


## Dedicated Hosts

Es una máquina física que reservo para mí y sobre ella creo instancias EC2. Al alquilarla podremos seleccionar las características mediante la instancia que deseemos, sin embargo es importante tener en cuenta que hay planes On Demand y anuales, y al reservar un Host dedicado por 1 año tendremos descuentos de aproximadamente el 40%.

Una cuenta nueva no puede crear Hosts dedicados por defecto, y hay que hacer la solicitud a Amazon para subir el límite de Hosts dedicados.


## Scheduled instances

Son instancias reservadas con planificación, es decir que planeamos usarlas en un período de tiempo o por cierta cantidad de tiempo. Sin embargo, esta opción ya no está disponible, si requerimos una instancia reservada podemos hacer uso de las Capacity Reservations.


## Capacity Reservations

Le indicamos a Amazon el período de tiempo y las características de la máquina que deseamos reservar. El período de tiempo puede ser incluso por horas pero hay que tener en cuenta que si reservamos un período de tiempo y una vez iniciado el período de tiempo no tenemos la instancia creada o no la estamos usando Amazon igual generará el cobro.


# AWS CLI

Nos permite conectarnos a los servicios de Amazon mediante líneas de comandos. Para conectarnos tendremos que buscar la opción Security Credencials en nuestra cuenta y crear un Access Key. Es importante tener claro que debemos copiar la clave para poder conectarnos porque luego no podremos verla. Para configurar el CLI con las credenciales podremos usar el siguiente comando:

```bash
aws configure

<Access-Key>

<Access-Secret-Key>

<Codigo-region>

<Output-format(none)>
```

Y aquí unos comandos que podemos usar con CLI:

| Descripción | Comando |
|--|--|
| Listar instancias EC2 | `aws ec2 describe-instances` |
| Listar VPCs (JSON) | `aws ec2 describe-vpcs` |
| Listar VPCs con formato YAML | `aws ec2 describe-vpcs --output yaml` |
| Listar VPCs con formato Text | `aws ec2 describe-vpcs --output text` |
| Listar VPCs con formato Table | `aws ec2 describe-vpcs --output table` |
| Listar subredes | `aws ec2 describe-subnets` |
| Listar subred filtrando por id | `aws ec2 describe-subnets --subnet-ids <subnet-id>` |
| Listar subred con varios filtros | `aws ec2 describe-subnets --filters "Name=<nombre-filtro>, Values=<valor-filtro>" "Name=<nombre-filtro2>, Values=<valor-filtro2>"` |
| Listar instancias EC2 | `aws ec2 describe-instances` |
| Listar subredes y guardar el resultado en un archivo | `aws ec2 describe-subnets > <nombre-archivo>.<extension-archivo>` |
| Pintar todos los campos que estén dentro de Subnets | `aws ec2 describe-subnets --query 'Subnets[*]'` |
| Pintar la subred 1 | `aws ec2 describe-subnets --query 'Subnets[0]'` |
| Pintar ciertas posiciones de subredes | `aws ec2 describe-subnets --query 'Subnets[1:3]'` |
| Pintar de todas las subredes la propiedad AvailabilityZone | `aws ec2 describe-subnets --query 'Subnets[*].AvailabilityZone'` |
| Pintar las VPCs y renombrar propiedades | `aws ec2 describe-vpcs --query 'Vpcs[].[VpcId,{Estado:State},{"VPC por defecto": IsDefault}]'` |
| Crear instancia EC2 | `aws ec2 run-instances --image-id <ami-id> --count <cantidad-instancias> --instance-type <tipo-instancia> --key-name <nombre-key-pair> --security-groups <nombre-grupo-seguridad>` |
| Listar instancias EC2 (filtros opcionales) | `aws ec2 describe-instances --filters "Name:instance-type, Values=t3.micro"` |
| Detener una instancia | `aws ec2 stop-instances --instance-ids <id-instancia>` |
| Encender una instancia | `aws ec2 start-instances --instance-ids <id-instancia>` |
| Terminar una instancia | `aws ec2 terminate-instances --instance-ids <id-instancia>` |


## Cloud Shell

Es una terminal en la nube que nos brinda Amazon, con esto nos ahorramos la configuración de Amazon CLI, tiene pre instalado el CLI, Python, NodeJS entre otros. Tiene 1GB de almacenamiento por región y guarda los archivos para futuros usos necesarios.