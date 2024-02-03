# Solo para una Imagen Herida


<p float="center">
   &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;
   &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 
  <img src="https://github.com/alejoRGB/Solo-para-una-imagen-herida/blob/main/1T8A1022.JPG" width="400"/>
</p>
<p float="center">
<img src="https://github.com/alejoRGB/Solo-para-una-imagen-herida/blob/main/WhatsApp%20Image%202024-01-29%20at%2009.54.31.jpeg" width="250" />
   &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;
<img src="https://github.com/alejoRGB/Solo-para-una-imagen-herida/blob/main/1T8A1033.JPG" width="250" /> 
 &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;
<img src="https://github.com/alejoRGB/Solo-para-una-imagen-herida/blob/main/WhatsApp%20Image%202024-01-29%20at%2022.49.53.jpeg" width="250" /> 
 
  
</p>

_Solo para una Imagen Herida_ es una obra interactiva realizada por Lucía Ranzuglia en el marco de la materia Proyecto Audiovisual 4 en la cátedra [Cámpos-Trilnick](https://campostrilnick.org/equipo/) de
la facultad de Arquitectura, diseño y urbanismo de la [UBA](https://www.uba.ar/).


> Solo para una imagen herida es una escultura sonora realizada con desechos de hierro común. La disposición de estos tubos pendulan entre lo aleatorio y lo dispuesto, mientras que funcionan como plataforma para activar la reproducción -mediante el tacto- de una serie de tracks sonoros extraidos del ruido de una cinta de video magnético herida por su propioa sobre-reproduccion. Un instrumento ruidoso, con el fin de poner de manifiesto el carácter esencial y no accidental del ruido, trabajando una estética propia de los aparatos y no necesariamente de lo "real" y lo visible.


## Realización Técnica

La solución técnica para el funcionamiento de la obra se divide en 2 partes. Por un se encuentra el sensado de las personas cuando tocan la obra y por otro lado la reproducción sonora de los sonidos que fueron compuestos por la artista. 

### Detección táctil.

Para detectar cuando una persona se encuentra en contacto con la obra se utilizó un [Sensor Capacitivo](https://es.wikipedia.org/wiki/Sensor_capacitivo). Este tipo de sensores son capaces de dectar la diferencia de corriente de un objeto conductor, en este caso los tubos de hierro, cuando este se encuentra en contacto con el cuerpo humano. En este caso usamos uno 
de los sensores capacitivos que vienen incorporados en la placa de desarrollo [ESP32](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/touch_pad.html)

La programación fue hecha con el[Arduino IDE](https://proyectoidis.org/arduino/)
```
  int total = sensor.capacitiveSensor(30);

  threshold = 9000;

  if (total > threshold) {
    Serial.println("1");
  } else {
    Serial.println("0");
  }

```

En el codigo se establece un umbral de valores que detecta el sensor, cuando este umbral es superado significa que alguien está tocando la 
obra. En ese momento el arduino envía mediante comunicación [Serial](https://es.wikipedia.org/wiki/Comunicaci%C3%B3n_serie) el número 1 al servidor que esta escuchando el puerto 
que le especificamos, lo cual activa los sonidos

### Reprodución de Sonidos.

En la carpeta incluida en este repositorio se encuentran todos los archivos necesarios para reproducir los sonidos.
Para iniciar este paso es necesario que tengamos ya conectado nuestro arduino o ESP32 y que este seteado el mismo puerto serial
que esta indicado en el archivo src/App.js. Más adelante daremos más detalles de la configuración que se puede hacer en este archivo. 


<img src="https://github.com/alejoRGB/Solo-para-una-imagen-herida/blob/main/server_manu.PNG" width="500" />


Primero hay que abrir una terminal, o powershell, en la direccion donde tengamos la carpeta descargada. 
Luego hay que ejecutar 2 comandos: 

```
npm run server

```
Este comando inicializa el servidor.

```
npm run start

```
Este comando nos abre un navegador en la dirección localhost:3000 la cual se encarga de recibir los comandos 
que llegan por el puerto serial que tengamos seteado y reproduce los sonidos.

En el archivo "src/App.js" se encuentran los valores que indican que sonidos y de que forma se reproducen al llegarles las señales del
sensor capacitivo. 

Los archivos de audio estan cargados en la carpeta "sonidos" e importados de la siguiente manera:
```
const SONIDOS_TRIGGEREABLES = [
	"/sonidos/NOISE_AGUDO.wav",
	"/sonidos/NOISE_GRAVE.wav",
	"/sonidos/LOOPS_VOCES.wav",
	"/sonidos/LOOP_VOCES.wav",
	"/sonidos/PERSONA_HABLANDO_EN_INGLES.wav",
	"/sonidos/GLITCH.wav",
	"/sonidos/TELE_Y_NOISE.wav",
	"/sonidos/MUSICA_GLITCH.wav",
	"/sonidos/GRITOS.wav",
	"/sonidos/RUIDO_FINITO.wav",
	"/sonidos/RUIDO_CLARO.wav",
];

```

La variable "ATTACK_CAPAS_DE_SONIDO" indica los milisegundos que tarda el programa en reproducir un audio desde que recibe la señal. Un valor más bajo
indica que es más inmediata la reproducción desde que recibe la señal. "RELEASE_CAPAS_DE_SONIDO" indica cuanto tardan los sonidos en dejar de sonar una vez que
el espectador deja de tocar la escultura, es decir cuando el sensor deja de envíar señales. 
```
const ATTACK_CAPAS_DE_SONIDO = 150;
const RELEASE_CAPAS_DE_SONIDO = 5000;

```

Los sonidos tienen un efecto de "overlaping" es decir que se reproduce más de una vez los sonidos, sin esperar a que el primero termine de sonar.
Este efecto genera una sensación de "capas" de sonido" que se van agregando una encima de la otra, mezclando los sonidos. Las variables que afectan este
efecto se encuentran con el prefijo "PHASER". 

```
const PHASER = 0.7;
const PHASER_FREQ = 0;
const PHASER_BASE_FREQ = 100;
const PHASER_OCTAVAS = 1;

```



