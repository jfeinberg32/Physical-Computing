# Physical-Computing


## SOS Project Documentation:

The following video depicts my Arduino SOS Signal, which in morse code consists of 3 short flashes, then 3 long flashes, then 3 short flashes.


Here is the code for the SOS Signal:
```
` int ledpin = 2; `

` void setup() {
    // put your setup code here, to run once:
    pinMode(ledpin, OUTPUT);
} `

` void loop() {
  // put your main code here, to run repeatedly: `
  
 ` //3 short
        digitalWrite(ledpin, HIGH);
        delay(500);
        digitalWrite(ledpin, LOW);
        delay(300);
        digitalWrite(ledpin, HIGH);
        delay(500);
        digitalWrite(ledpin, LOW);
        delay(300);
        digitalWrite(ledpin, HIGH);
        delay(500);
        digitalWrite(ledpin, LOW);
        delay(300); `

  ` //3 long
        digitalWrite(ledpin, HIGH);
        delay(1500);
        digitalWrite(ledpin, LOW);
        delay(300);
        digitalWrite(ledpin, HIGH);
        delay(1500);
        digitalWrite(ledpin, LOW);
        delay(300);
        digitalWrite(ledpin, HIGH);
        delay(1500);
        digitalWrite(ledpin, LOW);
        delay(300); `

 ` //3 short
        digitalWrite(ledpin, HIGH);
        delay(500);
        digitalWrite(ledpin, LOW);
        delay(300);
        digitalWrite(ledpin, HIGH);
        delay(500);
        digitalWrite(ledpin, LOW);
        delay(300);
        digitalWrite(ledpin, HIGH);
        delay(500);
        digitalWrite(ledpin, LOW);
        delay(300); `

 ` delay(1000); `

`}`

```
