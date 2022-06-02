# Prosthetic-arm-DIY-code
Using a digital to analog converter, I was able to convert digital values to analog and allow the user to interact with
a force sensor to make the motor move which will move the fingers.
  #include <Servo.h>//the servo library needed to implement
  
        Servo servo;
        int reading;
        int LEDpin = 4;
        int LED1pin = 5;
        int LED2pin = 6;
        int LED3pin = 7;
        int sevA = 53;
        int sevB = 51;
        int sevC = 49;
        int sevD = 47;
        int sevE = 45;
        int sevF = 43;
        int sevG = 41;


This will set up the variables and define the inputs and outputs for my device.

      void setup(void) {
      Serial.begin(9600);
      servo.attach(9); //servo at digital pin 9
      servo.write(0); //initial point for servo
      pinMode(LEDpin, OUTPUT);//Line 22-32 are setting the LEDs and SSD to output values
      pinMode(LED1pin, OUTPUT);
      pinMode(LED2pin, OUTPUT);
      pinMode(LED3pin, OUTPUT);
      pinMode(sevA, OUTPUT);
      pinMode(sevB, OUTPUT);
      pinMode(sevC, OUTPUT);
      pinMode(sevD, OUTPUT);
      pinMode(sevE, OUTPUT);
      pinMode(sevF, OUTPUT);
      pinMode(sevG, OUTPUT);

    }
I will read the analog values and determine the maximum threshold that the force sensor can take.

    void loop(void) {
      reading = analogRead(A0); //attached to analog 0
      Serial.print("Sensor value = ");//displays a text to indicate the values displayed
      Serial.println(reading);//displays the values read by the force sensor
      
I created "if" conditions so that when a force sensor detects a specific value, then a different value will be displayed on the seven segment display.

      int value = map(reading, 0, 1023, 0, 255);
      if (value == 0) {       
        digitalWrite(sevA, HIGH);
        digitalWrite(sevB, HIGH);
        digitalWrite(sevC, HIGH);
        digitalWrite(sevD, HIGH);
        digitalWrite(sevE, HIGH);
        digitalWrite(sevF, HIGH);
        digitalWrite(sevG, LOW);

      }
      else if (value > 0 && value < 25) {
        digitalWrite(sevA, LOW);
        digitalWrite(sevB, HIGH);
        digitalWrite(sevC, HIGH);
        digitalWrite(sevD, LOW);
        digitalWrite(sevE, LOW);
        digitalWrite(sevF, LOW);
        digitalWrite(sevG, LOW);


      }
      else if (value > 25 && value < 50 ) {
        digitalWrite(sevA, HIGH);
        digitalWrite(sevB, HIGH);
        digitalWrite(sevC, LOW);
        digitalWrite(sevD, HIGH);
        digitalWrite(sevE, HIGH);
        digitalWrite(sevF, LOW);
        digitalWrite(sevG, HIGH);

      }
      else if (value > 50 && value < 75) {
        digitalWrite(sevA, HIGH);
        digitalWrite(sevB, HIGH);
        digitalWrite(sevC, HIGH);
        digitalWrite(sevD, HIGH);
        digitalWrite(sevE, LOW);
        digitalWrite(sevF, LOW);
        digitalWrite(sevG, HIGH);


      }
      else if (value > 75 && value < 100) {
        digitalWrite(sevA, LOW);
        digitalWrite(sevB, HIGH);
        digitalWrite(sevC, HIGH);
        digitalWrite(sevD, LOW);
        digitalWrite(sevE, LOW);
        digitalWrite(sevF, HIGH);
        digitalWrite(sevG, HIGH);
      }
      else if (value > 100 && value < 125) {
        digitalWrite(sevA, HIGH);
        digitalWrite(sevB, LOW);
        digitalWrite(sevC, HIGH);
        digitalWrite(sevD, HIGH);
        digitalWrite(sevE, LOW);
        digitalWrite(sevF, HIGH);
        digitalWrite(sevG, HIGH);


      }
      else if (value > 125 && value < 150) {
        digitalWrite(sevA, HIGH);
        digitalWrite(sevB, LOW);
        digitalWrite(sevC, HIGH);
        digitalWrite(sevD, HIGH);
        digitalWrite(sevE, HIGH);
        digitalWrite(sevF, HIGH);
        digitalWrite(sevG, HIGH);


      }
      else if (value > 150 && value < 175) {
        digitalWrite(sevA, HIGH);
        digitalWrite(sevB, HIGH);
        digitalWrite(sevC, HIGH);
        digitalWrite(sevD, LOW);
        digitalWrite(sevE, LOW);
        digitalWrite(sevF, LOW);
        digitalWrite(sevG, LOW);


      }
      else if (value > 175 && value < 190) {
        digitalWrite(sevA, HIGH);
        digitalWrite(sevB, HIGH);
        digitalWrite(sevC, HIGH);
        digitalWrite(sevD, HIGH);
        digitalWrite(sevE, HIGH);
        digitalWrite(sevF, HIGH);
        digitalWrite(sevG, HIGH);


      }
      else if (value > 190) {
        digitalWrite(sevA, HIGH);
        digitalWrite(sevB, HIGH);
        digitalWrite(sevC, HIGH);
        digitalWrite(sevD, LOW);
        digitalWrite(sevE, LOW);
        digitalWrite(sevF, HIGH);
        digitalWrite(sevG, HIGH);
     }
  
  allows the motor to turn according to the values read by the force sensor
  
      servo.write(value);
      if (value == 0) {// turns off the LEDs if no input is detected
        analogWrite(LEDpin, LOW);
        analogWrite(LED1pin, LOW);
        analogWrite(LED2pin, LOW);
        analogWrite(LED3pin, LOW);
      }
      
 sets turns on the LEDs according to the sensor values (notice how the map function is used here to create a gradual increase in LED brightness      

      if (value > 0) {                                       
        int LED1brightness = map(reading, 0, 1000, 0, 255);
        analogWrite(LEDpin, LED1brightness);
      }
      else {
        analogWrite(LEDpin, LOW);
      }
      if (value > 100) {
        int LED2brightness = map(reading, 0, 5000, 0, 255);
        analogWrite(LED1pin, LED2brightness);
      }
      else {
        analogWrite(LED1pin, LOW);
      }
      if (value > 150) {
        int LED3brightness = map(reading, 0, 7000, 0, 255);
        analogWrite(LED2pin, LED3brightness);
      }
      else {
        analogWrite(LED2pin, LOW);
      }
      if (value > 190) {
        int LED4brightness = map(reading, 0, 9000, 0, 255);
        analogWrite(LED3pin, LED4brightness);
      }
      else {
        analogWrite(LED3pin, LOW);
      }
      delay(100);// a small delay to allow the LEDs to grudually turn off

    }
