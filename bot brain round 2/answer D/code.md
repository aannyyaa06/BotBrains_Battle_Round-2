// ultrasonic sensor pins
const int trigPin = 9; 
const int echoPin = 10;

 
// Motor control pins 
const int leftMotorPin = 5; 
const int rightMotorPin = 6;

void setup() {
// Initialize serial communication for debugging
Serial.begin(9600);

// Initialize ultrasonic sensor pins
pinMode(trigPin, OUTPUT);
pinMode(echoPin, INPUT);

// Initialize motor control pins
pinMode(leftMotorPin, OUTPUT);
pinMode(rightMotorPin, OUTPUT);
}

void loop() {
digitalWrite(trigPin, LOW);
delayMicroseconds(2);
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

// Read duration from ultrasonic sensor
long duration = pulseIn(echoPin, HIGH);

// Calculate distance in centimeters
int distance_cm = duration * 0.034 / 2;

Serial.print("Distance: ");
Serial.print(distance_cm);
Serial.println(" cm");

// Decision making based on distance
if (distance_cm <= 20) {
// If obstacle detected within 20 cm, stop and turn right
stopRobot();
delay(1000); 
turnRight(); 
} else {
moveForward();
}

delay(100); 
}

// Function to stop the robot
void stopRobot() {
digitalWrite(leftMotorPin, LOW);
digitalWrite(rightMotorPin, LOW);
}

// Function to turn right
void turnRight() {
digitalWrite(leftMotorPin, HIGH);
digitalWrite(rightMotorPin, LOW);
}

// Function to move forward
void moveForward() {
digitalWrite(leftMotorPin, HIGH);
digitalWrite(rightMotorPin, HIGH);
}