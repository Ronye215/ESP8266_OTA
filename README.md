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

_Al momento de instalar y agregar la tarjeta ESP8266 al entorno de arduino podemos hacer uso de todas las caracteristicas que la placa ofrece_

_Para crear un codigo OTA propio podemos modificar con nuestro propio codigo el siguiente codigo_

```
#include <ESP8266WiFi.h>
#include <ESP8266mDNS.h>
#include <WiFiUdp.h>
#include <ArduinoOTA.h>

#ifndef STASSID
#define STASSID "your-ssid"
#define STAPSK  "your-password"
#endif

const char* ssid = STASSID;
const char* password = STAPSK;

void setup() {
  Serial.begin(115200);
  Serial.println("Booting");
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);
  while (WiFi.waitForConnectResult() != WL_CONNECTED) {
    Serial.println("Connection Failed! Rebooting...");
    delay(5000);
    ESP.restart();
  }

  // Port defaults to 8266
  // ArduinoOTA.setPort(8266);

  // Hostname defaults to esp8266-[ChipID]
  // ArduinoOTA.setHostname("myesp8266");

  // No authentication by default
  // ArduinoOTA.setPassword("admin");

  // Password can be set with it's md5 value as well
  // MD5(admin) = 21232f297a57a5a743894a0e4a801fc3
  // ArduinoOTA.setPasswordHash("21232f297a57a5a743894a0e4a801fc3");

  ArduinoOTA.onStart([]() {
    String type;
    if (ArduinoOTA.getCommand() == U_FLASH) {
      type = "sketch";
    } else { // U_FS
      type = "filesystem";
    }

    // NOTE: if updating FS this would be the place to unmount FS using FS.end()
    Serial.println("Start updating " + type);
  });
  ArduinoOTA.onEnd([]() {
    Serial.println("\nEnd");
  });
  ArduinoOTA.onProgress([](unsigned int progress, unsigned int total) {
    Serial.printf("Progress: %u%%\r", (progress / (total / 100)));
  });
  ArduinoOTA.onError([](ota_error_t error) {
    Serial.printf("Error[%u]: ", error);
    if (error == OTA_AUTH_ERROR) {
      Serial.println("Auth Failed");
    } else if (error == OTA_BEGIN_ERROR) {
      Serial.println("Begin Failed");
    } else if (error == OTA_CONNECT_ERROR) {
      Serial.println("Connect Failed");
    } else if (error == OTA_RECEIVE_ERROR) {
      Serial.println("Receive Failed");
    } else if (error == OTA_END_ERROR) {
      Serial.println("End Failed");
    }
  });
  ArduinoOTA.begin();
  Serial.println("Ready");
  Serial.print("IP address: ");
  Serial.println(WiFi.localIP());
}

void loop() {
  ArduinoOTA.handle();
}
```
