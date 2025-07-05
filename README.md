// Iron Man-style AutoBoots - Smart Pressure + Thruster Assist

#define LEFT_SENSOR A0
#define RIGHT_SENSOR A1
#define MOTOR_LEFT 9
#define MOTOR_RIGHT 10
#define THRESHOLD 200  // Adjust based on your pressure sensor range

void setup() {
  Serial.begin(9600);
  pinMode(MOTOR_LEFT, OUTPUT);
  pinMode(MOTOR_RIGHT, OUTPUT);
}

void loop() {
  int leftPressure = analogRead(LEFT_SENSOR);
  int rightPressure = analogRead(RIGHT_SENSOR);

  Serial.print("Left: ");
  Serial.print(leftPressure);
  Serial.print(" | Right: ");
  Serial.println(rightPressure);

  if (leftPressure > THRESHOLD) {
    analogWrite(MOTOR_LEFT, map(leftPressure, THRESHOLD, 1023, 0, 255));
  } else {
    analogWrite(MOTOR_LEFT, 0);
  }

  if (rightPressure > THRESHOLD) {
    analogWrite(MOTOR_RIGHT, map(rightPressure, THRESHOLD, 1023, 0, 255));
  } else {
    analogWrite(MOTOR_RIGHT, 0);
  }

  delay(50); // Smoothing
}
