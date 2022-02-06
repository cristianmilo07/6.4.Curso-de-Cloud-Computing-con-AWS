# 6.4.Curso-de-Cloud-Computing-con-AWS

_____________________________________________________________________
![](https://static.platzi.com/media/courses/Opengraph0.png)
_____________________________________________________________________
### Introducción al documento
_____________________________________________________________________
El contenido de este documento esta basado en el curso del mismo nombre dictado por Mauro Parra Miranda en Platzi.

**Table of Contents**

[TOCM]

[TOC]

# 1. Agenda

Esto es lo que verás en este curso de Cloud Computing con AWS:

    -Introducción: AWS cómputo se refiere a cualquier producto de AWS que nos permite servir algún archivo, procesar o calcular algo.
    -EC2: Son máquinas virtuales que nos renta Amazon por segundo. Hay Linux o Windows. Podemos elegir número de CPUs, RAM, discos duros, tipo de conectividad, entre otras opciones.
    -Lightsail: Es un producto particular porque es un VPS sobre Amazon similar a Dreamhost o Digital Ocean estando en la red de Amazon conservando los bajos costos de los VPS comerciales.
    -ECR/ECS/EKS: ECR es donde registramos contenedores, ECS es el producto de Amazon para Docker y EKS es el producto de Amazon para Kubernetes.
    -Lambda: Es la infraestructura de Amazon para poder correr diferentes funciones.
    -Elastic Beanstalk: Permite correr diversos software o cargas productivas, pudiendo autoescalar hacia arriba o hacia abajo de manera automática.
Nuestro proyecto será un software que nos permitirá mostrar diferentes citas en pantalla. Cada que recarguemos pantalla veremos una nueva cita.

Lecturas recomendadas

Amazon Lightsail

https://aws.amazon.com/es/lightsail/


Amazon ECR | Amazon Web Services

https://aws.amazon.com/es/ecr/


AWS | Gestión de contenedores (ECS) compatible con los de Docker

https://aws.amazon.com/es/ecs/


Amazon EKS – Servicio de Kubernetes administrado

https://aws.amazon.com/es/eks/


AWS | Lambda - Gestión de recursos informáticos

https://aws.amazon.com/es/lambda/


AWS | Elastic beanstalk para aplicaciones web desarrolladas con Java

https://aws.amazon.com/es/elasticbeanstalk/

# 2. Introducción a EC2

¿Qué son los EC2?

    -Son máquinas virtuales, llamadas instancias en Amazon que te van a permitir correr diferentes software en diferentes sistemas operativos con diferentes configuraciones.
    -Amazon tiene ya unas imágenes preconfiguradas llamadas AMIs .
    -Podremos seleccionar diferentes tamaños de CPU´s y su cantidad, cantidad de RAM, espacio en disco, diferente conectividad, entre otros. El costo depende de las capacidades que especifiquemos.
    
Arquitectura de EC2:

Podemos crear diferentes imágenes, por ejemplo una con Ubuntu, configurando o instalando diferentes software, finalmente haciendo una imágen con ello. Las imágenes van hacia una instancia de EC2, seleccionando capacidad que necesitamos en la máquina virtual.
Asociado a esto, están los temas de redes como los grupos de seguridad, los balanceadores de cargas hacia los cuales llega el tráfico de la web externo como interno.
De storage tenemos uno que es efímero que sólo existe mientras la máquina esté prendida, y el otro es un bloque elástico que permanece a pesar de borrar la máquina y de él podemos hacer copias en caso de que vaya evolucionando otro proyecto.

Lecturas recomendadas

Amazon EC2

https://aws.amazon.com/ec2/

# 3. Tipos de instancias al momento de crear un EC2

Cosas a tener en cuenta al momento de crear tu EC2:

    -Hay ocasiones en las cuales puedes entrar y no ver tus instancias creadas. Esto puede pasar porque no seleccionaste la región adecuada o la que tenías al momento de crearlas.
    -Al momento de crear las imágenes se recomienda usar la de Amazon ya que viene actualizada con los últimos drivers.
    -La sección T2/T3 Unlimited en la configuración de la instancia nos sirve si necesitamos mucha CPU o red, al habilitarla, Amazon nos lo dará sin límite. El problema es que tiende a ser más costoso.
    -Es muy útil al momento de poner tag que se use uno aunque sea un nombre para recordar para qué sirve la máquina.
    -Para conectarnos a la máquina debemos crear una llave. Es importante guardarla en un lugar seguro haciéndole una copia de seguridad ya que si no se tiene la llave, no es posible conectarse por medio de SSH.
 
Lecturas recomendadas

AWS | Elastic compute cloud (EC2) de capacidad modificable en la nube

https://aws.amazon.com/es/ec2/

# 4. Tipos de instancias al momento de crear un EC2

Cosas a tener en cuenta al momento de instalar tu proyecto:

    -Si tienes Linux o MAC, ya cuentas con la terminal para poderte conectar por medio de SSH; si tienes Windows, es necesario usar un software como MobaXterm que es gratis para uso personal.
    -El comando que debes usar es “sudo apt install apache2 git libapache2-mod-php -y”
    -Si acabas de iniciar tu máquina, es posible que no encuentre los paquetes, ya que los DNS no son los correctos. Con “apt-get update” lo solucionas.
    -La dirección del repositorio usado en clase es: https://github.com/mauropm/quotes-generator
    
   Lecturas recomendadas

MobaXterm free Xserver and tabbed SSH client for Windows

https://mobaxterm.mobatek.net/


GitHub - mauropm/quotes-generator: A simple PHP application to generate a random quote as HTML.

https://github.com/mauropm/quotes-generator

Apache2 Ubuntu Default Page: It works Momo!

https://annex.exploratorium.edu/

# 5. Imágenes de instancias

Crear una imagen es muy útil porque cuando quieras crear una instancia nueva, podrás seleccionar la imagen, ahorrándote los pasos de instalación.

Cosas a tener en cuenta al momento de crear imágenes de instancias:

Creando una imagen te encontrarás con la opción de No reboot, si no se selecciona, Amazon va a apagar nuestra instancia para poder hacer la copia; si se selecciona, la instancia no se apagará, corriendo el riesgo de que pueda salir una copia corrupta. Se recomienda reiniciar la instancia.
Si estás en producción y la instancia que tienes se quedó corta en capacidades, seleccionarías que no se reinicie, para hacer tu copia y crear una nueva instancia con esta copia.
Si seleccionaste que sí se reiniciara la instancia, tu IP pública cambiará y no podrás conectarte a tu máquina con la anterior IP.
Lecturas recomendadas

AWS | Elastic compute cloud (EC2) de capacidad modificable en la nube

https://aws.amazon.com/es/ec2/

# 6. Snapshots y sus operaciones

Cuando creas una imagen, vas a poder reproducir esa instancia con el mismo sistema operativo, software y capacidades, estás haciendo una copia del sistema al completo. Si quisieras hacer una copia de una sola de sus características, por ejemplo el software, ahí es donde usarías un **Snapshot” del volumen que es el disco duro. Esto se hace en situaciones especiales para añadir un volumen a una máquina virtual que ya esté corriendo.

Se recomienda crear una imagen nueva o AMI cada vez que hagas un cambio mayor en la instancia, versionando a través de imágenes para hacer rollback en caso de que el update falle o la configuración sea errónea.

Lecturas recomendadas

Precios de Amazon EBS: Amazon Web Services

https://aws.amazon.com/es/ebs/pricing/

# 7. Configuración de Red

Cuando reinicies o apagues tu instancia, la IP pública asignada muy probablemente cambiará. En muchos casos esto no es lo deseado y vamos a querer tener una IP que no cambie.
Amazon tiene la solución a este problema ya que nos ofrece el servicio para comprar una IP estática y asignarla a cualquiera de nuestras instancias.

Lecturas recomendadas

Direcciones IP elÃ¡sticas - Amazon Elastic Compute Cloud

https://docs.aws.amazon.com/es_es/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html

# 8. Balanceadores de carga

Un Load balancer o balanceador de carga lo puedes conectar a una o más instancias y lo que hace es balancear las solicitudes que le llegan pudiendo generar respuestas de una de las instancias que tiene a disposición dependiendo de su disponibilidad. Puedes balancear peticiones HTTP, HTTPS o TCP con los servicios de AWS.

Cuando creamos un load balancer, podemos ver en sus configuraciones básicas un DNS el cual podemos usar en Route 53 como CNAME para ponerme un nombre de dominio o subdominio.

# 9. Balanceadores de carga con https

Normalmente, cuando usas un balanceador de cargas, quieres prover dos distintos servicios:

Https - puerto 443
Http - puerto 80
Para dar servicio en el puerto 443, sigue las instrucciones que viene en la clase de load balancer, y la hora de anexar el puerto 443, te pedirá un certificado. Vamos a crear un nuevo certificado antes, para que solo selecciones el correcto.

Creando un certificado nuevo.

Requisitos
Poseer algún dominio o subdominio, que asignaras al certificado inicialmente, y después al balanceador de carga.
Tener acceso a recibir el correo por parte del administrador del dominio, para poder anexar el certificado del lado de AWS. Si no lo tienes, necesitas acceso al DNS de ese dominio, para anexar un “entry” en el DNS, relacionado con la autenticación que requiere AWS para que muestres que eres el dueño del dominio (o que tienes control para él, si es que eres el administrador para alguna compañía).
Actividades
Ve al Certificate Manager. Visita la consola de amazon http://console.aws.amazon.com/ y de ahi ponle en el search “Certificate Manager”.
Dale click en “Provision certificates”-> Get Started.
Selecciona “Request a public certificate”
Click en el botón “Request a certificate”.
En la sección “Add a domain name”, pon un dominio wildcard al menos. Por ejemplo, en la clase de Networking & CDN en AWS compramos un dominio pruebaplatzi.de. En mi caso, pondría *.pruebaplatzi.de”. Tu tienes que poner *.tudominio.com, pensando que tu dominio se llama tudominio.com. Puedes anexar mas, como por ejemplo www.tudominio.com, test.tudominio.com, etc. Puedes anexar tantos como necesites, de tal manera que ese certificado cubra a todos tus servidores de prueba o desarrollo. Te recomiendo que si estas haciendo un producto, tu dominio producto.tudominio.com tenga su propio certificado solito, para que la gente no se confunda cuando lo revisa en el candado verde en tu navegador.
Dale ‘Next’
Selecciona que tipo de validación puedes hacer: si te llegan los mails de quien registro el dominio, selecciona mail. Si no es así, pero tienes acceso al DNS, selecciona DNS.
En el caso de que manejes el dominio y el DNS del dominio en Route53, es mas sencillo ponerle DNS, y puedes ver la clase de Route53 para ver como anexas subdominios con el valor que te solicita AWS.
Click en “Confirm request” y listo.
En el caso que selecciones mail, revisa tu mail y dale click al url que te incluyen.
Una vez que termines la validación, ya te aparecerá listado en los certificados.
Creando el balanceador de carga
Ahora que ya tienes el certificado, puedes ir directamente a la consola de AWS, y crear o editar el balanceador de cargas, anexa el puerto 443/https, y cuando te pida el certificado, utiliza el que recién creaste.

Si tienes alguna duda o quisieras una guía paso a paso, ve al Curso de Networking y Content Delivery en AWS.
