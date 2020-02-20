# Representing Emotion Project
## Calmness 

I wanted to create a project that I would enjoy using in my own life. As a result, I felt that calmness was a good choice, because I could theoretically set up the project in my room and enjoy the peacefulness of it whenever I want. I decided to implement a night and day aspect because I thought the fading lights would work well with this. Below, you can see a visual of what this looks like.

### Pictures
![gif](https://github.com/jfeinberg32/Physical-Computing/blob/master/emotion.gif)

![arduino](https://github.com/jfeinberg32/Physical-Computing/blob/master/arduino.jpeg)

![circuit](https://github.com/jfeinberg32/Physical-Computing/blob/master/circuit.jpeg)

![backview](https://github.com/jfeinberg32/Physical-Computing/blob/master/backview.jpeg)

### Project Code
```
int small = 3; //short led (blue)
int medium = 5; //medium led (red)
int large = 6; //tall led (yellow)
int pushButton = 2;

boolean pressed = 0;
int counter = 0;
int num = 0;
long pMillis = 0;
int interval = 10;
boolean flipFlop = false;

int lightingUp = 0;

void setup() {
  Serial.begin(9600);
  pinMode(pushButton, INPUT);
  pinMode(small, OUTPUT);
  pinMode(medium, OUTPUT);
  pinMode(large, OUTPUT);

}

void loop() {
  int buttonState = digitalRead(pushButton);
  //Serial.println(buttonState);
  if (buttonState == 1)
  {
    pressed = true;
  }
  if (buttonState == 0 && pressed == true)
  {
    pressed = false;
    //Serial.println("Pressed");
    num++;
  }
  Serial.println(lightingUp);
  if (num == 0) {
    digitalWrite(small, LOW);
    digitalWrite(medium, LOW);
    digitalWrite(large, LOW);
  } else if (num == 1) {
    digitalWrite(small, HIGH);
    digitalWrite(medium, HIGH);
    digitalWrite(large, HIGH);
  } else if (num == 2) {
    lightingUp++;
    if (millis() - pMillis >= interval)
    {
      pMillis = millis();
      if (flipFlop == false)
      {
        counter++;
      }
      else
      {
        counter--;
      }
    }

    if (lightingUp < 1000) {
      analogWrite(3, counter);
    } else if (lightingUp >= 1000 && lightingUp < 2000) {
      analogWrite(5, counter);
    } else if (lightingUp >= 2000 && lightingUp < 3000) {
      ;
      analogWrite(6, counter);
    } else {
      lightingUp = 0;
    }

    if (counter >= 255)
    {
      flipFlop = true;
    }
    if (counter <= 0)
    {
      flipFlop = false;
    }


  } else {
    num = 0;
  }

}
```
