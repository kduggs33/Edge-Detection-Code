# Edge-Detection-Code
#include <Wire.h>
#include <Adafruit_MotorShield.h>
Adafruit_MotorShield AFMS = Adafruit_MotorShield();
Adafruit_DCMotor *leftMotor = AFMS.getMotor(1);
Adafruit_DCMotor *rightMotor = AFMS.getMotor(2);
const int leftanalogPin = A0;
const int centeranalogPin = A1;
const int rightanalogPin = A2;
const int threshold = 250;

void setup() {
  Serial.begin(9600);
  Serial.println("Edge Detection Program");
  AFMS.begin(1000);
  leftMotor->setSpeed(50);
  rightMotor->setSpeed(50);
  leftMotor->run(FORWARD);
  leftMotor->run(RELEASE);
  rightMotor->run(FORWARD);
  rightMotor->run(RELEASE);
  
}

void loop() {
  int leftanalogValue = analogRead(leftanalogPin);
  int centeranalogValue = analogRead(centeranalogPin);
  int rightanalogValue = analogRead(rightanalogPin); 
  
  if ((leftanalogValue > threshold) || (centeranalogValue > threshold) || (rightanalogValue > threshold)) {
    leftMotor->setSpeed(0);
    leftMotor->run(RELEASE);
    rightMotor->setSpeed(0);
    rightMotor->run(RELEASE);
    
    delay(1000);
    
    leftMotor->setSpeed(100);
    leftMotor->run(BACKWARD);
    rightMotor->setSpeed(100);
    rightMotor->run(BACKWARD);

    delay(1000);

    leftMotor->setSpeed(150);
    leftMotor->run(BACKWARD);
    rightMotor->setSpeed(150);
    rightMotor->run(FORWARD);

    delay(1000);

  } 
  
 if ((leftanalogValue < threshold) && (centeranalogValue < threshold) && (rightanalogValue < threshold)) {
  leftMotor->setSpeed(50);
  leftMotor->run(FORWARD);
  rightMotor->setSpeed(50);
  rightMotor->run(FORWARD);
 }
  
  Serial.println(leftanalogValue);
  delay(1);
  Serial.println(centeranalogValue);
  delay(1);
  Serial.println(rightanalogValue);
  delay(1);
  }
