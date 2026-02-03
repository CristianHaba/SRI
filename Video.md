# Objetivos de la Práctica
#### 1. Monta un Ubuntu 24 como servidor de streaming

1. Instala FFmpeg.

```bash
sudo apt install ffmpeg
```

2. Descarga el vídeo de Aules. Se trata de un .mp4 a 1080p.
3. Haz ffprobe -v error -show_streams fichero.mp4
y localiza información que has estudiado

**Información Imporatente**

* codec_name=h264

* width=1920

* height=1080

* r_frame_rate=24/1

* duration=30.000000

* bit_rate=5860270

* codec_name=aac

* sample_rate=48000

* channels=6

* r_frame_rate=0/0

* duration=30.000000

 * bit_rate=192580

---

## Remuxing: cambio de contenedor. De .mp4 a .mkv:
```bash
sudo ffmpeg -i big-buck-bunny-1080p-30sec.mp4 -c:v copy -c:a copy big-bunny.mkv
```

**a) ¿Ha cambiado el tamaño de forma significativa?**

![tamaño1](/imagenes/capturas_video/tamaño%20imagen.png)

Casi no ha cambiado el tamaño

**b) ¿Ha habido carga de CPU?¿Ha tardado mucho?**

Ha tenido muy poca carga, ha tardado muy pocos segundos.

---
## Cambio de códecs y comparación.

Crea el fichero en H.264 con un bitrate de 2Mbps:
```bash
ffmpeg -i big-buck-bunny-1080p-30sec.mp4 -c:v libx264 -b:v 2M -c:a copy h264_2mbps.mp4
```

Ahora hazlo en H.265 con el mismo bitrate:

```bash
ffmpeg -i big-buck-bunny-1080p-30sec.mp4 -c:v libx265 -b:v 2M -c:a copy h265_2mbps.mp4
```
---
## Reproduce ambos vídeos a la vez. Pon pausa en una escena con mucho movimiento.

* ¿Cuál de los dos presenta más "artefactos" (cuadraditos)?

El de 2 de bitrate ya que tiene mas pixeles borrosos


* Si ambos tienen el mismo bitrate (2 Mbps), ¿pesan lo mismo los archivos finales?

![tamaño2](/imagenes/capturas_video/tamañovideo.png)

NO pesan lo mismo, en mi caso el que utiliza H.265 pesa 8 MB menos que el que utiliza H.264.
 
## Simulación de streaming con diferentes tipos de fichero.

# Low (móvil):

Resolución 240p

Bitrate: 400k

```bash
ffmpeg -i big-buck-bunny-1080p-30sec.mp4 -vf "scale=-2:240" -c:v libx264 -b:v 400k -c:a copy low_movil.mp4
```
<video src="/imagenes/capturas_video/low.mp4"
       controls
       style="max-width: 1000px;">
</video>


# High (fibra):

Resolución: 1080p

Bitrate: 2Mbps

```bash
ffmpeg -i big-buck-bunny-1080p-30sec.mp4 -vf scale=-1:1080 -b:v 2M high.mp4
```

<video src="/imagenes/capturas_video/high.mp4"
       controls
       style="max-width: 1000px;">
</video>

---

## Preguntas finales:

Almacenamiento: Si tu servidor tiene un disco de 500 GB, ¿cuántas horas de vídeo del perfil "HD" (2 Mbps) podrías alojar?

1. Convertir 2 Mbps a MB/s
2 Mbps = 2/8 = 0,25 MB/s

2. Calcular cuántos MB ocupa una hora de vídeo
0,25 MB/s × 3600 s = 900 MB/h

Cada hora de vídeo HD a 2 Mbps ocupa aprox. 0,9 GB.

3. Con un disco de 500 GB
500 GB / 0,9 GB/h ≈ 555 horas

Red: Tienes una línea de 100 Mbps simétricos. ¿Cuántos usuarios podrían ver el perfil "Móvil" (400 kbps) simultáneamente antes de saturar el 80% de la línea?

1. Capacidad útil al 80 %
100 Mbps × 0,8 = 80 Mbps

2. Bitrate por usuario (perfil Móvil)
400 kbps = 0,4 Mbps

3. Número máximo de usuarios simultáneos
80 Mbps / 0,4 Mbps = 200 