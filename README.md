# Actividad 1. Generar Docker

## 1. Instala Docker en tu máquina

Para Ubuntu:

Primero, actualiza tus paquetes:

```bash
sudo apt update
```

Siguiente, instala Docker con apt-get:

```bash
sudo apt install docker.io
```

Finalmente, verifica que Docker se ha instalado correctamente:

```bash
sudo docker run hello-world
```

- Para MacOS puedes seguir [este enlace](https://docs.docker.com/docker-for-mac/install/)
- Para Windows puedes serguir [este enlace](https://docs.docker.com/docker-for-windows/install/)

## 2. Crea tu proyecto en python

Para crear tu primera aplicación Docker, te invito a crear una carpeta en tu computadora. Debe contener los siguientes dos archivos:

- Un archivo *main.py* (un archivo python que tendrá el código a ejecutar).
- Un archivo *Dockerfile* (un archivo Docker que tendrá las instrucciones necesarias para crear el entorno).

Monta esta arquitectura de carpeta:

```bash
.
├── Dockerfile
└── main.py

0 directories, 2 files
```

## 3. Edita el archivo Python

```python
#!/usr/bin/env python3 

print("¡Soy nombre y apellidos de 2 curso de DAM!")
```

Edita el archivo Docker

Un poco de teoría: lo primero que hay que hacer cuando quieres crear tu Dockerfile es preguntarte qué quieres hacer. Nuestro objetivo aquí es lanzar código Python.

Para ello, nuestro Docker debe contener todas las dependencias necesarias para lanzar Python. Un Linux (Ubuntu) con Python instalado en él debería ser suficiente.

El primer paso para crear un archivo Docker es acceder al sitio web [DockerHub](https://hub.docker.com/) to an external site.. Este sitio contiene muchas imágenes prediseñadas para ahorrarte tiempo (por ejemplo: todas las imágenes para Linux o lenguajes de código).

En nuestro caso, escribiremos ‘Python’ en la barra de búsqueda. El primer resultado es la imagen oficial creada para ejecutar Python. Perfecto, ¡lo usaremos!

```dockerfile
# Un archivo docker (dockerfile) comienza siempre importando la imagen base.
# Utilizamos la palabra clave 'FROM' para hacerlo.
# En nuestro ejemplo, queremos importar la imagen de python.
# Así que escribimos 'python' para el nombre de la imagen y 'lastest' para la versión.
FROM python:latest

# Para lanzar nuestro código python, debemos importarlo a nuestra imagen.
# Utilizamos la palabra clave 'COPY' para hacerlo.
# El primer parámetro 'main.py' es el nombre del archivo en el host.
# El segundo parámetro '/' es la ruta donde poner le archivo en la imagen.
# Aquí ponemos el archivo en la carpeta raíz de la imagen.
COPY main.py /

# Necesitamos definir el comando a lanzar cuando vayamos a ejecutar la imagen.
# Utilizamos la palabra clave 'CMD' para hacerlo.
# El siguiente comando ejecutará "python ./main.py"
CMD [ "python", "./main.py" ]
```

## 4. Crea la imagen Docker

Una vez que tu código esté listo y el Dockerfile está escrito, todo lo que tienes que hacer es crear tu imagen para contener tu aplicación.

```bash
docker build -t python-tunombreyapellidos .
```

La opción *-t* te permite definir el nombre de tu imagen. En nuestro caso hemos elegido ’tunombreyapellidos’ pero le puedes poner lo que quieras.

## 5. Corre la imagen Docker

Una vez la imagen esté creada, tu código está listo para lanzar.

```bash
docker run tunombreyapellidos
```

## 6. Presenta el pantallazo de la aplicación con tus nombres y apellidos
