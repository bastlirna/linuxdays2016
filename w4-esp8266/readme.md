# Drátujeme IoT: ESP8266
Workshop na programování chipu ESP8266

## Demo 1
Naprogramujte ESP8266 tak aby po seriové lince vypisovalo "Hello world". Použijte Arduino knihovny.

## Demo 2
Ukázka připojení k MQTT serveru. [demo 2] (demo2.zip)

* Přepište kód tak, aby jste zápisem do kanálu **/linuxdays/espDemoBoard*<serialNO>*/command** mohli rozsvítit ledku.
* Přepište kód tak, aby při stisku tlačítka odeslal zprávu do topicu **/linuxdays/espDemoBoard*<serialNO>*/button**


## Používané knihovny
	
	lib_deps = WifiManager@~0.12, PubSubClient@~2.6, DebouncedInput@~1.0.13
