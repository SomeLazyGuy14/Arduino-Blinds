# Arduino-Blinds
Adding to the school sensor

Blinking light Code:

void setup() {
  // put your setup code here, to run once:
pinMode(13, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
digitalWrite(13, HIGH);     //turns the led on
delay(1000);                //delay 1 second
digitalWrite(13, LOW);      //turns the led off
delay(1000);                //delay 1 second
}
