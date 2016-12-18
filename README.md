# Codice-Arduino-lampada-colori


#include <Adafruit_NeoPixel.h>
#ifdef __AVR__
  #include <avr/power.h>
#endif

// Which pin on the Arduino is connected to the NeoPixels?
// On a Trinket or Gemma we suggest changing this to 1
#define PIN            8

// How many NeoPixels are attached to the Arduino?
#define NUMPIXELS      9
#define BUTTON 1    

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

// constants won't change. They're used here to
// set pin numbers:
const int buttonPin = 1;     // the number of the pushbutton pin
const int ledPin = 8;      // the number of the LED pin

int stato = 0;
// variables will change:
int buttonState = 0;         // variable for reading the pushbutton status

void setup() {
  // initialize the LED pin as an output:
  pinMode(ledPin, OUTPUT);
  // initialize the pushbutton pin as an input:
  pinMode(buttonPin, INPUT_PULLUP);

   pixels.begin(); 
}

void accendi(int r, int g, int b) {
 for(int i=0;i<NUMPIXELS;i++){

    // pixels.Color takes RGB values, from 0,0,0 up to 255,255,255
    pixels.setPixelColor(i, pixels.Color(r,g,b)); // Moderately bright green color.

    pixels.show(); // This sends the updated pixel color to the hardware.
 }
  
}

void loop() {
  // read the state of the pushbutton value:
  buttonState = digitalRead(buttonPin);
  
  // check if the pushbutton is pressed.
  // if it is, the buttonState is HIGH:
  if (buttonState == LOW) {
    delay(300);
    buttonState = digitalRead(buttonPin);
    if ( buttonState == LOW ) {
          stato=stato+1;
          if (stato>4) {
            stato=0;
            accendi (0,0,0);
          }
    }
  }
  if(stato == 1) {
    // lampada on
    accendi(255,255,255);
  }  
  if(stato == 2) {
    // off
    accendi(255,0,0);
  }
  if (stato == 3) {
    accendi(0,255,0);
  }
  if (stato == 4){
    accendi(0,0,255);
  }
 
 
}
