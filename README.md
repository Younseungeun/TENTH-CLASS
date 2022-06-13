# TENTH-CLASS

## TOPIC
- QUIZ(Turn on the LED when rotating)
![image](https://user-images.githubusercontent.com/102523600/173338536-289cad5e-7cad-485d-86cf-d4add40593e7.png)
### CODE
#include <SoftwareSerial.h> //
SoftwareSerial BTSerial(12, 13); //12-TX IMPORTANT!! TX of BTS serial is connected to RX of Serial, RX of BTS serial is connected to TX of Serial (RX is received, T of TX is transmit)
int motor1PinA = 2 ; //connect to pin2
int motor1PinB =3 ; //connect to pin3
int enableRPin= 11 ; // RIGHT, the motor 1 Pin is the motor on the right
int motor2PinA = 4 ; //connect to pin4
int motor2PinB =5; //connect to pin5
int enableLPin= 10 ; //left, the motor 2pin is the motor on the left
int RLED=8;
int LLED=7;
char in; //Specify a variable
void setup() {
pinMode(RLED, OUTPUT);
pinMode(LLED, OUTPUT);
pinMode(motor1PinA, OUTPUT); //use motor1PinA as an output (result)
pinMode(motor1PinB, OUTPUT); //use motor1PinB as an output (result)
pinMode(enableLPin, OUTPUT); //use enableLPin as output (result)
pinMode(motor2PinA, OUTPUT); //use motor2PinA as an output (result)
pinMode(motor2PinB, OUTPUT); //use motor2PinB as an output (result)
pinMode(enableRPin, OUTPUT) ; //use enableRPin as output (result)
analogWrite(enableRPin, 100);//set the speed of the motor(maximum is 255)
analogWrite(enableLPin, 100);//set the speed of the motor(maximum is 255)
Serial.begin(9600);
BTSerial.begin(9600); //Initialize Bluetooth data rate
}
void loop() {
if (BTSerial.available()) //if you receive data through Bluetooth,
Serial.write(BTSerial.read()); //send data from Bluetooth to the RX pin on the serial port, and output the received data to the PC serial window
if (Serial.available())//If you enter the data that came into the serial monitor window and send it,
BTSerial.write(Serial.read());// output data sent via Bluetooth to your smartphone
if (BTSerial.available())
{ in =BTSerial.read();
Serial.write(in);
}
if (Serial.available())
{ BTSerial.write(Serial.read());
Serial.print("data =");
Serial.println(in);
}
switch(in){
case 'F':Forward(); break;
case 'R': Right(); break;
case 'S': Stop(); break;
case 'L': Left(); break;
case 'B': Back(); break;
case 'G': FowardLeft(); break;
case 'I': FowardRight(); break;
case 'H': BackLeft(); break;
case 'J':BackRight();break;
}
}
void Forward(){ // FRONT
analogWrite(enableRPin, 255);
analogWrite(enableLPin, 255);
digitalWrite(motor1PinA, HIGH);
digitalWrite(motor1PinB,LOW);
digitalWrite(motor2PinA,HIGH);
digitalWrite(motor2PinB,LOW);
}
void Right(){ // RIGHT
digitalWrite(RLED, HIGH);
analogWrite(enableRPin, 255);
analogWrite(enableLPin, 255);
digitalWrite(motor1PinA, LOW);
digitalWrite(motor1PinB,LOW);
digitalWrite(motor2PinA,HIGH);
digitalWrite(motor2PinB,LOW);
}
void Left(){ // LEFT
  digitalWrite(LLED, HIGH);
analogWrite(enableRPin, 255);
analogWrite(enableLPin, 255);
digitalWrite(motor1PinA, HIGH);
digitalWrite(motor1PinB,LOW);
digitalWrite(motor2PinA,LOW);
digitalWrite(motor2PinB,LOW);
}
void Stop(){ // STOP
  digitalWrite(LLED, LOW);
  digitalWrite(RLED, LOW);
analogWrite(enableRPin, 255);
analogWrite(enableLPin, 255);
digitalWrite(motor1PinA, LOW);
digitalWrite(motor1PinB,LOW);
digitalWrite(motor2PinA,LOW);
digitalWrite(motor2PinB,LOW);
}
void Back(){ // BACK
analogWrite(enableRPin, 255);
analogWrite(enableLPin, 255);
digitalWrite(motor1PinA, LOW);
digitalWrite(motor1PinB,HIGH);
digitalWrite(motor2PinA,LOW);
digitalWrite(motor2PinB,HIGH);
}
void FowardRight(){ // RIGHT 45 ANGLE
analogWrite(enableRPin,100);
analogWrite(enableLPin, 255);
digitalWrite(motor1PinA, HIGH);
digitalWrite(motor1PinB,LOW);
digitalWrite(motor2PinA,HIGH);
digitalWrite(motor2PinB,LOW);
}
void FowardLeft(){ // LEFT 45 ANGLE
analogWrite(enableRPin, 255);
analogWrite(enableLPin, 100);
digitalWrite(motor1PinA, HIGH);
digitalWrite(motor1PinB,LOW);
digitalWrite(motor2PinA,HIGH);
digitalWrite(motor2PinB,LOW);
}
void BackLeft(){// LEFT BACK 45 ANGLE
analogWrite(enableRPin, 255);
analogWrite(enableLPin, 100);
digitalWrite(motor1PinA,LOW);
digitalWrite(motor1PinB,HIGH);
digitalWrite(motor2PinA,LOW);
digitalWrite(motor2PinB,HIGH);
}
void BackRight(){// RIGHT BACK 45 ANGLE
analogWrite(enableRPin,100);
analogWrite(enableLPin, 255);
digitalWrite(motor1PinA,LOW);
digitalWrite(motor1PinB,HIGH);
digitalWrite(motor2PinA,LOW);
digitalWrite(motor2PinB,HIGH);
}
