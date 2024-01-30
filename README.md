# Solo para una Imagen Herida


<p float="center">
   &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;
   &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; 
  <img src="https://github.com/alejoRGB/Solo-para-una-imagen-herida/blob/main/1T8A1022.JPG" width="400"/>
</p>
<p float="center">
<img src="https://github.com/alejoRGB/Solo-para-una-imagen-herida/blob/main/WhatsApp%20Image%202024-01-29%20at%2009.54.31.jpeg" width="250" />
   &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;
<img src="https://github.com/alejoRGB/Solo-para-una-imagen-herida/blob/main/1T8A1033.JPG" width="250" /> 
 &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;
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

Link server: https://drive.google.com/file/d/1eXvFFY03ChPnQHWmixiWRVksmJXMQVWD/view


