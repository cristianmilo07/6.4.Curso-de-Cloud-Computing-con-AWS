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

# EC2

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

# 10. Marketplace de AMIs

La URL para acceder al marketplace es: https://aws.amazon.com/marketplace

En el marketplace podrás encontrar una gran cantidad de imágenes generadas para crear instancias. Algunas de ellas serán de pago y otras serán gratuitas sólo cobrando por la infraestructura de Amazon.
Esto puede resultar muy útil porque nos ahorra el tiempo de creación de instancias y sus copias, dándonos configuraciones perfectas para nuestras necesidades, que alguien ya resolvió con anterioridad.

Lecturas recomendadas

AWS Marketplace: Homepage

https://aws.amazon.com/marketplace/

# 11. Reto EC2

El reto de esta clase consiste en crear una instancia de EC2 y configurarle nuestro proyecto de frases motivacionales. Para probar que lo hiciste bien, copia la IP pública de la instancia en tu navegador y deberías poder ver una de las frases.

# Lightsail

# 12. Qué es Lightsail

    -Es un VPS (Virtual Private Server) como lo es Digital Ocean o el mismo EC2 de Amazon. Tiene una IP pública y un dominio gratis. Su mayor diferencia con EC2 es el precio más bajo.
    -Se inicia en segundos
    -Viene con varios templates pre-configurados como LAMP, Wordpress, Magento, etc.
    -Su principal ventaja es su costo, bajo y predecible.
    -Puedes aumentar o disminuir su capacidad cuando lo quieras, al alcance de un click.
    -Puedes usar bases de datos.
    -Puedes hacer respaldos como los Snapshots.
    -Te ofrece la opción de restauración.
    -Puede ser multi-región o multi-zonas (que en la misma zona geográfica tendrás diferentes data centers).

Lecturas recomendadas

Amazon Lightsail

https://aws.amazon.com/es/lightsail/

# 13. Marketplace LS

El marketplace de Lightsail te permite elegir entre Linux y Windows, siendo esta opción la manera más económica de tener Windows de todos los servicios de Amazon.
Puedes instalar el SO más aplicaciones como Wordpress o Node.js; también puedes decidir por inicializar la imagen sólo con el sistema operativo, teniendo muchas opciones en la familia de Linux.
Instalar todos los parches de seguridad o actualizaciones es tu responsabilidad al igual que en EC2.

# 14. Comparativa
Esto es lo que te ofrece Lightsail:

    -El costo de los CPUs depende del número que elijas.
    -Tienes almacenamiento SSD.
    -Te ofrece Networking y transferencia de datos.
    -Incluye manejo de DNS.
    -Tienes una IP estática asignada a ti.
    -Tienes acceso a otros servicios de AWS
    -En una comparativa de costos, el plan más económico de Lightsail ofrece por $3.50 1 TB de transferencia mientras que la misma capacidad en EC2 puede salir por más de $90.
    
# 15. Creando un VPS
  
  Lecturas recomendadas

Amazon Lightsail

https://aws.amazon.com/es/lightsail/


# 16. Instalando Frases Citables

Instalar un proyecto en Lightsail es muy parecido al procedimiento que se realiza en EC2.

Cosas a tener en cuenta al momento de instalar tu proyecto con Lightsail:

    -Si estás en Windows, deberás usar un software como MobaXterm para tener una terminal que se conecte por SSH.
    -Recuerda hacerte administrador con el comando “sudo su”
    -Recuerda hacer update con el comando “apt-get update” porque es una instancia nueva y no tiene en memoria caché las direcciones desde dónde debe tomar el software. Si el proyecto se instala sin hacer esto, fallará.
    -El comando para instalar el software es “sudo apt install apache2 git libapache2-mod-php -y”.
    -La URL del proyecto es “https://github.com/mauropm/quotes-generator”.
    -Configurar todo lo que esté en la red de Amazon es súper veloz, dándole más ventajas a la instalación de proyectos en Lightsail.
    
# 17. Creando una BD

