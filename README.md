# AndroidBluetoothControlledCar
AndroidBluetoothControlledCar is a repository on Coding in Arduino UNO. This is a simple code for operating a Android (Arduino-based) CAR using a Bluetooth Module.
The following code should be written in ardunio app and it will function properly.
......................................Code Begin.......................................
<!-- Using Pin 4 and Pin 7 of Arduino -->

#include <AFMotor.h>
#include <Servo.h>
AF_DCMotor motor1(7);    
AF_DCMotor motor2(4); 
char command; 
void setup() 
{       
  Serial.begin(9600);  
  Serial.flush();                  
}

void loop(){
  if(Serial.available() > 0){ 
    command = Serial.read(); 
    Stop();     //initialize state 
    Serial.println("Device Connected!");                         
    Serial.println(command);
    switch(command){
    case 'F':  
      forward();
      break;
    case 'B':  
       back();
      break;
    case 'L':  
      left();
      break;
    case 'R':
      right();
      break;
    }
  } 
}
void forward()
{
  motor1.setSpeed(255); //Define maximum velocity
  motor1.run(FORWARD); //rotate the motor clockwise
  motor2.setSpeed(255); //Define maximum velocity
  motor2.run(FORWARD); //rotate the motor clockwise
}

void back()
{
  motor1.setSpeed(255); 
  motor1.run(BACKWARD); //rotate the motor counterclockwise
  motor2.setSpeed(255); 
  motor2.run(BACKWARD); //rotate the motor counterclockwise
}

void left()
{
  motor1.setSpeed(255); //Define maximum velocity
  motor1.run(FORWARD); //rotate the motor clockwise
  motor2.setSpeed(0);
  motor2.run(RELEASE); //turn motor2 off
}

void right()
{
  motor1.setSpeed(0);
  motor1.run(RELEASE); //turn motor1 off
  motor2.setSpeed(255); //Define maximum velocity
  motor2.run(FORWARD); //rotate the motor clockwise
}

void Stop()
{
  motor1.setSpeed(0);
  motor2.run(RELEASE); //turn motor1 off
  motor2.setSpeed(0);
  motor2.run(RELEASE); //turn motor2 off
}

...........................................................END.......................................................................

\\The following code will implement few commands : FORWARD, BACK, LEFT,RIGHT,STOP....
\\Working to improve it...n IA will create a new repository for the new version

