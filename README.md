
#include <Servo.h>

int TRIGGER_PIN = 6;
int ECHO_PIN = 3;
int SERVO_PIN = 5;

Servo gateServo;

void setup() {
  pinMode(TRIGGER_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  gateServo.attach(SERVO_PIN);
  gateServo.write(0); // Initially close the gate
  Serial.begin(9600);
}

void loop() {
  long duration, distance;
  
  // Trigger the ultrasonic sensor
  digitalWrite(TRIGGER_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIGGER_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIGGER_PIN, LOW);

  // Measure the distance
  duration = pulseIn(ECHO_PIN, HIGH);
  distance = duration * 0.034 / 2; // Calculate the distance in centimeters
  
  // Check if a car is nearby
  if (distance < 10) { // Adjust this threshold as per your requirement
    gateServo.write(90); // Open the gate to 90 degrees
    delay(5000); // Wait for 5 seconds
    gateServo.write(0); // Close the gate
  }

  delay(500); // Adjust the delay as needed between distance measurements
}

![image](https://github.com/saddamsssssssss/Open_gate/assets/139205268/3812dd63-7b65-439a-98a2-22a9f9bc3b0e)
