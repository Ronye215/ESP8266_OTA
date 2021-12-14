# ESP8266 Over-The-Air
_Se trata de un chip integrado con conexión WiFi y compatible con el protocolo TCP/IP. El objetivo principal es dar acceso a cualquier microcontrolador a una red._
_La gran ventaja del ESP8266 es su bajo consumo. Es el producto ideal para wereables y dispositivos del IoT._

## Comenzando 🚀

_En este repositorio encontraras las herramientas necesarias para realizar pruebas locales._


### Pre-requisitos 📋

_Los requisitos necesarios para realizar este proyecto son:_

```
* Sistema Windows 7 o posteriores
* Python 2.7
* Entorno de programación arduino 1.6.4 o posteriores
* Librerias OTA
```

### Instalación 🔧

_Para la instalación y uso se necesita instalar [python-2.7.msi](https://github.com/Ronye215/ESP8266_OTA/blob/main/python-2.7.msi)_

_Esto utilizando la insttalación asistida de Python_

* [Pasos](https://user-images.githubusercontent.com/88066056/146032737-2f85e2f7-e354-4119-9e06-a61147404fd6.jpg)

_Al igual para la instalación del entorno de Arduino_

* [Arduino ide 1.8.16](https://downloads.arduino.cc/arduino-1.8.16-windows.exe)

_Las librerias OTA se incluyen automaticamente al agregar el microprocesador ESP8266 al entorno de programación Arduino_

_En Arduino ide, nos dirijimos a_

```
Archivo -> Preferencias -> Gestor de URLs Adicionales de Tarjetas
```

_Y agregamos el siguiente Link_

```
http://arduino.esp8266.com/stable/package_esp8266com_index.json
```

_Para agregar la tarjeta ESP8266 nos dirijimos a_ 

```
Herramientas -> Placa -> Gestor de tarjetas
```

_Y en el filtro de busqueda ponemos -ESP8266- e instalamos la ultima versión_

# Uso ✔
