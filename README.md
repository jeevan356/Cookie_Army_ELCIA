#Aggibot System(Robot that Supports and help Farmer)
## Cookie_Army_ELCIA

<p align="justify">
Intelligent robotic system that can autonomously perform agricultural tasks. This system aims to support farmers by increasing productivity, reducing manual labor, and ensuring precise resource management. The system should enhance efficiency and optimize resource usage, while being adaptable to various types of crops and farming environments.
 
![P1](https://github.com/jeevan356/Cookie_Army_ELCIA/assets/112291164/20a5bc5f-ca17-499f-b5e4-49381b08fe72.type)

"The development phase has already begun. According to our previous plan, we have successfully completed the rover section, and the 3D printing of the arms is also finished. Now, the next step is to add the best features to the arm that is Semi Autonomous Planting,Automated Watering,Semi Autonomous Harvesting,Environmental Monitoring."

![P2](https://github.com/jeevan356/Cookie_Army_ELCIA/assets/112291164/af1ad1b8-1a36-43e9-a105-cd0360629ae9) 
![P3](https://github.com/jeevan356/Cookie_Army_ELCIA/assets/112291164/46d4abba-2360-432e-a32e-7d1b07fc4439)
![P4](https://github.com/jeevan356/Cookie_Army_ELCIA/assets/112291164/d02434c5-8cb4-49c2-8bfb-aa66b38d5be9)
![P5](https://github.com/jeevan356/Cookie_Army_ELCIA/assets/112291164/8faaba71-c322-48ff-98b4-32e3e6701f51)

The Demo video of The First Part of the Prototype stage
https://github.com/jeevan356/Cookie_Army_ELCIA/assets/112291164/c4181283-e21a-4574-89d0-80748104fe1e



#our code for the rover
// Motor driver pins
#define IN1 2
#define IN2 3
#define IN3 4
#define IN4 5
#define ENA 9
#define ENB 10

// Ultrasonic sensor pins
#define TRIG 6
#define ECHO 7

// Distance threshold (in cm) to stop the motors
#define DISTANCE_THRESHOLD 30

void setup() {
  // Set motor driver pins as outputs
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);
  pinMode(ENA, OUTPUT);
  pinMode(ENB, OUTPUT);
  
  // Set ultrasonic sensor pins
  pinMode(TRIG, OUTPUT);
  pinMode(ECHO, INPUT);
  
  Serial.begin(9600);
}

void loop() {
  // Measure distance with ultrasonic sensor
  long duration, distance;
  digitalWrite(TRIG, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG, LOW);
  duration = pulseIn(ECHO, HIGH);
  distance = duration * 0.034 / 2;

  // Print distance to Serial Monitor
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance < DISTANCE_THRESHOLD) {
    // Stop motors if an object is detected within the threshold distance
    stopMotors();
  } else {
    // Move forward if no object is detected within the threshold distance
    moveForward();
  }

  delay(100); // Small delay to prevent excessive sensor readings
}

void stopMotors() {
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);
  analogWrite(ENA, 0); // Stop speed
  analogWrite(ENB, 0); // Stop speed
}

void moveForward() {
  analogWrite(ENA, 255); // Full speed
  analogWrite(ENB, 255); // Full speed
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}


