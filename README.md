# LINE FOLLOWER ROBOT USING ARDUINO UNO R3

## DESCRIPTION

This is a line follower robot made by arduino uno r3, it is based on 5 channel IR sensor array installed on 4WD robot car.

## COMPONENTS REQUIRED

1. ARDUINO UNO R3
2. 5 CHANNEL IR SENSOR ARRAY (BFD-1000)
3. 4WD CAR KIT (CAN ALSO USE 2WD CAR)
4. 4 LITHIUM ION BATTERIES
5. L298N MOTOR DRIVER OR L293D MOTOR DRIVER SHIELD FOR ARDUINO
6. ON/OFF SWITCH (SPST)
7. JUMPER WIRES

## CIRCUIT DIAGRAM
![Ayush drive](https://user-images.githubusercontent.com/102857010/177578269-3a453d88-5671-4180-83d0-dee0653adc36.jpg)

## CODE
````
#define m1 7 //Right Motor MA1
#define m2 6 //Right Motor MA2
#define m3 4 //Left Motor MB1
#define m4 5 //Left Motor MB2
#define e1 9 //Right Motor Enable Pin EA
#define e2 3 //Left Motor Enable Pin EB

//**********5 Channel IR Sensor Connection**********//
#define ir1 A0
#define ir2 A1
#define ir3 A2
#define ir4 A3
#define ir5 A4
//*************************************************//

void setup() {
  pinMode(m1, OUTPUT);
  pinMode(m2, OUTPUT);
  pinMode(m3, OUTPUT);
  pinMode(m4, OUTPUT);
  pinMode(e1, OUTPUT);
  pinMode(e2, OUTPUT);
  pinMode(ir1, INPUT);
  pinMode(ir2, INPUT);
  pinMode(ir3, INPUT);
  pinMode(ir4, INPUT);
  pinMode(ir5, INPUT);
}

void loop() {
  //Reading Sensor Values
  int s1 = digitalRead(ir1); //Left Most Sensor
  int s2 = digitalRead(ir2); //Left Sensor
  int s3 = digitalRead(ir3); //Middle Sensor
  int s4 = digitalRead(ir4); //Right Sensor
  int s5 = digitalRead(ir5); //Right Most Sensor

  //if only middle sensor detects black line
  if((s1 == 1) && (s2 == 1) && (s3 == 0) && (s4 == 1) && (s5 == 1))
  {
    //going forward with full speed 
    analogWrite(e1, 100); //you can adjust the speed of the motors from 0-255
    analogWrite(e2, 100); //you can adjust the speed of the motors from 0-255
    digitalWrite(m1, HIGH);
    digitalWrite(m2, LOW);
    digitalWrite(m3, HIGH);
    digitalWrite(m4, LOW);
  }
  
  //if only left sensor detects black line
  if((s1 == 1) && (s2 == 0) && (s3 == 1) && (s4 == 1) && (s5 == 1))
  {
    //going right with full speed 
    analogWrite(e1, 80); //you can adjust the speed of the motors from 0-255
    analogWrite(e2, 80); //you can adjust the speed of the motors from 0-255
    digitalWrite(m1, HIGH);
    digitalWrite(m2, LOW);
    digitalWrite(m3, LOW);
    digitalWrite(m4, LOW);
  }
  
  //if only left most sensor detects black line
  if((s1 == 0) && (s2 == 1) && (s3 == 1) && (s4 == 1) && (s5 == 1))
  {
    //going right with full speed 
    analogWrite(e1, 80); //you can adjust the speed of the motors from 0-255
    analogWrite(e2, 80); //you can adjust the speed of the motors from 0-255
    digitalWrite(m1, HIGH);
    digitalWrite(m2, LOW);
    digitalWrite(m3, LOW);
    digitalWrite(m4, HIGH);
  }

  //if only right sensor detects black line
  if((s1 == 1) && (s2 == 1) && (s3 == 1) && (s4 == 0) && (s5 == 1))
  {
    //going left with full speed 
    analogWrite(e1, 80); //you can adjust the speed of the motors from 0-255
    analogWrite(e2, 80); //you can adjust the speed of the motors from 0-255
    digitalWrite(m1, LOW);
    digitalWrite(m2, LOW);
    digitalWrite(m3, HIGH);
    digitalWrite(m4, LOW);
  }

  //if only right most sensor detects black line
  if((s1 == 1) && (s2 == 1) && (s3 == 1) && (s4 == 1) && (s5 == 0))
  {
    //going left with full speed 
    analogWrite(e1, 80); //you can adjust the speed of the motors from 0-255
    analogWrite(e2, 80); //you can adjust the speed of the motors from 0-255
    digitalWrite(m1, LOW);
    digitalWrite(m2, HIGH);
    digitalWrite(m3, HIGH);
    digitalWrite(m4, LOW);
  }

  //if middle and right sensor detects black line
  if((s1 == 1) && (s2 == 1) && (s3 == 0) && (s4 == 0) && (s5 == 1))
  {
    //going left with full speed 
    analogWrite(e1,80); //you can adjust the speed of the motors from 0-255
    analogWrite(e2,80); //you can adjust the speed of the motors from 0-255
    digitalWrite(m1, LOW);
    digitalWrite(m2, LOW);
    digitalWrite(m3, HIGH);
    digitalWrite(m4, LOW);
  }

  //if middle and left sensor detects black line
  if((s1 == 1) && (s2 == 0) && (s3 == 0) && (s4 == 1) && (s5 == 1))
  {
    //going right with full speed 
    analogWrite(e1,80); //you can adjust the speed of the motors from 0-255
    analogWrite(e2,80); //you can adjust the speed of the motors from 0-255
    digitalWrite(m1, HIGH);
    digitalWrite(m2, LOW);
    digitalWrite(m3, LOW);
    digitalWrite(m4, LOW);
  }

  //if middle, left and left most sensor detects black line
  if((s1 == 0) && (s2 == 0) && (s3 == 0) && (s4 == 1) && (s5 == 1))
  {
    //going right with full speed 
    analogWrite(e1,80); //you can adjust the speed of the motors from 0-255
    analogWrite(e2,80); //you can adjust the speed of the motors from 0-255
    digitalWrite(m1, HIGH);
    digitalWrite(m2, LOW);
    digitalWrite(m3, LOW);
    digitalWrite(m4, HIGH);
  }

  //if middle, right and right most sensor detects black line
  if((s1 == 1) && (s2 == 1) && (s3 == 0) && (s4 == 0) && (s5 == 0))
  {
    //going left with full speed 
    analogWrite(e1,80); //you can adjust the speed of the motors from 0-255
    analogWrite(e2,80); //you can adjust the speed of the motors from 0-255
    digitalWrite(m1, LOW);
    digitalWrite(m2, HIGH);
    digitalWrite(m3, HIGH);
    digitalWrite(m4, LOW);
  }

  //if all sensors are on a black line
  if((s1 == 0) && (s2 == 0) && (s3 == 0) && (s4 == 0) && (s5 == 0))
  {
    //stop
    digitalWrite(m1, LOW);
    digitalWrite(m2, LOW);
    digitalWrite(m3, LOW);
    digitalWrite(m4, LOW);
  }
    if((s1 == 0) && (s2 == 0) && (s3 == 1) && (s4 == 1) && (s5 == 1))
  {
    //going right with full speed 
    analogWrite(e1,80); //you can adjust the speed of the motors from 0-255
    analogWrite(e2,80); //you can adjust the speed of the motors from 0-255
    digitalWrite(m1, HIGH);
    digitalWrite(m2, LOW);
    digitalWrite(m3, LOW);
    digitalWrite(m4, HIGH);
        }
    if((s1 == 1) && (s2 == 1) && (s3 == 1) && (s4 == 0) && (s5 == 0))
  {
    //going left with full speed 
    analogWrite(e1,80); //you can adjust the speed of the motors from 0-255
    analogWrite(e2,80); //you can adjust the speed of the motors from 0-255
    digitalWrite(m1, LOW);
    digitalWrite(m2, HIGH);
    digitalWrite(m3, HIGH);
    digitalWrite(m4, LOW);
  }
}
````