Las bases de datos en Lightsail también tienen un costo fijo con la disponibilidad que ofrece Amazon.

Cosas a tener en cuenta al momento de crear tu base de datos:

    -Lightsail nos ofrece varias versiones de MySQL; si es un proyecto nuevo es recomendado utilizar la más actual. Si es una migración deberemos elegir la versión más     -cercana a nuestra base de datos existente.
    -Lightsail nos propone un password seguro, es recomendable usarlo.
Puedes configurar tu base de datos de dos maneras:
    -Estándar: Un servidor con una conexión desde afuera.
    -HA: Alta disponibilidad, donde tienes dos servidores o más con un load balancer.
    
Lecturas recomendadas
Databases in Amazon Lightsail | Lightsail Documentation

https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-databases

# 18. Reto Lightsali

# ECR/ECS/EKS

# 19. Introducción a ECR/ECS/EKS

ECR es el servicio que te permite registrar los contenedores a través de Dockerfiles en Amazon.
Aunque existe ECR, no aparece como producto. Es necesario entrar a ECS y ya desde ahí encontramos las opciones para entrar al ECR.
Importante antes de registrar contenedores: Tener instalado el AWS CLI y Docker, adicionalmente es importante tener instalado Git.

Lecturas recomendadas

ubuntu - Got permission denied while trying to connect to the Docker daemon socket while executing docker stop - Stack Overflow

https://stackoverflow.com/questions/46759268/got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket-while

How To Install and Use Docker on Ubuntu 18.04 | DigitalOcean

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04


# 20. Introducción a ECS

ECS es toda la infraestructura que te permite correr contenedores de Docker directo en AWS.

Su ventaja es que no debes poner una máquina con Docker donde encima corran los contenedores. Amazon da la infraestructura pre-hecha y nosotros solo elegimos capacidades.
Únicamente se paga por la capacidad solicitada (cCPU, memoria, transferencia de datos).
Puedes escalar tu instancia basada en contenedor de manera manual.
Usos clásicos de ECS:

Microservicios.
Migración de aplicaciones Legacy al Cloud.
Lecturas recomendadas

Amazon ECR | Amazon Web Services

https://aws.amazon.com/es/ecr/


Â¿QuÃ© es Amazon Elastic Container Service? - Amazon Elastic Container Service

https://docs.aws.amazon.com/es_es/AmazonECS/latest/developerguide/Welcome.html

# 21. Corriendo un contenedor

Cosas a tener en cuenta al momento de correr un contenedor:

Networking only está basado en un producto llamado AWS Fargate que nos da la infraestructura de Docker sin tener que preocuparnos por las máquinas base y es el que usaremos en este proyecto.
Es necesario crear una tarea relacionada con la imagen de Docker que creamos anteriormente.

# 22. Instalando ambiente docker en EC2

**Introducción**

Para poder ejecutar comandos como “docker build” necesitamos configurar nuestro ambiente de docker en una instancia EC2 pequeña.

Configuración de Docker

	-Crea una instancia de EC2 con Ubuntu.
	-Selecciona una instancia de tamaño mínimo (nano, por ejemplo, si tienes una cuenta AWS de mas de un año. - En caso contrario, la t2.micro es la gratuita en tu primer año de servicio (recuerda, únicamente por un año).
	-Una vez que este en estado “Running” conectate a ella.
	-Teclea:
		a) sudo su
		b) apt-get update
	-Una vez que termine, corre, como usuario root:
		a) snap install docker -y
		b) apt-get install git -y
	-Después de esto, ya podrás hacer:
		a) git clone https://github.com/mauropm/quotes-generator.git
		b) cd quotes-generator
		c) dock build

Con esto, ya podrás hacer imágenes de contenedores y siguiendo las instrucciones de la clase, podrás enviarlo a ECR (El registro de contenedores de AWS).

# 23. Introducción a EKS

	-EKS es una implementación de Kubernetes en Amazon que no requiere que coordines nodos maestros y esclavos.
	-Te permite crear un ambiente de workers de k8s en AWS.
	-Podrás correr contenedores con el dashboard de Kubernetes o cualquier orquestador que quieras usar.
	
