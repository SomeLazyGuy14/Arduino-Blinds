# Arduino-Blinds
Adding to the school sensor
This example for the Arduino Yún shows how to use the Bridge library to access the digital and analog pins on the board through REST calls. It demonstrates how you can create your own API when using REST style calls through the browser.

When running this example, make sure your computer is on the same network as the Yún. When you have have programmed the board, you can request the value on a pin, write a value to a pin, and configure a pin as an input or output.

When the REST password is turned off, you can use a browser with the following URL structure :

http://myArduinoYun.local/arduino/digital/13 : calls digitalRead(13);
http://myArduinoYun.local/arduino/digital/13/1 : calls digitalWrite(13,1);
http://myArduinoYun.local/arduino/analog/9/123 : analogWrite(9,123);
http://myArduinoYun.local/arduino/analog/2 : analogRead(2);
http://myArduinoYun.local/arduino/mode/13/input : pinMode(13, INPUT);
http://myArduinoYun.local/arduino/mode/13/output : pinMode(13, OUTPUT);
You can use the CURL command from the command line instead of a browser if you prefer.

Hardware Required

Arduino Yún
computer and Yún on the same wireless or wired network
Software Required

web browser
Circuit

There is no circuit for this example.


image developed using Fritzing. For more circuit examples, see the Fritzing project page

Code

The example code shows how it is possible to make REST requests to the Yún to read from and write information to the board's pins.

You need to include the Bridge, YunServer, and YunClient libraries :

#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>
[Get Code]
Instantiate a server enabling the the Yun to listen for connected clients.

YunServer server;

In setup(), start serial communication for debugging purposes, and turn the built-in LED on pin 13 high while Bridge begins. Bridge.begin() is blocking, and should take about 2 seconds to complete. Once Bridge starts up, turn the LED off.

void setup() {
  Serial.begin(9600);
  pinMode(13,OUTPUT);
  digitalWrite(13, LOW);
  Bridge.begin();
  digitalWrite(13, HIGH);
[Get Code]
In the second part of setup(), tell the instance of YunServer to listen for incoming connections only coming from localhost. Connections made to Linux will be passed to the 32U4 processor for parsing and controlling the pins. This happens on port 5555. Start the server with server.begin().

server.listenOnLocalhost();
  server.begin();
}
[Get Code]
In loop(), you'll create an instance of the YunClient for managing the connection. If the client connects, process the requests in a custom function (described below) and close the connection when finished.

Putting a delay at the end of loop() will be helpful in keeping the processor from doing too much work.

void loop() {
  YunClient client = server.accept();

  if (client) {
    process(client);
    client.stop();
  }

  delay(50); 
}
[Get Code]
Create a function named process that accepts the YunClient as its argument. Read the command by creating a string to hold the incoming information. Parse the REST commands by their functionality (digital, analog, and mode) and pass the information to the appropriately named function.

void process(YunClient client) {
  String command = client.readStringUntil('/');

  if (command == "digital") {
    digitalCommand(client);
  }
  if (command == "analog") {
    analogCommand(client);
  }
  if (command == "mode") {
    modeCommand(client);
  }
}
[Get Code]
Create a function to deal with digital commands. Accept the client as the argument. Create some local variables to hold the pin and value of the command.

