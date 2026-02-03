# Objetivos de la Práctica
#### 1. Monta un Ubuntu 24 como servidor de streaming

1. Instala FFmpeg.
2. Descarga el vídeo de Aules. Se trata de un .mp4 a 1080p.
3. Haz
ffprobe -v error -show_streams fichero.mp4
y localiza información que has estudiado
4. Remuxing: cambio de contenedor. De .mp4 a .mkv:
ffmpeg -i original.mp4 -c:v copy -c:a copy salida.mkv
Responde:
a) ¿Ha cambiado el tamaño de forma significativa?
b) ¿Ha habido carga de CPU?¿Ha tardado mucho?
5. Cambio de códecs y comparación.
5. Cambio de códecs y comparación.

Crea el fichero en H.264 con un bitrate de 2Mbps:
```bash
ffmpeg -i original.mp4 -c:v libx264 -b:v 2M -c:a copy
h264_2mbps.mp4
```

Ahora hazlo en H.265 con el mismo bitrate:

```bash
ffmpeg -i original.mp4 -c:v libx265 -b:v 2M -c:a copy
h265_2mbps.mp4
```

● Reproduce ambos vídeos a la vez. Pon pausa en una escena con mucho movimiento.

● ¿Cuál de los dos presenta más "artefactos" (cuadraditos)?


● Si ambos tienen el mismo bitrate (2 Mbps), ¿pesan lo mismo los archivos finales?

6. Simulación de streaming con diferentes tipos de fichero.

1. Low (móvil):

Resolución 240p

Bitrate: 400k

2. High (fibra):

Resolución: 1080p

Bitrate: 2Mbps

---

## Preguntas finales:

Almacenamiento: Si tu servidor tiene un disco de 500 GB, ¿cuántas horas de vídeo del perfil "HD" (2 Mbps) podrías alojar?

Red: Tienes una línea de 100 Mbps simétricos. ¿Cuántos usuarios podrían ver el perfil "Móvil" (400 kbps) simultáneamente antes de saturar el 80% de la línea?