# IT-neopixel-tutorial

Since the adafruit library is used we need to include it at the beginning. After this we need to define pin 2 because this is the pin which my neopixel ring is plugged into
```cpp
#include <Adafruit_NeoPixel.h>
#define PIN 2
```

since the neopixel ring has 24 LEDs we need to declare this as a variable.
```cpp
int numPix = 24;
```
This sets the LEDs in the neopixel ring to be RGB

```cpp

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(numPix, PIN, NEO_GRB + NEO_KHZ800);

```
Now we need to setup some variables.
```cpp

int delay1 = 1;

int red = 0;
int green = 0;
int blue = 0;
int potAngle = 0;
int redPot = 1;
int greenPot = 2;
int bluePot = 3;

```
This initializes the NeoPixel library

```cpp
void setup()
{
  pixels.begin(); 
}

```
This loop converts the angle of the potentiometer and maps it to the amount of LED's to turn on 
```cpp

void loop()
{
  getColor();
  pixels.show();
  int val = analogRead(potAngle);
  int numPixNow = map(val, 0, 1023, 1, 24);
  for (int i = 0; i < numPix; i++){
    if (i < numPixNow){
      pixels.setPixelColor(i, pixels.Color(red, green, blue)); // this sends updated pixel colour to the neopixel ring
    } else{
      pixels.setPixelColor(i, pixels.Color(0, 0, 0)); 
    }
    ```
    This starts the loop again so the code is infinate and always checking
    ```cpp
    if (i == numPix){
      i=0;
    }
  }
}
```
This picks random values to sed for RGB

```cpp
void setColor(){
 red = random(0,255);
 green = random(0,255);
 blue = random(0,255);
 
}

```
This function is used to get the values from the potentiometers and then mapp them to 0-255 which is the range for RGB's
```cpp

void getColor(){
  int redAngle = analogRead(redPot);
  int greenAngle = analogRead(greenPot);
  int blueAngle = analogRead(bluePot);
  int rVal = map(redAngle, 0, 1023, 0, 255);
  int gVal = map(greenAngle, 0, 1023, 0, 255);
  int bVal = map(blueAngle, 0, 1023, 0, 255);
  
  
}
