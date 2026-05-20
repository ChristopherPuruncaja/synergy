<p align="center"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTsWESkUMmFtbO3AtqDZNfSEn4kSaH6z4eEzg&s"></p>


<p align="center">
  <br>
  
  <br>
  <img src="[https://i.imgur.com/1wJVDV5.png](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTsWESkUMmFtbO3AtqDZNfSEn4kSaH6z4eEzg&s)">
</p>


El concepto detrás de SYNERGY es simple: al igual que alojamos páginas de phishing para obtener credenciales, ¿por qué no alojar una página falsa que solicite tu ubicación, como hacen muchos sitios web populares basados ​​en la ubicación?, La herrramienta muestra una prueba de como se realiza el robo de informacion, aloja un sitio web falso que solicita permiso de ubicación. Si el objetivo lo permite, podemos obtener:

* Longitud
* Latitud
* Precisión
* Altitud (no siempre disponible)
* Dirección (solo disponible si el usuario se mueve)
* Velocidad (solo disponible si el usuario se mueve)

Además de la información de ubicación, también obtenemos **Información del dispositivo** sin necesidad de permisos:

* ID único mediante huella digital Canvas
* Modelo del dispositivo (no siempre disponible)
* Sistema operativo
* Plataforma
* Número de núcleos de CPU (resultados aproximados)
* Cantidad de RAM (resultados aproximados)
* Resolución de pantalla
* Información de la GPU
* Nombre y versión del navegador
* Dirección IP pública
* Dirección IP local
* Puerto local

Tras recibir la información anterior, se realiza un **reconocimiento automático de la dirección IP**.

**Esta herramienta es una prueba de concepto y tiene fines exclusivamente educativos. Seeker muestra qué datos puede recopilar un sitio web malicioso sobre usted y sus dispositivos, y por qué no debe hacer clic en enlaces aleatorios ni otorgar permisos críticos como la ubicación, etc.**

## ¿En qué se diferencia de la geolocalización por IP?

* Otras herramientas y servicios ofrecen geolocalización por IP, la cual no es precisa y no proporciona la ubicación del objetivo, sino la ubicación aproximada del proveedor de servicios de internet (ISP).

* Seeker utiliza la API HTML, obtiene el permiso de ubicación y luego captura la longitud y latitud mediante el hardware GPS del dispositivo. Por lo tanto, Seeker funciona mejor con teléfonos inteligentes. Si el hardware GPS no está presente, como en una computadora portátil, Seeker recurre a la geolocalización por IP o busca coordenadas almacenadas en caché.

* Generalmente, si un usuario acepta el permiso de ubicación, la precisión de la información recibida es de aproximadamente 30 metros.

* La precisión depende de varios factores que usted puede o no controlar, como:

* Dispositivo: No funciona en portátiles ni teléfonos con GPS averiado.

* Navegador: Algunos navegadores bloquean JavaScript.

* Calibración del GPS: Si el GPS no está calibrado, puede obtener resultados inexactos, lo cual es muy común.

## Plantillas

Plantillas disponibles:

* NearYou
* Google Drive (Sugerida por @Akaal_no_one)
* WhatsApp (Sugerida por @Dazmed707)
* Telegram
* Zoom (Creada por @a7maadf)
* Google reCAPTCHA (Creada por @MrEgyptian)

¡Crea tu propia plantilla! Los pasos para crear tu plantilla se describen en este [how-to](./createTemplate.md).

Una vez que tu plantilla esté lista, **no olvides proponerla a la comunidad mediante una solicitud de extracción (pull request)**.

## Probado en:

* Kali Linux
* BlackArch Linux
* Ubuntu
* Fedora
* Kali Nethunter
* Termux
* Parrot OS
* OSX - Monterey v.12.0.1

## Installation

### Kali Linux / Arch Linux / Ubuntu / Fedora / Parrot OS / Termux

```bash
git clone https://github.com/ChristopherPuruncaja/synergy.git
cd synergy/
chmod +x install.sh
./install.sh
```

### BlackArch Linux

```bash
sudo pacman -S seeker
```

### Docker

```bash
docker pull thewhiteh4t/seeker
```

### OSX
```bash
git clone https://github.com/thewhiteh4t/seeker.git
cd seeker/
python3 seeker.py
````

In order to run in tunnel mode, install ngrok by running this command in the terminal:
```bash
brew install ngrok/ngrok/ngrok

ngrok http 8080
````

## Usage

```bash
python3 seeker.py -h

usage: seeker.py [-h] [-k KML] [-p PORT] [-u] [-v] [-t TEMPLATE] [-d] [--telegram token:chatId] [--webhook WEBHOOK]

options:
  -h, --help                            show this help message and exit
  -k KML, --kml KML                     KML filename
  -p PORT, --port PORT                  Web server port [ Default : 8080 ]
  -u, --update                          Check for updates
  -v, --version                         Prints version
  -t TEMPLATE, --template TEMPLATE      Auto choose the template with the given index
  -d, --debugHTTP                       Disable auto http --> https redirection for testing purposes 
                                        (only works for the templates having index_temp.html file)
  --telegram                            Send info to a telegram bot, provide telegram token and chat to use
                                        format = token:chatId separated by a colon
  --webhook                             Send events to a webhook endpoint to be processed
                                        Note : endpoint must be unauthenticated and accept POST request

#########################
# Environment Variables #
#########################

Some of the options above can also be enabled via environment variables, to ease deployment.
Other parameters can be provided via environment variables to avoid interactive mode.

Variables:
  DEBUG_HTTP            Same as -d, --debugHTTP
  PORT                  Same as -p, --port
  TEMPLATE              Same as -t, --template
  TITLE                 Provide the group title or the page title
  REDIRECT              Provide the URL to redirect the user to, after the job is done
  IMAGE                 Provide the image to use, can either be remote (http or https) or local
                        Note : Remote image will be downloaded locally during the startup
  DESC                  Provide the description of the item (group or webpage depending on the template)
  SITENAME              Provide the name of the website
  DISPLAY_URL           Provide the URL to display on the page
  MEM_NUM               Provide the number of group membres (Telegram so far)
  ONLINE_NUM            Provide the number of the group online members (Telegram so far)
  TELEGRAM              Provide telegram token and chat to use to send info to a telegram bot
                        format = token:chatId separated by a colon
  WEBHOOK               Provide the webhook url to forward the events to 
                        Note : endpoint should be unauthenticated and accept POST method
                        

##################
# Usage Examples #
##################

# Step 1 : In first terminal
$ python3 synergy.py

# Step 2 : In second terminal start a tunnel service such as ngrok
$ ./ngrok http 8080

###########
# Options #
###########

# Ouput KML File for Google Earth
$ python3 synergy.py -k <filename>

# Use Custom Port
$ python3 synergy.py -p 1337
$ ./ngrok http 1337

# Pre-select a specific template
$ python3 synergy.py -t 1

################
# Docker Usage #
################

# Step 1
$ docker network create ngroknet

# Step 2
$ docker run --rm -it --net ngroknet --name synergy thewhiteh4t/synergy

# Step 3
$ docker run --rm -it --net ngroknet --name ngrok wernight/ngrok ngrok http synergy:8080
```

## Local Tunnels
Use
```
ssh -R 80:localhost:8080 nokey@localhost.run
```
as an alterntive to ngrok


