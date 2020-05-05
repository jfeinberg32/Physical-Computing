# LCD Stock Ticker
## Introduction:
My final project will be a stock ticker using the Arduino LCD screen to display the current value of the Dow Jones Industrial Average. In addition to the display, there will be visual and auditory feedback based on the current change in value of the Dow. 

## Materials:
- Arduino Uno
- LCD1602 Module
- Button 
- 2x 10k ohm resistors
- 4x 220 ohm resistor
- Jumper wires
- Piezo buzzer
- Red LED
- Green LED

## Interaction
Pressing the button will cause the Arduino to interact with a website that pulls the current Dow Jones value from an API. The value will be sent to the Arudino using a serial function, and then displayed on the LCD screen, along with the light/sound feedback based on the value itself. 

### Demo
![Demo Gif]()

## Schematic 
![Circuit Schematic](https://github.com/jfeinberg32/Physical-Computing/blob/master/finalSchematic.JPG)

## 3D Printer
The 3D printed aspect of this project is the housing that will contain all of the components to create a safe and user friendly way to operate the device.

![Circuit Housing](https://github.com/jfeinberg32/Physical-Computing/blob/master/finalHousingLabeled.JPG)

## Code
~~~
#include <LiquidCrystal.h>;
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
int greenPin = 8;
int redPin = 9;
int buzzPin = 10;

const int switchPin = 6;
int switchRead = 0;
int counter = 0;
boolean pressing = false;

String inputString = "";
boolean stringComplete = false;


void setup() {
  pinMode(switchPin, INPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(redPin, OUTPUT);
  pinMode(buzzPin, OUTPUT);
  // Switch on the LCD screen
  lcd.begin(16, 2);
  // Print these words to my LCD screen
  Serial.begin(115200);
}

void loop() {
  // put your main code here, to run repeatedly:
  switchRead = digitalRead(switchPin);
  if (counter == 0) {
    lcd.print("Press button for");
    lcd.setCursor(0, 1);
    lcd.print("Dow Jones info. ");
  }

  if (switchRead == 1)
  {
    pressing = true;
    counter++;
  }

  if (switchRead == 0 && pressing == true)
  {
    pressing = false;
    Serial.println("pressed");
    Serial.flush();

  }
}


void serialEvent()
{
  while (Serial.available())
  {
    char inChar = Serial.read();

    if (inChar != '\n')
    {
      inputString += inChar;
    } else {
      stringComplete = true;
    }

    if (stringComplete == true)
    {
      float curStock = inputString.toFloat();
      Serial.println(curStock);
      Serial.flush();

    // CODE TO RUN
      if (curStock > 0)
      {
        lcd.clear();
        lcd.setCursor(0, 0);
        lcd.print("Dow Jones: ");
        lcd.setCursor(0, 1);
        lcd.print("Up ");
        lcd.print(curStock);
        lcd.print(" pts");
        digitalWrite(greenPin, HIGH);
        digitalWrite(redPin, LOW);
        tone(buzzPin, 5000, 500);

      }
      else if (curStock < 0)
      {
        lcd.clear();
        lcd.setCursor(0, 0);
        lcd.print("Dow Jones: ");
        lcd.setCursor(0, 1);
        lcd.print("Down ");
        lcd.print(curStock);
        lcd.print(" pts");
        digitalWrite(redPin, HIGH);
        digitalWrite(greenPin, LOW);
        tone(buzzPin, 2000, 500);

      }
        stringComplete = false;
        inputString = "";
    }
  }
}
~~~ 
