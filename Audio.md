# Objetivos de la Práctica
#### 1. Monta un Ubuntu 24 como servidor de streaming

a. Red: adaptador puente (configura como fija la IP que te dé el DHCP)

b. Comprueba que funciona el sonido

c. Instala Icecast2

#### 2. Monta otro Ubuntu 24 como DJ

a. Red: adaptador puente

b. Comprueba que funciona el sonido

c. Instala Mixxx

d. Crea una radio con tu nombre (/manu)

#### 3. Comprueba en la máquina anfitrión que escuchas tus ficheros. Hazlo desde el navegador y desde VLC. 

---

### 1. Monta un Ubuntu 24 como servidor de streaming

a. Red: adaptador puente (configura como fija la IP que te dé el DHCP)

| Campos |  Configuración |
| ----------- | ----------- |
| IP | 192.168.1.139 |
| Máscara | 24 |
| Gateway | 192.168.1.1|
| DNS | 8.8.8.8 |

---
b. Comprueba que funciona el sonido

```bash
sudo apt install alsa-utils -y
```

Este comando sirve para instalar un paquete que nos va a permitir controlar y mezclar el audio, la reproducción y grabación.

```bash
speaker-test -t sine -f 440
```
Este comandoreproduce un tono puro de 440 Hz (la nota La estándar) para comprobar que tu sistema de audio funciona correctamente.

---
c. Instala Icecast2

```bash
sudo apt install icecast2 -y 
```
Con este comando instalamos el servicio de icecast2.


### 2. Monta un Ubuntu 24 como cliente DJ

a. Red: adaptador puente (configura como fija la IP que te dé el DHCP)

| Campos |  Configuración |
| ----------- | ----------- |
| IP | 192.168.1.141 |
| Máscara | 24 |
| Gateway | 192.168.1.1|
| DNS | 8.8.8.8 |

---
b. Comprueba que funciona el sonido

```bash
sudo apt install alsa-utils -y
```

Este comando sirve para instalar un paquete que nos va a permitir controlar y mezclar el audio, la reproducción y grabación.

```bash
speaker-test -t sine -f 440
```
Este comandoreproduce un tono puro de 440 Hz (la nota La estándar) para comprobar que tu sistema de audio funciona correctamente.

---
c. Instala Mixxx

```bash
sudo apt install mixxx -y 
```
Con este comando instalamos el servicio de Mixxx.

* Configuración de Mixxx

Ahora abrimos Mixxx y vamos al apartado: 

"Opciones --> Preferencias --> Emisión en vivo".

En el apartado de conexión al servidor hay que poner:

| Campos |  Configuración |
| ----------- | ----------- |
| Servidor | 192.168.1.139 |
| Montar | /haba |
| Identificación | source|
| Contraseña | 1234 |

Cuando tengamos esta configuración clickamos en el apartado de "Aceptar".

Ahora tenemos que descargar una canción e importarla en Mixx, podemos importarla arrastrandola desde la carpeta a la interfaz de Mixx.

Cuando la tengamos tenemos que darle a la opción "ON AIR" hasta que se ponga en verde.

## COMPROBACIÓN NAVEGADOR

http://192.168.1.139:8000/haba

[Ver video](/imagenes/capturas_audio/navegador.mp4)

## COMPROBACIÓN VLC

http://192.168.1.139:8000/haba

[Ver video](/imagenes/capturas_audio/vlc.mp4)
