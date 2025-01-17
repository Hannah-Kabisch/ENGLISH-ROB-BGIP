<!--

author:   Hannah Kabisch
version:  0.1.0
language: EN
narrator: US English Female Female

import: https://raw.githubusercontent.com/liaTemplates/AVR8js/main/README.md

-->

[![LiaScript](https://raw.githubusercontent.com/LiaScript/LiaScript/master/badges/course.svg)](https://liascript.github.io/course/?https://github.com/TUBAF-IUZ-LiaScript/ENGLISH-ROB-BGIP/blob/main/HK_LED_bubblesort/Bubblesort.md)

# Bubblesort on a Strip of 12 LEDs
## The Programm
1. It fills the strip randomly with 5 different colors
2. Starts the Bubblesort and orders the colors according to values assingend to them
3. In the end the strip shows the color in order and starts all over again

## The Code
<div id="matrix-experiment">
<wokwi-neopixel-matrix pin="6" cols="12" rows="1"></wokwi-neopixel-matrix>
<span id="simulation-time"></span>
</div>

```HK_LED_bubblesort.cpp             Automata
#include <Arduino.h>
#include "FastLED.h"
#define DATA_PIN 6
#define BRIGHTNESS 180
#define NUM_LEDS 12
#define NUM_COLORS 6
int i = 0;
CRGB leds[NUM_LEDS];
CRGB colors[] = {CRGB:: Black, CRGB::Purple, CRGB::Blue , CRGB::Green,  CRGB::Yellow , CRGB::Red};
int sort[NUM_LEDS];

void led_colorval(int* array, CRGB* colors ){
  for(int i = 0; i < NUM_LEDS; i++){
    leds[i] = colors[sort[i]];
  }
}

void bubbleSort (int* array, int leng){
    int j = 0;
    int swapped = 0;
    for(int fertig = 0; fertig< leng; fertig ++){
        for(int i = leng-1; i> fertig; i--){
            if(array[i-1]> array[i]){
                int tmp = array[i];
                array[i]=array[i-1];
                array[i-1]= tmp;
                swapped = 1;
                delay(250); 
                led_colorval(array, colors);
                FastLED.show(); 

            }
        }
        delay(300);
        if(!swapped) return;
        swapped = 0;
    }
}

void setup() {
  FastLED.addLeds<NEOPIXEL, DATA_PIN>(leds, NUM_LEDS);
  FastLED.setBrightness(BRIGHTNESS);
}

void loop() {
  for(int i = 0; i<NUM_LEDS; i++){
    sort[i] = rand() % (NUM_COLORS -1) +1;
  }
  led_colorval(sort, colors);
  FastLED.show();
  delay(1500);

  bubbleSort( sort, NUM_LEDS);

  delay(2000);

}
```
@AVR8js.sketch(matrix-experiment)

## Idea:
1. use the LEDs in a fun way thats also educational
2. visualize bubblesort
3. use the potential of having multiple colors

## further development:
1. also implement other Sorting Algorithms (like quicksort) in the same way
2. add more colors or LEDs
3. use a matrix to also be able to use height to show the values (not only color)


