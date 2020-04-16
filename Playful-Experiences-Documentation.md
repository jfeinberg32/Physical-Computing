# LCD Light Detector
## Introduction:
My playful experiences project will involve a light sensor and LCD screen to give you a reading of the current ambient light. Based on a few different ranges in light amount, the LCD screen will output a different interpretation of the value it is given (ex. "It's really bright out!").

## Materials:
- Arduino Uno
- LCD1602 Module
- Photoresistor
- Button 
- 3x 10k ohm resistors
- 1x 220 ohm resistor
- Jumper wires

## Interaction
The interaction of this interface will be pretty simple. All the user needs to do is press a button, which will cause the photoresistor to read the current ambient light to the Arduino, which will then take the value and send the appropriate interpretation to the LCD screen for the user to view. 

- VIDEO/GIF

## Schematic 

## Code
~~~
// Import the Liquid Crystal library
#include <LiquidCrystal.h>;
//Initialise the LCD with the arduino. LiquidCrystal(rs, enable, d4, d5, d6, d7)
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
int pResistor = A0;
int lightAmount;

const int switchPin = 6;
int switchRead = 0;
int counter = 0;

boolean pressing = false;

void setup() {
  pinMode(pResistor, INPUT);
  pinMode(switchPin, INPUT);
  //switch on LCD screen
  lcd.begin(16, 2);
  Serial.begin(9600);
}

void loop() {
  lightAmount = analogRead(pResistor);
  Serial.println(counter);
  switchRead = digitalRead(switchPin);
    if (counter == 0){
      lcd.print(" Press button to");
      lcd.setCursor(0,1);
      lcd.print(" measure light.");
    }

    if (switchRead == 1)
    {
      pressing = true;
      counter++;
    }

    if (switchRead == 0 && pressing == true)
    {
      pressing = false;
      if (lightAmount <= 350)
      {
        lcd.clear();
        lcd.setCursor(0,0);
        lcd.print(" It's pretty");
        lcd.setCursor(0,1);
        lcd.print(" dark out.");
      
      }
      else if (lightAmount > 350 && lightAmount <= 550)
      {
        lcd.clear();
        lcd.setCursor(0,0);
        lcd.print(" It's a");
        lcd.setCursor(0,1);
        lcd.print(" little sunny.");
       
      }
      else if (lightAmount > 550)
      {
        lcd.clear();
        lcd.setCursor(0,0);
        lcd.print(" It's really"); 
        lcd.setCursor(0,1);
        lcd.print(" bright out!");
        }

      }
    }
~~~ 