****************************************************************************************************************************************************
Docker 

preparando el repositorio, ya que ubuntu 16 no tiene soporte por docker


curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
sudo apt-get update



* Instalar Docker en la máquina y que quede corriendo después de reboot.	
	una vez preparado el entorno de ubuntu y respotiroios se procede a instalar. 
		sudo apt-get install docker-ce
			sudo apt-get install docker-ce docker-ce-cli containerd.io 
			
	iniciar docker despues del reinicio 
		systemctl enable docker.service
		docker run --restart=always
	
* Ejecutar un servidor web (Nginx o Apache) usando la imagen de Docker para Nginx. Exponer el servidor web corriendo en Docker en el puerto 8888.

	buscar imagenes en docker 
		docker search nginx

	salvar image
		docker pull nginx

	revisar images descargadas 
		docker images

	ejecutar contenedor 
		docker run -it nginx

	ejecutar en pueto especifico externo
		docker run -p 8888:80 nginx

	ejecutar en pueto especifico externo (-d para que no bloquee la pantallas)
	docker run -p 8888:80 -d nginx  

otros comandos 
docker rm id (eliminar )

* Poner como página web por defecto del servidor web corriendo usando Docker la misma usada en la tarea 3 de las actividades de administración de 
  sistemas operativos Linux.

	para levar a cabo la insercion de contenido estatico, debemos hacer uso de las rutas origen y destino. para ello usamos la siguiente sintaxis.

	recuerda detener la imagen que está corriendo por el puerto 8888
		docker run -d -p 8888:80 --name instance1indexapache2 -v /var/www/html:/usr/share/nginx/html:ro nginx 


* Ejecutar dos instancias del misma imagen de Docker usada en la tarea 2.

	iguales a la de la tarea 2
		docker run -p 9090:80 --name instance2 -d nginx
		docker run -p 9191:80 --name instance3 -d nginx

	iguales a la de la tarea 3
		docker run -d -p 9595:80 --name indexapache2-2 -v /var/www/html:/usr/share/nginx/html:ro nginx 
		docker run -d -p 9696:80 --name indexapache2-3 -v /var/www/html:/usr/share/nginx/html:ro nginx 

* Hacer pull del código versionado en el repositorio de la tarea de Devops, crear un Dockerfile y crear una imagen propia, luego levantar un cuarto contenedor a 
  partir de esta nueva imagen propia. Versionar el Dockerfile y un readme con los pasos a seguir para este propósito.

	hacer el pull 
		git push --tags

	Creacion del Dockerfile
	Nos ubicamos en la ruta del proyecto y creamos el archivo Dockerfile 

	editamos el archivo Dockerfile para ingresar los parametros 

		FROM nginx
		WORKDIR /usr/share/nginx/html
		COPY . .

	Contruimos la imagen 
		docker build -t miprimerimages .

	inciamos la imagen
		docker run -p 9999:80 --name instance4 -d miprimerimages
		
	versionar el proyecto con el docker file y crear un archico readme que contanga el paso a paso.
		git tag -a v2.0.0 -m "Version 2.0.0"


* Crear una cuenta en hub.docker.com y crear una imagen pública a partir de la imagen creada en el punto 5.
	
	crear imagen publica, para esto volvemos a crear una imagen relacionando el id de usuario 

		docker build -t diegoanaya9010/miprimeraimagepublica .

		docker login (ingresar credenciales de usuario)
		usuario: diegoanaya9010
		password: Cecar12345..
	
	hacer push para publicar.
		docker push diegoanaya9010/miprimerimagepublica****************************************************************************************************************************************************
Docker 

preparando el repositorio, ya que ubuntu 16 no tiene soporte por docker


curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
sudo apt-get update



* Instalar Docker en la máquina y que quede corriendo después de reboot.	
	una vez preparado el entorno de ubuntu y respotiroios se procede a instalar. 
		sudo apt-get install docker-ce
			sudo apt-get install docker-ce docker-ce-cli containerd.io 
			
	iniciar docker despues del reinicio 
		systemctl enable docker.service
		docker run --restart=always
	
* Ejecutar un servidor web (Nginx o Apache) usando la imagen de Docker para Nginx. Exponer el servidor web corriendo en Docker en el puerto 8888.

	buscar imagenes en docker 
		docker search nginx

	salvar image
		docker pull nginx

	revisar images descargadas 
		docker images

	ejecutar contenedor 
		docker run -it nginx

	ejecutar en pueto especifico externo
		docker run -p 8888:80 nginx

	ejecutar en pueto especifico externo (-d para que no bloquee la pantallas)
	docker run -p 8888:80 -d nginx  

otros comandos 
docker rm id (eliminar )

* Poner como página web por defecto del servidor web corriendo usando Docker la misma usada en la tarea 3 de las actividades de administración de 
  sistemas operativos Linux.

	para levar a cabo la insercion de contenido estatico, debemos hacer uso de las rutas origen y destino. para ello usamos la siguiente sintaxis.

	recuerda detener la imagen que está corriendo por el puerto 8888
		docker run -d -p 8888:80 --name instance1indexapache2 -v /var/www/html:/usr/share/nginx/html:ro nginx 


* Ejecutar dos instancias del misma imagen de Docker usada en la tarea 2.

	iguales a la de la tarea 2
		docker run -p 9090:80 --name instance2 -d nginx
		docker run -p 9191:80 --name instance3 -d nginx

	iguales a la de la tarea 3
		docker run -d -p 9595:80 --name indexapache2-2 -v /var/www/html:/usr/share/nginx/html:ro nginx 
		docker run -d -p 9696:80 --name indexapache2-3 -v /var/www/html:/usr/share/nginx/html:ro nginx 

* Hacer pull del código versionado en el repositorio de la tarea de Devops, crear un Dockerfile y crear una imagen propia, luego levantar un cuarto contenedor a 
  partir de esta nueva imagen propia. Versionar el Dockerfile y un readme con los pasos a seguir para este propósito.

	hacer el pull 
		git push --tags

	Creacion del Dockerfile
	Nos ubicamos en la ruta del proyecto y creamos el archivo Dockerfile 

	editamos el archivo Dockerfile para ingresar los parametros 

		FROM nginx
		WORKDIR /usr/share/nginx/html
		COPY . .

	Contruimos la imagen 
		docker build -t miprimerimages .

	inciamos la imagen
		docker run -p 9999:80 --name instance4 -d miprimerimages
		
	versionar el proyecto con el docker file y crear un archico readme que contanga el paso a paso.
		git tag -a v2.0.0 -m "Version 2.0.0"


* Crear una cuenta en hub.docker.com y crear una imagen pública a partir de la imagen creada en el punto 5.
	
	crear imagen publica, para esto volvemos a crear una imagen relacionando el id de usuario 

		docker build -t diegoanaya9010/miprimeraimagepublica .

		docker login (ingresar credenciales de usuario)
		usuario: diegoanaya9010
		password: Cecar12345..
	
	hacer push para publicar.
		docker push diegoanaya9010/miprimerimagepublica
