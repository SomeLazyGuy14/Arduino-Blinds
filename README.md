
 Code  Issues 0  Pull requests 0  Wiki  Pulse  Graphs
Branch: master Find file Copy pathArduino-Blinds/Joystick x & y axis Code
2c2d018  19 minutes ago
@JeffreyAlfonso JeffreyAlfonso Rename Joystick x & y axis to Joystick x & y axis Code
1 contributor
RawBlameHistory     25 lines (21 sloc)  596 Bytes
// Pin Numbers!

const int VRx_pin = 0; // Analog pin A0 connected X to output
const int VRy_pin = 1; // Analog pin A1 connected Y to output
const int SW_pin = 2; // Analog pin A0 connected X to output

void setup () {
 pinMode(SW_pin, INPUT);
 digitalWrite(SW_pin, HIGH);
 Serial.begin(115200);
}
 Code  Issues 0  Pull requests 0  Wiki  Pulse  Graphs
Branch: master Find file Copy pathArduino-Blinds/Joystick x & y axis Code
2c2d018  19 minutes ago
@JeffreyAlfonso JeffreyAlfonso Rename Joystick x & y axis to Joystick x & y axis Code
1 contributor
RawBlameHistory     25 lines (21 sloc)  596 Bytes
// Pin Numbers!

const int VRx_pin = 0; // Analog pin A0 connected X to output
const int VRy_pin = 1; // Analog pin A1 connected Y to output
const int SW_pin = 2; // Analog pin A0 connected X to output

void setup () {
 pinMode(SW_pin, INPUT);
 digitalWrite(SW_pin, HIGH);
 Serial.begin(115200);
}

