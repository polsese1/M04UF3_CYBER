1) Importación de módulos:


``` import urllib.request
import json
```

- urllib.request: Este módulo permite realizar solicitudes HTTP para acceder a datos en línea. En este caso, se usa para obtener información desde la API del clima.


- json: Este módulo se usa para manejar datos en formato JSON (JavaScript Object Notation), que es el formato en el que la API devuelve la información del clima.


2) Función consultar_tiempo:


``` def consultar_tiempo(nombre_ciudad, lat, lon): ```


- nombre_ciudad: El nombre de la ciudad.

- lat: La latitud de la ciudad.

- lon: La longitud de la ciudad.


``` enlace = "https://api.open-meteo.com/v1/forecast" + \
         "?latitude=" + str(lat) + "&longitude=" + str(lon) + \
         "&current=temperature_2m,wind_speed_10m,relative_humidity_2m" 
```

Aquí se está construyendo la URL de la API de Open-Meteo, agregando la latitud y longitud de la ciudad, así como los parámetros para obtener la temperatura a 2 metros, la velocidad del viento a 10 metros y la humedad relativa a 2 metros.


``` with urllib.request.urlopen(enlace) as respuesta_api:
    info_tiempo = json.load(respuesta_api)
```

Se hace una solicitud a la API con urllib.request.urlopen(enlace). El resultado de la respuesta se carga en un objeto Python usando json.load, lo que convierte la respuesta JSON en un diccionario de Python.


``` print("Clima actual en " + nombre_ciudad + ":")
print(" - Temp. actual:", info_tiempo["current"]["temperature_2m"], "°C")
print(" - Viento:", info_tiempo["current"]["wind_speed_10m"], "km/h")
print(" - Humedad:", info_tiempo["current"]["relative_humidity_2m"], "%")
```

Finalmente, se imprime la información obtenida del clima, que incluye la temperatura, la velocidad del viento y la humedad relativa, accediendo a los valores en el diccionario info_tiempo.


3) Función menu_clima_interactivo:


``` def menu_clima_interactivo():
    eleccion = -1
```

Esta función crea un menú interactivo en el que el usuario puede seleccionar entre varias ciudades para consultar el clima.


``` while eleccion != 0:
    print("Menu de consulta del clima")
    print("1 - Barcelona")
    print("2 - Madrid")
    print("3 - Valencia")
    print("0 - Salir")
```

Aquí se imprime el menú de opciones. El usuario puede elegir entre consultar el clima de tres ciudades (Barcelona, Madrid y Valencia) o salir del programa.
entrada_usuario = input("Selecciona una ciudad (0-3): ")
Se solicita al usuario que ingrese su elección.


``` if entrada_usuario.isdigit():
    eleccion = int(entrada_usuario)
    match eleccion:
```
Si la entrada del usuario es un número válido (comprobado con isdigit()), se convierte en entero y se evalúa mediante un match.


``` case 0:
    print("Saliendo..")
case 1:
    consultar_tiempo("Barcelona", 41.3888, 2.159)
case 2:
    consultar_tiempo("Madrid", 40.4165, -3.7026)
case 3:
    consultar_tiempo("Valencia", 39.4699, -0.3763)
case _:
    print("Numero fuera de rango. Intenta de nuevo.")
Caso 0: Imprime "Saliendo.." y termina el ciclo.
```


Caso 1, 2, 3: Llama a la función consultar_tiempo con las coordenadas de Barcelona, Madrid o Valencia.


Caso _: Si el número no está en el rango 0-3, muestra un mensaje de error.


``` else:
    print("Entrada no valida. Debes escribir un numero.")
```

Si el usuario ingresa algo que no es un número, se muestra un mensaje de error.


4) Ejecutar el programa:

``` menu_clima_interactivo()
```
Llama a la función menu_clima_interactivo() para iniciar la interacción con el usuario.