EKS va desde poner el nodo maestro de Kubernetes, poner los workers y ya podrás conectarte a la API para correr tareas.

Lecturas recomendadas

Amazon EKS – Servicio de Kubernetes administrado

https://aws.amazon.com/es/eks/


Production-Grade Container Orchestration - Kubernetes

https://kubernetes.io/


# 24. Configuración kops / k8s en AWS


**Introducción**
kops es una herramienta que nos permite crear y administrar kubernetes (también conocido como k8s) en AWS (y otros clouds). En esta lectura pondremos las instrucciones para configurarlo localmente y crear un cluster de k8s en AWS.

Instrucciones

Como root, en alguna instancia EC2 pequeña o en su máquina local (estas instrucciones son para linux).

	-sudo apt update
	-sudo apt install -y awscli
	-sudo snap install kubectl --classic
	-curl -LO https://github.com/kubernetes/kops/releases/download/1.7.0/kops-linux-amd64
	-chmod +x kops-linux-amd64
	-mv ./kops-linux-amd64 /usr/local/bin/kops
	-Tienen que crear un usuario llamado kops en IAM.
	-Entren en IAM, hagan un nuevo usuario.
	-Configuren esto como acceso programatico.
	-Apunten el Access Key ID y el password.
	-Asígnenle el rol de AdministratorAccess (un rol preconfigurado en AWS IAM).
	-Salvar.
	-Regresen de la consola de AWS a tu consola / terminal, y continúen con lo siguiente:
	-aws config
	-aws iam create-group --group-name kops
	-aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonEC2FullAccess --group-name kops
	-aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonRoute53FullAccess --group-name kops
	-aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess --group-name kops
	-aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/IAMFullAccess --group-name kops
	-aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonVPCFullAccess --group-name kops
	-aws iam add-user-to-group --user-name kops --group-name kops
	-aws s3api create-bucket --bucket s3kopstudominiocom --region us-west-2
	-Antes de ejecutar el próximo comando, anexen lo siguiente a su archivo ~/.bashrc (al final):
	export AWS_ACCESS_KEY_ID=tuaccesskey
	export AWS_SECRET_ACCESS_KEY=tusecret
	export KOPS_STATE_STORE=s3://s3kopstudominiocom
	export KOPS_CLUSTER_NAME=kops-cluster-tudominio
	-Sálvenlo. Cierren sesión con “exit” y vuelvan a entrar. Ahora si, ejecuta:
	-kops create cluster --name=kops-cluster-tudominio --cloud=aws --zones=us-west-2a --state=s3kopstudominiocom
	-Esta operación puede tardar 20 minutos.
	-Cuando terminen, denle:
	kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
	-Con eso, se instalará el dashboard de k8s que vieron en el ejemplo.
	-Loguearse con user admin, y el password se obtiene con:
	kops get secrets kube --type secret -oplaintext
	-Cuando se conecten, seleccionen anunciarse por token, y el token lo obtienen ejecutando lo siguiente:
	kops get secrets admin --type secret -oplaintext
	-Con eso, ya podrán dar click en “Create” y poder poner su imagen del contenedor en ECR.
	-Cuando termine de hacer el deployment, encontrarán la url en la sección en el menú llamada “Services”.

Nota:

Si estas instrucciones las llevan a cabo en su máquina local, si tecleas kubectl proxy, tendrán el dashboard en la dirección: https://localhost:8001 - Noten que usa https siempre, y que el certificado no es confiable, por lo que tendrán que autorizar a su browser para poder abrirlo. La url completa para el dashboard, utilizando kubectl proxy, es:

http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#!/login

Conclusión:

Esta actividad no es fácil. Kubernetes es un proyecto en construcción, por lo que está en constante cambio todo el tiempo, y evoluciona tan rápido que estas instrucciones podrían volverse obsoletas pronto, por lo que les pido que no desesperen, y que si hay alguna situación que no esté funcionando, pregunten en la sección de comentarios.