void loop () {
 Code  Issues 0  Pull requests 0  Wiki  Pulse  Graphs
Branch: master Find file Copy pathArduino-Blinds/Joystick x & y axis Code
2c2d018  19 minutes ago
@JeffreyAlfonso JeffreyAlfonso Rename Joystick x & y axis to Joystick x & y axis Code
1 contributor
RawBlameHistory     25 lines (21 sloc)  596 Bytes
// Pin Numbers!

const int VRx_pin = 0; // Analog pin A0 connected X to output
const int VRy_pin = 1; // Analog pin A1 connected Y to output
const int SW_pin = 2; // Analog pin A0 connected X to output

void setup () {
 pinMode(SW_pin, INPUT);
 digitalWrite(SW_pin, HIGH);
 Serial.begin(115200);
}

void loop () {
  Serial.print("Switch: ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
  Serial.print(analogRead(VRx_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println (analogRead(VRy_pin));
  Serial.print("\n\n");
  delay(500);
}
Status API Training Shop Blog About Pricing
© 2016 GitHub, Inc. Terms Privacy Security Contact Help
  Serial.print("Switch: ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
  Serial.print(analogRead(VRx_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println (analogRead(VRy_pin));
  Serial.print("\n\n");
  delay(500);
}
Status API Training Shop Blog About Pricing
© 2016 GitHub, Inc. Terms Privacy Security Contact Help

void loop () {
  Serial.print("Switch: ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
 Code  Issues 0  Pull requests 0  Wiki  Pulse  Graphs
Branch: master Find file Copy pathArduino-Blinds/Joystick x & y axis Code
2c2d018  19 minutes ago
@JeffreyAlfonso JeffreyAlfonso Rename Joystick x & y axis to Joystick x & y axis Code
1 contributor
RawBlameHistory     25 lines (21 sloc)  596 Bytes
// Pin Numbers!

const int VRx_pin = 0; // Analog pin A0 connected X to output
const int VRy_pin = 1; // Analog pin A1 connected Y to output
const int SW_pin = 2; // Analog pin A0 connected X to output

void setup () {
 pinMode(SW_pin, INPUT);
 digitalWrite(SW_pin, HIGH);
 Serial.begin(115200);
}
 Code  Issues 0  Pull requests 0  Wiki  Pulse  Graphs
Branch: master Find file Copy pathArduino-Blinds/Joystick x & y axis Code
2c2d018  19 minutes ago
@JeffreyAlfonso JeffreyAlfonso Rename Joystick x & y axis to Joystick x & y axis Code
1 contributor
RawBlameHistory     25 lines (21 sloc)  596 Bytes
// Pin Numbers!

const int VRx_pin = 0; // Analog pin A0 connected X to output
const int VRy_pin = 1; // Analog pin A1 connected Y to output
const int SW_pin = 2; // Analog pin A0 connected X to output

void setup () {
 pinMode(SW_pin, INPUT);
 digitalWrite(SW_pin, HIGH);
 Serial.begin(115200);
}

void loop () {
 Code  Issues 0  Pull requests 0  Wiki  Pulse  Graphs
Branch: master Find file Copy pathArduino-Blinds/Joystick x & y axis Code
2c2d018  19 minutes ago
@JeffreyAlfonso JeffreyAlfonso Rename Joystick x & y axis to Joystick x & y axis Code
1 contributor
RawBlameHistory     25 lines (21 sloc)  596 Bytes
// Pin Numbers!

const int VRx_pin = 0; // Analog pin A0 connected X to output
const int VRy_pin = 1; // Analog pin A1 connected Y to output
const int SW_pin = 2; // Analog pin A0 connected X to output

void setup () {
 pinMode(SW_pin, INPUT);
 digitalWrite(SW_pin, HIGH);
 Serial.begin(115200);
}

void loop () {
  Serial.print("Switch: ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
  Serial.print(analogRead(VRx_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println (analogRead(VRy_pin));
  Serial.print("\n\n");
  delay(500);
}
Status API Training Shop Blog About Pricing
© 2016 GitHub, Inc. Terms Privacy Security Contact Help
  Serial.print("Switch: ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
  Serial.print(analogRead(VRx_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println (analogRead(VRy_pin));
  Serial.print("\n\n");
  delay(500);
}
Status API Training Shop Blog About Pricing
© 2016 GitHub, Inc. Terms Privacy Security Contact Help

void loop () {
  Serial.print("Switch: ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
  Serial.print(analogRead(VRx_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println (analogRead(VRy_pin));
  Serial.print("\n\n");
  delay(500);
}
Status API Training Shop Blog About Pricing
 Code  Issues 0  Pull requests 0  Wiki  Pulse  Graphs
Branch: master Find file Copy pathArduino-Blinds/Joystick x & y axis Code
2c2d018  19 minutes ago
@JeffreyAlfonso JeffreyAlfonso Rename Joystick x & y axis to Joystick x & y axis Code
1 contributor
RawBlameHistory     25 lines (21 sloc)  596 Bytes
// Pin Numbers!

const int VRx_pin = 0; // Analog pin A0 connected X to output
const int VRy_pin = 1; // Analog pin A1 connected Y to output
const int SW_pin = 2; // Analog pin A0 connected X to output

void setup () {
 pinMode(SW_pin, INPUT);
 digitalWrite(SW_pin, HIGH);
 Serial.begin(115200);
}
 Code  Issues 0  Pull requests 0  Wiki  Pulse  Graphs
Branch: master Find file Copy pathArduino-Blinds/Joystick x & y axis Code
2c2d018  19 minutes ago
@JeffreyAlfonso JeffreyAlfonso Rename Joystick x & y axis to Joystick x & y axis Code
1 contributor
RawBlameHistory     25 lines (21 sloc)  596 Bytes
// Pin Numbers!

const int VRx_pin = 0; // Analog pin A0 connected X to output
const int VRy_pin = 1; // Analog pin A1 connected Y to output
const int SW_pin = 2; // Analog pin A0 connected X to output

void setup () {
 pinMode(SW_pin, INPUT);
 digitalWrite(SW_pin, HIGH);
 Serial.begin(115200);
}

void loop () {
 Code  Issues 0  Pull requests 0  Wiki  Pulse  Graphs
Branch: master Find file Copy pathArduino-Blinds/Joystick x & y axis Code
2c2d018  19 minutes ago
@JeffreyAlfonso JeffreyAlfonso Rename Joystick x & y axis to Joystick x & y axis Code
1 contributor
RawBlameHistory     25 lines (21 sloc)  596 Bytes
// Pin Numbers!

const int VRx_pin = 0; // Analog pin A0 connected X to output
const int VRy_pin = 1; // Analog pin A1 connected Y to output
const int SW_pin = 2; // Analog pin A0 connected X to output

void setup () {
 pinMode(SW_pin, INPUT);
 digitalWrite(SW_pin, HIGH);
 Serial.begin(115200);
}

void loop () {
  Serial.print("Switch: ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
  Serial.print(analogRead(VRx_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println (analogRead(VRy_pin));
  Serial.print("\n\n");
  delay(500);
}
Status API Training Shop Blog About Pricing
© 2016 GitHub, Inc. Terms Privacy Security Contact Help
  Serial.print("Switch: ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
  Serial.print(analogRead(VRx_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println (analogRead(VRy_pin));
  Serial.print("\n\n");
  delay(500);
}
Status API Training Shop Blog About Pricing
© 2016 GitHub, Inc. Terms Privacy Security Contact Help

void loop () {
  Serial.print("Switch: ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
 Code  Issues 0  Pull requests 0  Wiki  Pulse  Graphs
Branch: master Find file Copy pathArduino-Blinds/Joystick x & y axis Code
2c2d018  19 minutes ago
@JeffreyAlfonso JeffreyAlfonso Rename Joystick x & y axis to Joystick x & y axis Code
1 contributor
RawBlameHistory     25 lines (21 sloc)  596 Bytes
// Pin Numbers!

const int VRx_pin = 0; // Analog pin A0 connected X to output
const int VRy_pin = 1; // Analog pin A1 connected Y to output
const int SW_pin = 2; // Analog pin A0 connected X to output

void setup () {
 pinMode(SW_pin, INPUT);
 digitalWrite(SW_pin, HIGH);
 Serial.begin(115200);
}
 Code  Issues 0  Pull requests 0  Wiki  Pulse  Graphs
Branch: master Find file Copy pathArduino-Blinds/Joystick x & y axis Code
2c2d018  19 minutes ago
@JeffreyAlfonso JeffreyAlfonso Rename Joystick x & y axis to Joystick x & y axis Code
1 contributor
RawBlameHistory     25 lines (21 sloc)  596 Bytes
// Pin Numbers!

const int VRx_pin = 0; // Analog pin A0 connected X to output
const int VRy_pin = 1; // Analog pin A1 connected Y to output
const int SW_pin = 2; // Analog pin A0 connected X to output

void setup () {
 pinMode(SW_pin, INPUT);
 digitalWrite(SW_pin, HIGH);
 Serial.begin(115200);
}

void loop () {
 Code  Issues 0  Pull requests 0  Wiki  Pulse  Graphs
Branch: master Find file Copy pathArduino-Blinds/Joystick x & y axis Code
2c2d018  19 minutes ago
@JeffreyAlfonso JeffreyAlfonso Rename Joystick x & y axis to Joystick x & y axis Code
1 contributor
RawBlameHistory     25 lines (21 sloc)  596 Bytes
// Pin Numbers!

const int VRx_pin = 0; // Analog pin A0 connected X to output
const int VRy_pin = 1; // Analog pin A1 connected Y to output
const int SW_pin = 2; // Analog pin A0 connected X to output

void setup () {
 pinMode(SW_pin, INPUT);
 digitalWrite(SW_pin, HIGH);
 Serial.begin(115200);
}

void loop () {
  Serial.print("Switch: ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
  Serial.print(analogRead(VRx_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println (analogRead(VRy_pin));
  Serial.print("\n\n");
  delay(500);
}
Status API Training Shop Blog About Pricing
© 2016 GitHub, Inc. Terms Privacy Security Contact Help
  Serial.print("Switch: ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
  Serial.print(analogRead(VRx_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println (analogRead(VRy_pin));
  Serial.print("\n\n");
  delay(500);
}
Status API Training Shop Blog About Pricing
© 2016 GitHub, Inc. Terms Privacy Security Contact Help

void loop () {
  Serial.print("Switch: ");
  Serial.print(digitalRead(SW_pin));
  Serial.print("\n");
  Serial.print("X-axis: ");
  Serial.print(analogRead(VRx_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println (analogRead(VRy_pin));
  Serial.print("\n\n");
  delay(500);
}
Status API Training Shop Blog About Pricing
© 2016 GitHub, Inc. Terms Privacy Security Contact Help
  Serial.print(analogRead(VRx_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println (analogRead(VRy_pin));
  Serial.print("\n\n");
  delay(500);
}
Status API Training Shop Blog About Pricing
© 2016 GitHub, Inc. Terms Privacy Security Contact Help
© 2016 GitHub, Inc. Terms Privacy Security Contact Help
  Serial.print(analogRead(VRx_pin));
  Serial.print("\n");
  Serial.print("Y-axis: ");
  Serial.println (analogRead(VRy_pin));
  Serial.print("\n\n");
  delay(500);
}
Status API Training Shop Blog About Pricing
© 2016 GitHub, Inc. Terms Privacy Security Contact Help