void digitalCommand(YunClient client) {
  int pin, value;
[Get Code]
Parse the client's request for the pin to work with using client.parseInt().
This example for the Arduino Yún shows how to use the Bridge library to access the digital and analog pins on the board through REST calls. It demonstrates how you can create your own API when using REST style calls through the browser.

When running this example, make sure your computer is on the same network as the Yún. When you have have programmed the board, you can request the value on a pin, write a value to a pin, and configure a pin as an input or output.

When the REST password is turned off, you can use a browser with the following URL structure :

http://myArduinoYun.local/arduino/digital/13 : calls digitalRead(13);
http://myArduinoYun.local/arduino/digital/13/1 : calls digitalWrite(13,1);
http://myArduinoYun.local/arduino/analog/9/123 : analogWrite(9,123);
http://myArduinoYun.local/arduino/analog/2 : analogRead(2);
http://myArduinoYun.local/arduino/mode/13/input : pinMode(13, INPUT);
http://myArduinoYun.local/arduino/mode/13/output : pinMode(13, OUTPUT);
You can use the CURL command from the command line instead of a browser if you prefer.

Hardware Required

Arduino Yún
computer and Yún on the same wireless or wired network
Software Required

web browser
Circuit

There is no circuit for this example.


image developed using Fritzing. For more circuit examples, see the Fritzing project page

Code

The example code shows how it is possible to make REST requests to the Yún to read from and write information to the board's pins.

You need to include the Bridge, YunServer, and YunClient libraries :

#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>
[Get Code]
Instantiate a server enabling the the Yun to listen for connected clients.

YunServer server;

In setup(), start serial communication for debugging purposes, and turn the built-in LED on pin 13 high while Bridge begins. Bridge.begin() is blocking, and should take about 2 seconds to complete. Once Bridge starts up, turn the LED off.

void setup() {
  Serial.begin(9600);
  pinMode(13,OUTPUT);
  digitalWrite(13, LOW);
  Bridge.begin();
  digitalWrite(13, HIGH);
[Get Code]
In the second part of setup(), tell the instance of YunServer to listen for incoming connections only coming from localhost. Connections made to Linux will be passed to the 32U4 processor for parsing and controlling the pins. This happens on port 5555. Start the server with server.begin().

server.listenOnLocalhost();
  server.begin();
}
[Get Code]
In loop(), you'll create an instance of the YunClient for managing the connection. If the client connects, process the requests in a custom function (described below) and close the connection when finished.

Putting a delay at the end of loop() will be helpful in keeping the processor from doing too much work.

void loop() {
  YunClient client = server.accept();

  if (client) {
    process(client);
    client.stop();
  }

  delay(50); 
}
[Get Code]
Create a function named process that accepts the YunClient as its argument. Read the command by creating a string to hold the incoming information. Parse the REST commands by their functionality (digital, analog, and mode) and pass the information to the appropriately named function.

void process(YunClient client) {
  String command = client.readStringUntil('/');

  if (command == "digital") {
    digitalCommand(client);
  }
  if (command == "analog") {
    analogCommand(client);
  }
  if (command == "mode") {
    modeCommand(client);
  }
}
[Get Code]
Create a function to deal with digital commands. Accept the client as the argument. Create some local variables to hold the pin and value of the command.

void digitalCommand(YunClient client) {
  int pin, value;
[Get Code]
Parse the client's request for the pin to work with using client.parseInt().

If the character after the pin is a "/", it means the URL is going to have a value of 1 or 0 following. This value will assign a value to the pin, turning it HIGH or LOW. If there is no trailing "/", read the value from the specified pin.

pin = client.parseInt();

  if (client.read()This example for the Arduino Yún shows how to use the Bridge library to access the digital and analog pins on the board through REST calls. It demonstrates how you can create your own API when using REST style calls through the browser.

When running this example, make sure your computer is on the same network as the Yún. When you have have programmed the board, you can request the value on a pin, write a value to a pin, and configure a pin as an input or output.

When the REST password is turned off, you can use a browser with the following URL structure :

http://myArduinoYun.local/arduino/digital/13 : calls digitalRead(13);
http://myArduinoYun.local/arduino/digital/13/1 : calls digitalWrite(13,1);
http://myArduinoYun.local/arduino/analog/9/123 : analogWrite(9,123);
http://myArduinoYun.local/arduino/analog/2 : analogRead(2);
http://myArduinoYun.local/arduino/mode/13/input : pinMode(13, INPUT);
http://myArduinoYun.local/arduino/mode/13/output : pinMode(13, OUTPUT);
You can use the CURL command from the command line instead of a browser if you prefer.

Hardware Required

Arduino Yún
computer and Yún on the same wireless or wired network
Software Required

web browser
Circuit

There is no circuit for this example.


image developed using Fritzing. For more circuit examples, see the Fritzing project page

Code

The example code shows how it is possible to make REST requests to the Yún to read from and write information to the board's pins.

You need to include the Bridge, YunServer, and YunClient libraries :

#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>
[Get Code]
Instantiate a server enabling the the Yun to listen for connected clients.

YunServer server;

In setup(), start serial communication for debugging purposes, and turn the built-in LED on pin 13 high while Bridge begins. Bridge.begin() is blocking, and should take about 2 seconds to complete. Once Bridge starts up, turn the LED off.

void setup() {
  Serial.begin(9600);
  pinMode(13,OUTPUT);
  digitalWrite(13, LOW);
  Bridge.begin();
  digitalWrite(13, HIGH);
[Get Code]
In the second part of setup(), tell the instance of YunServer to listen for incoming connections only coming from localhost. Connections made to Linux will be passed to the 32U4 processor for parsing and controlling the pins. This happens on port 5555. Start the server with server.begin().

server.listenOnLocalhost();
  server.begin();
}
[Get Code]
In loop(), you'll create an instance of the YunClient for managing the connection. If the client connects, process the requests in a custom function (described below) and close the connection when finished.

Putting a delay at the end of loop() will be helpful in keeping the processor from doing too much work.

void loop() {
  YunClient client = server.accept();

  if (client) {
    process(client);
    client.stop();
  }

  delay(50); 
}
[Get Code]
Create a function named process that accepts the YunClient as its argument. Read the command by creating a string to hold the incoming information. Parse the REST commands by their functionality (digital, analog, and mode) and pass the information to the appropriately named function.

void process(YunClient client) {
  String command = client.readStringUntil('/');

  if (command == "digital") {
    digitalCommand(client);
  }
  if (command == "analog") {
    analogCommand(client);
  }
  if (command == "mode") {
    modeCommand(client);
  }
}
[Get Code]
Create a function to deal with digital commands. Accept the client as the argument. Create some local variables to hold the pin and value of the command.

void digitalCommand(YunClient client) {
  int pin, value;
[Get Code]
Parse the client's request for the pin to work with using client.parseInt().

If the character after the pin is a "/", it means the URL is going to have a value of 1 or 0 following. This value will assign a value to the pin, turning it HIGH or LOW. If there is no trailing "/", read the value from the specified pin.

pin = client.parseInt();

  if (client.read() == '/') {
    value = client.parseInt();
    digitalWrite(pin, value);
  } 
  else {This example for the Arduino Yún shows how to use the Bridge library to access the digital and analog pins on the board through REST calls. It demonstrates how you can create your own API when using REST style calls through the browser.

When running this example, make sure your computer is on the same network as the Yún. When you have have programmed the board, you can request the value on a pin, write a value to a pin, and configure a pin as an input or output.

When the REST password is turned off, you can use a browser with the following URL structure :

http://myArduinoYun.local/arduino/digital/13 : calls digitalRead(13);
http://myArduinoYun.local/arduino/digital/13/1 : calls digitalWrite(13,1);
http://myArduinoYun.local/arduino/analog/9/123 : analogWrite(9,123);
http://myArduinoYun.local/arduino/analog/2 : analogRead(2);
http://myArduinoYun.local/arduino/mode/13/input : pinMode(13, INPUT);
http://myArduinoYun.local/arduino/mode/13/output : pinMode(13, OUTPUT);
You can use the CURL command from the command line instead of a browser if you prefer.

Hardware Required

Arduino Yún
computer and Yún on the same wireless or wired network
Software Required

web browser
Circuit

There is no circuit for this example.


image developed using Fritzing. For more circuit examples, see the Fritzing project page

Code

The example code shows how it is possible to make REST requests to the Yún to read from and write information to the board's pins.

You need to include the Bridge, YunServer, and YunClient libraries :

#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>
[Get Code]
Instantiate a server enabling the the Yun to listen for connected clients.

YunServer server;

In setup(), start serial communication for debugging purposes, and turn the built-in LED on pin 13 high while Bridge begins. Bridge.begin() is blocking, and should take about 2 seconds to complete. Once Bridge starts up, turn the LED off.

void setup() {
  Serial.begin(9600);
  pinMode(13,OUTPUT);
  digitalWrite(13, LOW);
  Bridge.begin();
  digitalWrite(13, HIGH);
[Get Code]
In the second part of setup(), tell the instance of YunServer to listen for incoming connections only coming from localhost. Connections made to Linux will be passed to the 32U4 processor for parsing and controlling the pins. This happens on port 5555. Start the server with server.begin().

server.listenOnLocalhost();
  server.begin();
}
[Get Code]
In loop(), you'll create an instance of the YunClient for managing the connection. If the client connects, process the requests in a custom function (described below) and close the connection when finished.

Putting a delay at the end of loop() will be helpful in keeping the processor from doing too much work.

void loop() {
  YunClient client = server.accept();

  if (client) {
    process(client);
    client.stop();
  }

  delay(50); 
}
[Get Code]
Create a function named process that accepts the YunClient as its argument. Read the command by creating a string to hold the incoming information. Parse the REST commands by their functionality (digital, analog, and mode) and pass the information to the appropriately named function.

void process(YunClient client) {
  String command = client.readStringUntil('/');

  if (command == "digital") {
    digitalCommand(client);
  }
  if (command == "analog") {
    analogCommand(client);
  }
  if (command == "mode") {
    modeCommand(client);
  }
}
[Get Code]
Create a function to deal with digital commands. Accept the client as the argument. Create some local variables to hold the pin and value of the command.

void digitalCommand(YunClient client) {
  int pin, value;
[Get Code]
Parse the client's request for the pin to work with using client.parseInt().

If the character after the pin is a "/", it means the URL is going to have a value of 1 or 0 following. This value will assign a value to the pin, turning it HIGH or LOW. If there is no trailing "/", read the value from the specified pin.

pin = client.parseInt();

  if (client.read() == '/') {
    value = client.parseInt();
    digitalWrite(pin, value);
  } 
  else {
    value = digitalRead(pin);
  }
[Get Code]
Print the value to the client aThis example for the Arduino Yún shows how to use the Bridge library to access the digital and analog pins on the board through REST calls. It demonstrates how you can create your own API when using REST style calls through the browser.

When running this example, make sure your computer is on the same network as the Yún. When you have have programmed the board, you can request the value on a pin, write a value to a pin, and configure a pin as an input or output.

When the REST password is turned off, you can use a browser with the following URL structure :

http://myArduinoYun.local/arduino/digital/13 : calls digitalRead(13);
http://myArduinoYun.local/arduino/digital/13/1 : calls digitalWrite(13,1);
http://myArduinoYun.local/arduino/analog/9/123 : analogWrite(9,123);
http://myArduinoYun.local/arduino/analog/2 : analogRead(2);
http://myArduinoYun.local/arduino/mode/13/input : pinMode(13, INPUT);
http://myArduinoYun.local/arduino/mode/13/output : pinMode(13, OUTPUT);
You can use the CURL command from the command line instead of a browser if you prefer.

Hardware Required

Arduino Yún
computer and Yún on the same wireless or wired network
Software Required

web browser
Circuit

There is no circuit for this example.


image developed using Fritzing. For more circuit examples, see the Fritzing project page

Code

The example code shows how it is possible to make REST requests to the Yún to read from and write information to the board's pins.

You need to include the Bridge, YunServer, and YunClient libraries :

#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>
[Get Code]
Instantiate a server enabling the the Yun to listen for connected clients.

YunServer server;

In setup(), start serial communication for debugging purposes, and turn the built-in LED on pin 13 high while Bridge begins. Bridge.begin() is blocking, and should take about 2 seconds to complete. Once Bridge starts up, turn the LED off.

void setup() {
  Serial.begin(9600);
  pinMode(13,OUTPUT);
  digitalWrite(13, LOW);
  Bridge.begin();
  digitalWrite(13, HIGH);
[Get Code]
In the second part of setup(), tell the instance of YunServer to listen for incoming connections only coming from localhost. Connections made to Linux will be passed to the 32U4 processor for parsing and controlling the pins. This happens on port 5555. Start the server with server.begin().

server.listenOnLocalhost();
  server.begin();
}
[Get Code]
In loop(), you'll create an instance of the YunClient for managing the connection. If the client connects, process the requests in a custom function (described below) and close the connection when finished.

Putting a delay at the end of loop() will be helpful in keeping the processor from doing too much work.

void loop() {
  YunClient client = server.accept();

  if (client) {
    process(client);
    client.stop();
  }

  delay(50); 
}
[Get Code]
Create a function named process that accepts the YunClient as its argument. Read the command by creating a string to hold the incoming information. Parse the REST commands by their functionality (digital, analog, and mode) and pass the information to the appropriately named function.

void process(YunClient client) {
  String command = client.readStringUntil('/');

  if (command == "digital") {
    digitalCommand(client);
  }
  if (command == "analog") {
    analogCommand(client);
  }
  if (command == "mode") {
    modeCommand(client);
  }
}
[Get Code]
Create a function to deal with digital commands. Accept the client as the argument. Create some local variables to hold the pin and value of the command.

void digitalCommand(YunClient client) {
  int pin, value;
[Get Code]
Parse the client's request for the pin to work with using client.parseInt().

If the character after the pin is a "/", it means the URL is going to have a value of 1 or 0 following. This value will assign a value to the pin, turning it HIGH or LOW. If there is no trailing "/", read the value from the specified pin.

pin = client.parseInt();

  if (client.read() == '/') {
    value = client.parseInt();
    digitalWrite(pin, value);
  } 
  else {
    value = digitalRead(pin);
  }
[Get Code]
Print the value to the client and update the datastore key with the current pin value.

By wrapping the value to the client in F(), you'll be printing form the flash memory. This helps conserve space in SRAM, which is useful when dealing with long strings like URLs.

The key will be the pin, and type. For example D2 will be saved for for digital pin 2. The value will be whatever value the pin is currently set to, or was read from the pin.

client.print(F("Pin D"));
  client.print(pin);nd update the datastore key with the current pin value.

By wrapping the value to the client in F(), you'll be printing form the flash memory. This helps conserve space in SRAM, which is useful when dealing with long strings like URLs.

The key will be the pin, and type. For example D2 will be saved for for digital pin 2. The value will be whatever value the pin is currently set to, or was read from the pin.

client.print(F("Pin D"));
  client.print(pin);
    value = digitalRead(pin);
  }
[Get Code]
Print the value to the client and update the datastore key with the current pin value.

By wrapping the value to the client in F(), you'll be printing form the flash memory. This helps conserve space in SRAM, which is useful when dealing with long strings like URLs.

The key will be the pin, and type. For example D2 will be saved for for digital pin 2. The value will be whatever value the pin is currently set to, or was read from the pin.

client.print(F("Pin D"));
  client.print(pin); == '/') {
    value = client.parseInt();
    digitalWrite(pin, value);
  } 
  else {
    value = digitalRead(pin);
  }
[Get Code]
Print the value to the client and update the datastore key with the current pin value.

By wrapping the value to the client in F(), you'll be printing form the flash memory. This helps conserve space in SRAM, which is useful when dealing with long strings like URLs.

The key will be the pin, and type. For example D2 will be saved for for digital pin 2. The value will be whatever value the pin is currently set to, or was read from the pin.

client.print(F("Pin D"));
  client.print(pin);
If the character after the pin is a "/", it means the URL is going to have a value of 1 or 0 following. This value will assign a value to the pin, turning it HIGH or LOW. If there is no trailing "/", read the value from the specified pin.

pin = client.parseInt();

  if (client.read() == '/') {
    value = client.parseInt();
    digitalWrite(pin, value);
  } 
  else {
    value = digitalRead(pin);
  }
[Get Code]# Arduino-Blinds
Adding to the school sensor
This example for the Arduino Yún shows how to use the Bridge library to access the digital and analog pins on the board through REST calls. It demonstrates how you can create your own API when using REST style calls through the browser.

When running this example, make sure your computer is on the same network as the Yún. When you have have programmed the board, you can request the value on a pin, write a value to a pin, and configure a pin as an input or output.

When the REST password is turned off, you can use a browser with the following URL structure :

http://myArduinoYun.local/arduino/digital/13 : calls digitalRead(13);
http://myArduinoYun.local/arduino/digital/13/1 : calls digitalWrite(13,1);
http://myArduinoYun.local/arduino/analog/9/123 : analogWrite(9,123);
http://myArduinoYun.local/arduino/analog/2 : analogRead(2);
http://myArduinoYun.local/arduino/mode/13/input : pinMode(13, INPUT);
http://myArduinoYun.local/arduino/mode/13/output : pinMode(13, OUTPUT);
You can use the CURL command from the command line instead of a browser if you prefer.

Hardware Required

Arduino Yún
computer and Yún on the same wireless or wired network
Software Required

web browser
Circuit

There is no circuit for this example.


image developed using Fritzing. For more circuit examples, see the Fritzing project page

Code

The example code shows how it is possible to make REST requests to the Yún to read from and write information to the board's pins.

You need to include the Bridge, YunServer, and YunClient libraries :

#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>
[Get Code]
Instantiate a server enabling the the Yun to listen for connected clients.

YunServer server;

In setup(), start serial communication for debugging purposes, and turn the built-in LED on pin 13 high while Bridge begins. Bridge.begin() is blocking, and should take about 2 seconds to complete. Once Bridge starts up, turn the LED off.

void setup() {
  Serial.begin(9600);
  pinMode(13,OUTPUT);
  digitalWrite(13, LOW);
  Bridge.begin();
  digitalWrite(13, HIGH);
[Get Code]
In the second part of setup(), tell the instance of YunServer to listen for incoming connections only coming from localhost. Connections made to Linux will be passed to the 32U4 processor for parsing and controlling the pins. This happens on port 5555. Start the server with server.begin().

server.listenOnLocalhost();
  server.begin();
}
[Get Code]
In loop(), you'll create an instance of the YunClient for managing the connection. If the client connects, process the requests in a custom function (described below) and close the connection when finished.

Putting a delay at the end of loop() will be helpful in keeping the processor from doing too much work.

void loop() {
  YunClient client = server.accept();

  if (client) {
    process(client);
    client.stop();
  }

  delay(50); 
}
[Get Code]
Create a function named process that accepts the YunClient as its argument. Read the command by creating a string to hold the incoming information. Parse the REST commands by their functionality (digital, analog, and mode) and pass the information to the appropriately named function.

void process(YunClient client) {
  String command = client.readStringUntil('/');

  if (command == "digital") {
    digitalCommand(client);
  }
  if (command == "analog") {
    analogCommand(client);
  }
  if (command == "mode") {
    modeCommand(client);
  }
}
[Get Code]
Create a function to deal with digital commands. Accept the client as the argument. Create some local variables to hold the pin and value of the command.

void digitalCommand(YunClient client) {
  int pin, value;
[Get Code]
Parse the client's request for the pin to work with using client.parseInt().
This example for the Arduino Yún shows how to use the Bridge library to access the digital and analog pins on the board through REST calls. It demonstrates how you can create your own API when using REST style calls through the browser.

When running this example, make sure your computer is on the same network as the Yún. When you have have programmed the board, you can request the value on a pin, write a value to a pin, and configure a pin as an input or output.

When the REST password is turned off, you can use a browser with the following URL structure :

http://myArduinoYun.local/arduino/digital/13 : calls digitalRead(13);
http://myArduinoYun.local/arduino/digital/13/1 : calls digitalWrite(13,1);
http://myArduinoYun.local/arduino/analog/9/123 : analogWrite(9,123);
http://myArduinoYun.local/arduino/analog/2 : analogRead(2);
http://myArduinoYun.local/arduino/mode/13/input : pinMode(13, INPUT);
http://myArduinoYun.local/arduino/mode/13/output : pinMode(13, OUTPUT);
You can use the CURL command from the command line instead of a browser if you prefer.

Hardware Required

Arduino Yún
computer and Yún on the same wireless or wired network
Software Required

web browser
Circuit

There is no circuit for this example.


image developed using Fritzing. For more circuit examples, see the Fritzing project page

Code

The example code shows how it is possible to make REST requests to the Yún to read from and write information to the board's pins.

You need to include the Bridge, YunServer, and YunClient libraries :

#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>
[Get Code]
Instantiate a server enabling the the Yun to listen for connected clients.

YunServer server;

In setup(), start serial communication for debugging purposes, and turn the built-in LED on pin 13 high while Bridge begins. Bridge.begin() is blocking, and should take about 2 seconds to complete. Once Bridge starts up, turn the LED off.

void setup() {
  Serial.begin(9600);
  pinMode(13,OUTPUT);
  digitalWrite(13, LOW);
  Bridge.begin();
  digitalWrite(13, HIGH);
[Get Code]
In the second part of setup(), tell the instance of YunServer to listen for incoming connections only coming from localhost. Connections made to Linux will be passed to the 32U4 processor for parsing and controlling the pins. This happens on port 5555. Start the server with server.begin().

server.listenOnLocalhost();
  server.begin();
}
[Get Code]
In loop(), you'll create an instance of the YunClient for managing the connection. If the client connects, process the requests in a custom function (described below) and close the connection when finished.

Putting a delay at the end of loop() will be helpful in keeping the processor from doing too much work.

void loop() {
  YunClient client = server.accept();

  if (client) {
    process(client);
    client.stop();
  }

  delay(50); 
}
[Get Code]
Create a function named process that accepts the YunClient as its argument. Read the command by creating a string to hold the incoming information. Parse the REST commands by their functionality (digital, analog, and mode) and pass the information to the appropriately named function.

void process(YunClient client) {
  String command = client.readStringUntil('/');

  if (command == "digital") {
    digitalCommand(client);
  }
  if (command == "analog") {
    analogCommand(client);
  }
  if (command == "mode") {
    modeCommand(client);
  }
}
[Get Code]
Create a function to deal with digital commands. Accept the client as the argument. Create some local variables to hold the pin and value of the command.

void digitalCommand(YunClient client) {
  int pin, value;
[Get Code]
Parse the client's request for the pin to work with using client.parseInt().

If the character after the pin is a "/", it means the URL is going to have a value of 1 or 0 following. This value will assign a value to the pin, turning it HIGH or LOW. If there is no trailing "/", read the value from the specified pin.

pin = client.parseInt();

  if (client.read()This example for the Arduino Yún shows how to use the Bridge library to access the digital and analog pins on the board through REST calls. It demonstrates how you can create your own API when using REST style calls through the browser.

When running this example, make sure your computer is on the same network as the Yún. When you have have programmed the board, you can request the value on a pin, write a value to a pin, and configure a pin as an input or output.

When the REST password is turned off, you can use a browser with the following URL structure :

http://myArduinoYun.local/arduino/digital/13 : calls digitalRead(13);
http://myArduinoYun.local/arduino/digital/13/1 : calls digitalWrite(13,1);
http://myArduinoYun.local/arduino/analog/9/123 : analogWrite(9,123);
http://myArduinoYun.local/arduino/analog/2 : analogRead(2);
http://myArduinoYun.local/arduino/mode/13/input : pinMode(13, INPUT);
http://myArduinoYun.local/arduino/mode/13/output : pinMode(13, OUTPUT);
You can use the CURL command from the command line instead of a browser if you prefer.

Hardware Required

Arduino Yún
computer and Yún on the same wireless or wired network
Software Required

web browser
Circuit

There is no circuit for this example.


image developed using Fritzing. For more circuit examples, see the Fritzing project page

Code

The example code shows how it is possible to make REST requests to the Yún to read from and write information to the board's pins.

You need to include the Bridge, YunServer, and YunClient libraries :

#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>
[Get Code]
Instantiate a server enabling the the Yun to listen for connected clients.

YunServer server;

In setup(), start serial communication for debugging purposes, and turn the built-in LED on pin 13 high while Bridge begins. Bridge.begin() is blocking, and should take about 2 seconds to complete. Once Bridge starts up, turn the LED off.

void setup() {
  Serial.begin(9600);
  pinMode(13,OUTPUT);
  digitalWrite(13, LOW);
  Bridge.begin();
  digitalWrite(13, HIGH);
[Get Code]
In the second part of setup(), tell the instance of YunServer to listen for incoming connections only coming from localhost. Connections made to Linux will be passed to the 32U4 processor for parsing and controlling the pins. This happens on port 5555. Start the server with server.begin().

server.listenOnLocalhost();
  server.begin();
}
[Get Code]
In loop(), you'll create an instance of the YunClient for managing the connection. If the client connects, process the requests in a custom function (described below) and close the connection when finished.

Putting a delay at the end of loop() will be helpful in keeping the processor from doing too much work.

void loop() {
  YunClient client = server.accept();

  if (client) {
    process(client);
    client.stop();
  }

  delay(50); 
}
[Get Code]
Create a function named process that accepts the YunClient as its argument. Read the command by creating a string to hold the incoming information. Parse the REST commands by their functionality (digital, analog, and mode) and pass the information to the appropriately named function.

void process(YunClient client) {
  String command = client.readStringUntil('/');

  if (command == "digital") {
    digitalCommand(client);
  }
  if (command == "analog") {
    analogCommand(client);
  }
  if (command == "mode") {
    modeCommand(client);
  }
}
[Get Code]
Create a function to deal with digital commands. Accept the client as the argument. Create some local variables to hold the pin and value of the command.

void digitalCommand(YunClient client) {
  int pin, value;
[Get Code]
Parse the client's request for the pin to work with using client.parseInt().

If the character after the pin is a "/", it means the URL is going to have a value of 1 or 0 following. This value will assign a value to the pin, turning it HIGH or LOW. If there is no trailing "/", read the value from the specified pin.

pin = client.parseInt();

  if (client.read() == '/') {
    value = client.parseInt();
    digitalWrite(pin, value);
  } 
  else {This example for the Arduino Yún shows how to use the Bridge library to access the digital and analog pins on the board through REST calls. It demonstrates how you can create your own API when using REST style calls through the browser.

When running this example, make sure your computer is on the same network as the Yún. When you have have programmed the board, you can request the value on a pin, write a value to a pin, and configure a pin as an input or output.

When the REST password is turned off, you can use a browser with the following URL structure :

http://myArduinoYun.local/arduino/digital/13 : calls digitalRead(13);
http://myArduinoYun.local/arduino/digital/13/1 : calls digitalWrite(13,1);
http://myArduinoYun.local/arduino/analog/9/123 : analogWrite(9,123);
http://myArduinoYun.local/arduino/analog/2 : analogRead(2);
http://myArduinoYun.local/arduino/mode/13/input : pinMode(13, INPUT);
http://myArduinoYun.local/arduino/mode/13/output : pinMode(13, OUTPUT);
You can use the CURL command from the command line instead of a browser if you prefer.

Hardware Required

Arduino Yún
computer and Yún on the same wireless or wired network
Software Required

web browser
Circuit

There is no circuit for this example.


image developed using Fritzing. For more circuit examples, see the Fritzing project page

Code

The example code shows how it is possible to make REST requests to the Yún to read from and write information to the board's pins.

You need to include the Bridge, YunServer, and YunClient libraries :

#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>
[Get Code]
Instantiate a server enabling the the Yun to listen for connected clients.

YunServer server;

In setup(), start serial communication for debugging purposes, and turn the built-in LED on pin 13 high while Bridge begins. Bridge.begin() is blocking, and should take about 2 seconds to complete. Once Bridge starts up, turn the LED off.

void setup() {
  Serial.begin(9600);
  pinMode(13,OUTPUT);
  digitalWrite(13, LOW);
  Bridge.begin();
  digitalWrite(13, HIGH);
[Get Code]
In the second part of setup(), tell the instance of YunServer to listen for incoming connections only coming from localhost. Connections made to Linux will be passed to the 32U4 processor for parsing and controlling the pins. This happens on port 5555. Start the server with server.begin().

server.listenOnLocalhost();
  server.begin();
}
[Get Code]
In loop(), you'll create an instance of the YunClient for managing the connection. If the client connects, process the requests in a custom function (described below) and close the connection when finished.

Putting a delay at the end of loop() will be helpful in keeping the processor from doing too much work.

void loop() {
  YunClient client = server.accept();

  if (client) {
    process(client);
    client.stop();
  }

  delay(50); 
}
[Get Code]
Create a function named process that accepts the YunClient as its argument. Read the command by creating a string to hold the incoming information. Parse the REST commands by their functionality (digital, analog, and mode) and pass the information to the appropriately named function.

void process(YunClient client) {
  String command = client.readStringUntil('/');

  if (command == "digital") {
    digitalCommand(client);
  }
  if (command == "analog") {
    analogCommand(client);
  }
  if (command == "mode") {
    modeCommand(client);
  }
}
[Get Code]
Create a function to deal with digital commands. Accept the client as the argument. Create some local variables to hold the pin and value of the command.

void digitalCommand(YunClient client) {
  int pin, value;
[Get Code]
Parse the client's request for the pin to work with using client.parseInt().

If the character after the pin is a "/", it means the URL is going to have a value of 1 or 0 following. This value will assign a value to the pin, turning it HIGH or LOW. If there is no trailing "/", read the value from the specified pin.

pin = client.parseInt();

  if (client.read() == '/') {
    value = client.parseInt();
    digitalWrite(pin, value);
  } 
  else {
    value = digitalRead(pin);
  }
[Get Code]
Print the value to the client aThis example for the Arduino Yún shows how to use the Bridge library to access the digital and analog pins on the board through REST calls. It demonstrates how you can create your own API when using REST style calls through the browser.

When running this example, make sure your computer is on the same network as the Yún. When you have have programmed the board, you can request the value on a pin, write a value to a pin, and configure a pin as an input or output.

When the REST password is turned off, you can use a browser with the following URL structure :

http://myArduinoYun.local/arduino/digital/13 : calls digitalRead(13);
http://myArduinoYun.local/arduino/digital/13/1 : calls digitalWrite(13,1);
http://myArduinoYun.local/arduino/analog/9/123 : analogWrite(9,123);
http://myArduinoYun.local/arduino/analog/2 : analogRead(2);
http://myArduinoYun.local/arduino/mode/13/input : pinMode(13, INPUT);
http://myArduinoYun.local/arduino/mode/13/output : pinMode(13, OUTPUT);
You can use the CURL command from the command line instead of a browser if you prefer.

Hardware Required

Arduino Yún
computer and Yún on the same wireless or wired network
Software Required

web browser
Circuit

There is no circuit for this example.


image developed using Fritzing. For more circuit examples, see the Fritzing project page

Code

The example code shows how it is possible to make REST requests to the Yún to read from and write information to the board's pins.

You need to include the Bridge, YunServer, and YunClient libraries :

#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>
[Get Code]
Instantiate a server enabling the the Yun to listen for connected clients.

YunServer server;

In setup(), start serial communication for debugging purposes, and turn the built-in LED on pin 13 high while Bridge begins. Bridge.begin() is blocking, and should take about 2 seconds to complete. Once Bridge starts up, turn the LED off.

void setup() {
  Serial.begin(9600);
  pinMode(13,OUTPUT);
  digitalWrite(13, LOW);
  Bridge.begin();
  digitalWrite(13, HIGH);
[Get Code]
In the second part of setup(), tell the instance of YunServer to listen for incoming connections only coming from localhost. Connections made to Linux will be passed to the 32U4 processor for parsing and controlling the pins. This happens on port 5555. Start the server with server.begin().

server.listenOnLocalhost();
  server.begin();
}
[Get Code]
In loop(), you'll create an instance of the YunClient for managing the connection. If the client connects, process the requests in a custom function (described below) and close the connection when finished.

Putting a delay at the end of loop() will be helpful in keeping the processor from doing too much work.

void loop() {
  YunClient client = server.accept();

  if (client) {
    process(client);
    client.stop();
  }

  delay(50); 
}
[Get Code]
Create a function named process that accepts the YunClient as its argument. Read the command by creating a string to hold the incoming information. Parse the REST commands by their functionality (digital, analog, and mode) and pass the information to the appropriately named function.

void process(YunClient client) {
  String command = client.readStringUntil('/');

  if (command == "digital") {
    digitalCommand(client);
  }
  if (command == "analog") {
    analogCommand(client);
  }
  if (command == "mode") {
    modeCommand(client);
  }
}
[Get Code]
Create a function to deal with digital commands. Accept the client as the argument. Create some local variables to hold the pin and value of the command.

void digitalCommand(YunClient client) {
  int pin, value;
[Get Code]
Parse the client's request for the pin to work with using client.parseInt().

If the character after the pin is a "/", it means the URL is going to have a value of 1 or 0 following. This value will assign a value to the pin, turning it HIGH or LOW. If there is no trailing "/", read the value from the specified pin.

pin = client.parseInt();

  if (client.read() == '/') {
    value = client.parseInt();
    digitalWrite(pin, value);
  } 
  else {
    value = digitalRead(pin);
  }
[Get Code]
Print the value to the client and update the datastore key with the current pin value.

By wrapping the value to the client in F(), you'll be printing form the flash memory. This helps conserve space in SRAM, which is useful when dealing with long strings like URLs.

The key will be the pin, and type. For example D2 will be saved for for digital pin 2. The value will be whatever value the pin is currently set to, or was read from the pin.

client.print(F("Pin D"));
  client.print(pin);nd update the datastore key with the current pin value.

By wrapping the value to the client in F(), you'll be printing form the flash memory. This helps conserve space in SRAM, which is useful when dealing with long strings like URLs.

The key will be the pin, and type. For example D2 will be saved for for digital pin 2. The value will be whatever value the pin is currently set to, or was read from the pin.

client.print(F("Pin D"));
  client.print(pin);
    value = digitalRead(pin);
  }
[Get Code]
Print the value to the client and update the datastore key with the current pin value.

By wrapping the value to the client in F(), you'll be printing form the flash memory. This helps conserve space in SRAM, which is useful when dealing with long strings like URLs.

The key will be the pin, and type. For example D2 will be saved for for digital pin 2. The value will be whatever value the pin is currently set to, or was read from the pin.

client.print(F("Pin D"));
  client.print(pin); == '/') {
    value = client.parseInt();
    digitalWrite(pin, value);
  } 
  else {
    value = digitalRead(pin);
  }
[Get Code]
Print the value to the client and update the datastore key with the current pin value.

By wrapping the value to the client in F(), you'll be printing form the flash memory. This helps conserve space in SRAM, which is useful when dealing with long strings like URLs.

The key will be the pin, and type. For example D2 will be saved for for digital pin 2. The value will be whatever value the pin is currently set to, or was read from the pin.

client.print(F("Pin D"));
  client.print(pin);
If the character after the pin is a "/", it means the URL is going to have a value of 1 or 0 following. This value will assign a value to the pin, turning it HIGH or LOW. If there is no trailing "/", read the value from the specified pin.

pin = client.parseInt();

  if (client.read() == '/') {
    value = client.parseInt();
    digitalWrite(pin, value);
  } 
  else {
    value = digitalRead(pin);
  }
[Get Code]
Print the value to the client and update the datastore key with the current pin value.

By wrapping the value to the client in F(), you'll be printing form the flash memory. This helps conserve space in SRAM, which is useful when dealing with long strings like URLs.

The key will be the pin, and type. For example D2 will be saved for for digital pin 2. The value will be whatever value the pin is currently set to, or was read from the pin.

client.print(F("Pin D"));
  client.print(pin);
Print the value to the client and update the datastore key with the current pin value.

By wrapping the value to the client in F(), you'll be printing form the flash memory. This helps conserve space in SRAM, which is useful when dealing with long strings like URLs.

The key will be the pin, and type. For example D2 will be saved for for digital pin 2. The value will be whatever value the pin is currently set to, or was read from the pin.

client.print(F("Pin D"));
  client.print(pin);
