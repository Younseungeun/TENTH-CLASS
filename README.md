# TENTH-CLASS

## TOPIC
- QUIZ(Turn on the LED when rotating)
![image](https://user-images.githubusercontent.com/102523600/173338536-289cad5e-7cad-485d-86cf-d4add40593e7.png)
### CODE
1. #include <SoftwareSerial.h> //
2. SoftwareSerial BTSerial(12, 13); //12-TX IMPORTANT!! TX of BTS serial is connected to RX of Serial, RX of BTS serial is connected to TX of Serial (RX is received,
3. of TX is transmit)int motor1PinA = 2 ; //connect to pin2
4. int motor1PinB =3 ; //connect to pin3
5. int enableRPin= 11 ; // RIGHT, the motor 1 Pin is the motor on the right
6. int motor2PinA = 4 ; //connect to pin4
7. int motor2PinB =5; //connect to pin5
8. int enableLPin= 10 ; //left, the motor 2pin is the motor on the left
9. int RLED=8;
10. int LLED=7;
11. char in; //Specify a variable
12. void setup() {
13. pinMode(RLED, OUTPUT);
14. pinMode(LLED, OUTPUT);
15. pinMode(motor1PinA, OUTPUT); //use motor1PinA as an output (result)
16. pinMode(motor1PinB, OUTPUT); //use motor1PinB as an output (result)
17. pinMode(enableLPin, OUTPUT); //use enableLPin as output (result)
18. pinMode(motor2PinA, OUTPUT); //use motor2PinA as an output (result)
19. pinMode(motor2PinB, OUTPUT); //use motor2PinB as an output (result)
20. pinMode(enableRPin, OUTPUT) ; //use enableRPin as output (result)
21. analogWrite(enableRPin, 100);//set the speed of the motor(maximum is 255)
22. analogWrite(enableLPin, 100);//set the speed of the motor(maximum is 255)
23. Serial.begin(9600);
24. BTSerial.begin(9600); //Initialize Bluetooth data rate
25. }
26. void loop() {
27. if (BTSerial.available()) //if you receive data through Bluetooth,
28. Serial.write(BTSerial.read()); //send data from Bluetooth to the RX pin on the serial port, and output the received data to the PC serial window
29. if (Serial.available())//If you enter the data that came into the serial monitor window and send it,
30. BTSerial.write(Serial.read());// output data sent via Bluetooth to your smartphone
31. if (BTSerial.available())
32. { in =BTSerial.read();
33. Serial.write(in);
34. }
35. if (Serial.available())
36. { BTSerial.write(Serial.read());
37. Serial.print("data =");
38. Serial.println(in);
39. }
40. switch(in){
41. case 'F':Forward(); break;
42. case 'R': Right(); break;
43. case 'S': Stop(); break;
44. case 'L': Left(); break;
45. case 'B': Back(); break;
46. case 'G': FowardLeft(); break;
47. case 'I': FowardRight(); break;
48. case 'H': BackLeft(); break;
49. case 'J':BackRight();break;
50. }
51. }
52. void Forward(){ // FRONT
53. analogWrite(enableRPin, 255);
54. analogWrite(enableLPin, 255);
55. digitalWrite(motor1PinA, HIGH);
56. digitalWrite(motor1PinB,LOW);
57. digitalWrite(motor2PinA,HIGH);
58. digitalWrite(motor2PinB,LOW);
59. }
60. void Right(){ // RIGHT
61. digitalWrite(RLED, HIGH);
62. analogWrite(enableRPin, 255);
63. analogWrite(enableLPin, 255);
64. digitalWrite(motor1PinA, LOW);
65. digitalWrite(motor1PinB,LOW);
66. digitalWrite(motor2PinA,HIGH);
67. digitalWrite(motor2PinB,LOW);
68. }
69. void Left(){ // LEFT
70. digitalWrite(LLED, HIGH);
71. analogWrite(enableRPin, 255);
72. analogWrite(enableLPin, 255);]
73. digitalWrite(motor1PinA, HIGH);
74. digitalWrite(motor1PinB,LOW);
75. digitalWrite(motor2PinA,LOW);
76. digitalWrite(motor2PinB,LOW);
77. }
78. void Stop(){ // STOP
79. digitalWrite(LLED, LOW);
80. digitalWrite(RLED, LOW);
81. analogWrite(enableRPin, 255);
82. analogWrite(enableLPin, 255);
83. digitalWrite(motor1PinA, LOW);
84. digitalWrite(motor1PinB,LOW);
85. digitalWrite(motor2PinA,LOW);
86. digitalWrite(motor2PinB,LOW);
87. }
88. void Back(){ // BACK
89. analogWrite(enableRPin, 255);
90. analogWrite(enableLPin, 255);
91. digitalWrite(motor1PinA, LOW);
92. digitalWrite(motor1PinB,HIGH);
93. digitalWrite(motor2PinA,LOW);
94. digitalWrite(motor2PinB,HIGH);
95. }
96. void FowardRight(){ // RIGHT 45 ANGLE
97. analogWrite(enableRPin,100);
98. analogWrite(enableLPin, 255);
99. digitalWrite(motor1PinA, HIGH);
100. digitalWrite(motor1PinB,LOW);
101. digitalWrite(motor2PinA,HIGH);
102. digitalWrite(motor2PinB,LOW);
103. }
104. void FowardLeft(){ // LEFT 45 ANGLE
105. analogWrite(enableRPin, 255);
106. analogWrite(enableLPin, 100);
107. digitalWrite(motor1PinA, HIGH);
108. digitalWrite(motor1PinB,LOW);
109. digitalWrite(motor2PinA,HIGH);
110. digitalWrite(motor2PinB,LOW);
111. }
112. void BackLeft(){// LEFT BACK 45 ANGLE
113. analogWrite(enableRPin, 255);
114. analogWrite(enableLPin, 100);
115. digitalWrite(motor1PinA,LOW);
116. digitalWrite(motor1PinB,HIGH);
117. digitalWrite(motor2PinA,LOW);
118. digitalWrite(motor2PinB,HIGH);
119. }
120. void BackRight(){// RIGHT BACK 45 ANGLE
121. analogWrite(enableRPin,100);
122. analogWrite(enableLPin, 255);
123. digitalWrite(motor1PinA,LOW);
124. digitalWrite(motor1PinB,HIGH);
125. digitalWrite(motor2PinA,LOW);
126. digitalWrite(motor2PinB,HIGH);
127. }
