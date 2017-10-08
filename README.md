
### Team Members
Hasan Erisir,
Keyrol Garcia Flacon,
Andy Jaramillo,
Jordan Wilson

___

### Project Details
Our project is based on an 8-bit Mario animation that runs across the screen. This looped animation also comes with an 8-bit style mario theme tune. This is an fun and easy Arduino project to replicate as it does not require much knowledge about Arduino and its components.
___
### How the Breadboard works
![breadboard image](https://sites.google.com/site/delseaphysics1/_/rsrc/1271270866717/Home/magnetism/series-and-parallel/building-circuits-1/Breadboard.png)
___
### Project Plan Gantt Chart
![Gantt Chart](http://puu.sh/xST8u/539c59e25e.png)
### Required Components
| Components    | Amount        | Average Price  |
| ------------- |:-------------:| -----:|
| Arduino Uno|1|£21.00|
| Piezo Buzzer|1|£3|
| LCD 16x2 |1|£7.50|
| Any colour LED |1|£0.09|
| Potentiometer(optional)|1|£3|
| Jumper Wires|22|£5.16 |
___
### Wiring the Arduino
![Arduino wiring](https://puu.sh/xSiOo/c8d5ac4185.png)
**<u> Step by step</u>**
1. Connect a wire from 5v into the positive bus.
2. Connect a wire from GROUND into the negative bus.
3. Place the LCD onto the breadboard. Make sure you allocate enough space for the other components as well.
4. Connect a wire from the NEGATIVE bus on the breadboard onto the GROUND port on the LCD and then connect a wire from the POSITIVE bus on the breadboard onto the VCC port on the LCD.
5. Place a potent adjuster onto the breadboard. Connect a cable from the POSITIVE and NEGATIVE bus into the correct ends. Then take a cable from the potent adjuster and insert it into the 3rd port on the LCD labelled "VO".
6. Insert cables into RS RW and E on the LCD and place them accordingly into the ports on the Arduino 12, 11 and 7.
7. Insert cables into DB4, DB5, DB6 and DB7 and place them into the ports 4, 5, 6 and 2 accordingly.
8. Take the last ports on the LCD(15 and 16) and place them into positive and negative in the that order.
9. Insert the Piezo buzzer onto the breadboard and take a cable from Port 3 on the Arduino into the positive leg on the Piezo. Take a cable from GROUND on the Arduino or the GROUND bus and place it onto the negative leg on the Piezo.
10. For the last step, insert the LED onto the board and take a cable from PORT 13 into the positive leg of the Arduino. Lastly, take a cable from the GROUND bus and place it into the LED's negative leg.

A **PDF** version of this tutorial can be found [here](http://puu.sh/xSlr2/14d0f2210f.pdf).
___
## Code
```
#include  <LiquidCrystal.h>
#define NOTE_G3  196
#define NOTE_GS3 208
#define NOTE_A3  220
#define NOTE_AS3 233
#define NOTE_B3  247
#define NOTE_C4  262
#define NOTE_CS4 277
#define NOTE_D4  294
#define NOTE_DS4 311
#define NOTE_E4  330
#define NOTE_F4  349
#define NOTE_FS4 370
#define NOTE_G4  392
#define NOTE_GS4 415
#define NOTE_A4  440
#define NOTE_AS4 466
#define NOTE_B4  494
#define NOTE_C5  523
#define NOTE_CS5 554
#define NOTE_D5  587
#define NOTE_DS5 622
#define NOTE_E5  659
#define NOTE_F5  698
#define NOTE_FS5 740
#define NOTE_G5  784
#define NOTE_GS5 831
#define NOTE_A5  880
#define NOTE_AS5 932
#define NOTE_B5  988
#define NOTE_C6  1047
#define NOTE_CS6 1109
#define NOTE_D6  1175
#define NOTE_DS6 1245
#define NOTE_E6  1319
#define NOTE_F6  1397
#define NOTE_FS6 1480
#define NOTE_G6  1568
#define NOTE_GS6 1661
#define NOTE_A6  1760
#define NOTE_AS6 1865
#define NOTE_B6  1976
#define NOTE_C7  2093
#define NOTE_CS7 2217
#define NOTE_D7  2349
#define NOTE_DS7 2489
#define NOTE_E7  2637
#define NOTE_F7  2794
#define NOTE_FS7 2960
#define NOTE_G7  3136
#define NOTE_GS7 3322
#define NOTE_A7  3520
#define NOTE_AS7 3729
#define NOTE_B7  3951
#define NOTE_C8  4186
#define NOTE_CS8 4435
#define NOTE_D8  4699
#define NOTE_DS8 4978

#define melodyPin 49

LiquidCrystal lcd(12, 11, 5, 4, 6, 2);
int backLight = 18;

int f=4;                  //set frames per second (fps)
int s;

int melody[] = {
  NOTE_E7, NOTE_E7, 0, NOTE_E7,
  0, NOTE_C7, NOTE_E7, 0,
  NOTE_G7, 0, 0,  0,
  NOTE_G6, 0, 0, 0,

  NOTE_C7, 0, 0, NOTE_G6,
  0, 0, NOTE_E6, 0,
  0, NOTE_A6, 0, NOTE_B6,
  0, NOTE_AS6, NOTE_A6, 0,

  NOTE_G6, NOTE_E7, NOTE_G7,
  NOTE_A7, 0, NOTE_F7, NOTE_G7,
  0, NOTE_E7, 0, NOTE_C7,
  NOTE_D7, NOTE_B6, 0, 0,

  NOTE_C7, 0, 0, NOTE_G6,
  0, 0, NOTE_E6, 0,
  0, NOTE_A6, 0, NOTE_B6,
  0, NOTE_AS6, NOTE_A6, 0,

  NOTE_G6, NOTE_E7, NOTE_G7,
  NOTE_A7, 0, NOTE_F7, NOTE_G7,
  0, NOTE_E7, 0, NOTE_C7,
  NOTE_D7, NOTE_B6, 0, 0
};
//Mario main them tempo
int tempo[] = {
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,

  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,

  9, 9, 9,
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,

  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,

  9, 9, 9,
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,
};

int underworld_melody[] = {
  NOTE_C4, NOTE_C5, NOTE_A3, NOTE_A4,
  NOTE_AS3, NOTE_AS4, 0,
  0,
  NOTE_C4, NOTE_C5, NOTE_A3, NOTE_A4,
  NOTE_AS3, NOTE_AS4, 0,
  0,
  NOTE_F3, NOTE_F4, NOTE_D3, NOTE_D4,
  NOTE_DS3, NOTE_DS4, 0,
  0,
  NOTE_F3, NOTE_F4, NOTE_D3, NOTE_D4,
  NOTE_DS3, NOTE_DS4, 0,
  0, NOTE_DS4, NOTE_CS4, NOTE_D4,
  NOTE_CS4, NOTE_DS4,
  NOTE_DS4, NOTE_GS3,
  NOTE_G3, NOTE_CS4,
  NOTE_C4, NOTE_FS4, NOTE_F4, NOTE_E3, NOTE_AS4, NOTE_A4,
  NOTE_GS4, NOTE_DS4, NOTE_B3,
  NOTE_AS3, NOTE_A3, NOTE_GS3,
  0, 0, 0
};
//Underwolrd tempo
int underworld_tempo[] = {
  12, 12, 12, 12,
  12, 12, 6,
  3,
  12, 12, 12, 12,
  12, 12, 6,
  3,
  12, 12, 12, 12,
  12, 12, 6,
  3,
  12, 12, 12, 12,
  12, 12, 6,
  6, 18, 18, 18,
  6, 6,
  6, 6,
  6, 6,
  18, 18, 18, 18, 18, 18,
  10, 10, 10,
  10, 10, 10,
  3, 3, 3
};

int thisNote = 0;
int thisSong = 0;
int buttonState = 0;
const int buttonPin = 2;
int acceso = 11;

byte mario11[8] = {
B00000,
B00000,
B00000,
B00000,
B00001,
B00001,
B00001,
B00000,

};
byte mario12[8] = {
B00001,
B00001,
B00001,
B00001,
B00000,
B00000,
B00000,
B00000
};
byte mario13[8] = {
  B00000,
B11111,
B11111,
B11111,
B11111,
B11111,
B11111,
B11111,

};
byte mario14[8] = {
B11111,
B11111,
B11111,
B11111,
B11111,
B11111,
B11111,
B11110
};

byte mario15[8] = {
   B00000,
B00000,
B11000,
B00000,
B11000,
B11100,
B11000,
B10000,

};

byte mario16[8] = {
B00000,
B10000,
B10000,
B10000,
B00000,
B00000,
B10000,
B00000
};

byte mario21[8] = {
   B00000,
B00000,
B00000,
B00000,
B00000,
B00000,
B00000,
B00000,
};

byte mario22[8] = {
B00111,
B00111,
B00111,
B00000,
B00001,
B00011,
B00011,
B00001
};

byte mario23[8] = {
   B00000,
B01111,
B11111,
B11111,
B11111,
B11111,
B11111,
B01111,

};

byte mario24[8] = {
B11111,
B11111,
B11111,
B11111,
B11111,
B11001,
B00000,
B10000
};
byte mario25[8] = {
B00000,
B00000,
B11100,
B10000,
B11100,
B11110,
B11100,
B11000,

};

byte mario26[8] = {
B11111,
B11111,
B10110,
B11110,
B11110,
B11110,
B00000,
B00000,
};

byte mario31[8] = {
B00000,
B00000,
B00000,
B00000,
B00000,
B00000,
B00000,
B00000,

};


byte mario32[8] = {
B00000,
B00000,
B00000,
B00000,
B00011,
B00011,
B00111,
B00000
};


byte mario33[8] = {
B00000,
B00000,
B00111,
B01111,
B01111,
B11111,
B11111,
B11111,

};

byte mario34[8] = {
B01111,
B11111,
B11111,
B11111,
B11111,
B11111,
B00111,
B00111
};

byte mario35[8] = {
B00000,
B00000,
B10000,
B11110,
B11000,
B11110,
B11111,
B11110,

};

byte mario36[8] = {
B11100,
B11110,
B11100,
B11000,
B11000,
B10000,
B00000,
B10000,
};

byte mario41[8] = {
B00000,
B00011,
B00111,
B00111,
B01111,
B01111,
B01111,
B00011,

};


byte mario42[8] = {
B01111,
B01111,
B01111,
B01111,
B00111,
B00011,
B00011,
B00011
};

byte mario43[8] = {
B00000,
B11000,
B11111,
B11100,
B11111,
B11111,
B11111,
B11110,
};

byte mario44[8] = {
B11100,
B11110,
B11110,
B11110,
B11100,
B11100,
B11110,
B10000
};


byte mario51[8] = {
B00000,
B00001,
B00011,
B00011,
B00111,
B00111,
B00111,
B00001,
};

byte mario52[8] = {
B11111,
B11111,
B11011,
B00111,
B01111,
B11111,
B11100,
B01110,
};

byte mario53[8] = {
B00000,
B11100,
B11111,
B11110,
B11111,
B11111,
B11111,
B11111,
};

byte mario54[8] = {
B11111,
B11111,
B11110,
B11111,
B11111,
B01111,
B00000,
B00000,
};



byte mario55[8] = {
B00000,
B00000,
B10000,
B00000,
B00000,
B10000,
B00000,
B00000,
};


byte mario56[8] = {
B11000,
B11000,
B10000,
B10000,
B10000,
B10000,
B00000,
B00000,
};


byte mario61[8] = {
B00000,
B00000,
B00000,
B00001,
B00001,
B00011,
B00011,
B00011,
};

byte mario62[8] = {
B00001,
B00011,
B00111,
B01111,
B01111,
B11111,
B11000,
B00000,
};



byte mario63[8] = {
B00000,
B00000,
B11110,
B11111,
B11111,
B11111,
B11111,
B11111,
};

byte mario64[8] = {
B11111,
B11111,
B11111,
B11111,
B11111,
B11110,
B11100,
B11110,
};

byte mario65[8] = {
B00000,
B00000,
B00000,
B10000,
B00000,
B10000,
B11000,
B10000,
};


byte mario66[8] = {
B00000,
B10000,
B00000,
B00000,
B00000,
B00000,
B00000,
B00000,
};

byte clean[8] = {
B00000,
B00000,
B00000,
B00000,
B00000,
B00000,
B00000,
B00000,
};

byte coin1[8] = {

B00000,
B00000,
B00000,
B00000,
B00111,
B01000,
B10001,
B10010,
};

byte coin2[8] = {

B10010,
B10010,
B10010,
B10010,
B10001,
B01000,
B00111,
B00000,
};


byte coin3[8] = {
B00000,
B00000,
B00000,
B00000,
B10000,
B01000,
B00100,
B10100,
};

byte coin4[8] = {
B10100,
B10100,
B10100,
B00100,
B00100,
B01000,
B10000,
B00000,
};

void setup() {
lcd.begin(18,2);
pinMode(backLight, OUTPUT);
digitalWrite(backLight, HIGH); 
lcd.clear();

  pinMode(3, OUTPUT);//buzzer
  pinMode(13, OUTPUT);//led indicator when singing a note
  for (int i = 3; i <= 7; i++) pinMode(i, OUTPUT);
  pinMode(buttonPin, INPUT);
s=1000/f;            //fps to ms

}

int size = sizeof(melody) / sizeof(int);
int noteDuration;
int activity = 0;

void loop() 
{
  buttonState = digitalRead(buttonPin);
  digitalWrite(acceso, HIGH);
  if (buttonState == HIGH) {
    if (thisSong == 2) {
      activity = underworld_tempo[thisNote];
      buzz(melodyPin, underworld_melody[thisNote], noteDuration);
      noteDuration = 1000 / underworld_tempo[thisNote];
      if (activity) {
        digitalWrite(acceso, LOW);
        if (acceso == 7) {
          acceso = 3;
        } else {
          acceso++;
        }
        digitalWrite(acceso, HIGH);
      }
    } else {
      activity = melody[thisNote];
      buzz(melodyPin, melody[thisNote], noteDuration);
      noteDuration = 1000 / tempo[thisNote];
      if (activity) {
        digitalWrite(acceso, LOW);
        if (acceso == 7) {
          acceso = 3;
        } else {
          acceso++;
        }
        digitalWrite(acceso, HIGH);
      }
    }
    int pauseBetweenNotes = noteDuration * 1.30;
    delay(pauseBetweenNotes);

    buzz(melodyPin, 0, noteDuration);
    if (thisNote == size) {
      thisNote = 0;
      if (thisSong == 2) {
        thisSong = 0;
        size = sizeof(melody) / sizeof(int);
      } else if (thisSong == 1) {
        thisSong = 2;
        size = sizeof(underworld_melody) / sizeof(int);
      } else if (thisSong == 0) {
        thisSong = 1;
        size = sizeof(melody) / sizeof(int);
      }
    } else {
      thisNote++;
    }

  } else {
    if (thisSong == 2) {
      activity = underworld_tempo[thisNote];
      if (activity == 0) {
        buzz(melodyPin, underworld_melody[thisNote], noteDuration);
        noteDuration = 1000 / underworld_tempo[thisNote];
        if (thisNote == size) {
          thisNote = 0;
          if (thisSong == 2) {
            thisSong = 0;
            size = sizeof(melody) / sizeof(int);
          } else if (thisSong == 1) {
            thisSong = 2;
            size = sizeof(underworld_melody) / sizeof(int);
          } else if (thisSong == 0) {
            thisSong = 1;
            size = sizeof(melody) / sizeof(int);
          }
        } else {
          thisNote++;
        }
      }
    } else {
      activity = melody[thisNote];
      if (activity == 0) {
        buzz(melodyPin, melody[thisNote], noteDuration);
        noteDuration = 1000 / tempo[thisNote];
        if (thisNote == size) {
          thisNote = 0;
          if (thisSong == 2) {
            thisSong = 0;
            size = sizeof(melody) / sizeof(int);
          } else if (thisSong == 1) {
            thisSong = 2;
            size = sizeof(underworld_melody) / sizeof(int);
          } else if (thisSong == 0) {
            thisSong = 1;
            size = sizeof(melody) / sizeof(int);
          }
        } else {
          thisNote++;
        }
      }
    }
  }

  /*sing(1);
    sing(1);
    sing(2);*/
}
{
  
lcd.setCursor(0,0);            //intro
lcd.print("  8-Bit Mario");
lcd.setCursor(0,1);
lcd.print(" Run Animation");
delay(2000);
lcd.clear();
lcd.setCursor(0,0);
lcd.print("    By");
lcd.setCursor(0,1);
lcd.print("Jan Stapler");


lcd.createChar(1, coin1);       //coin frames for the intro
lcd.createChar(2, coin2);
lcd.createChar(3, coin3);
lcd.createChar(4, coin4);

lcd.setCursor(11,0);
lcd.write(1);
lcd.setCursor(11,1);
lcd.write(2);
lcd.setCursor(12,0);
lcd.write(3);
lcd.setCursor(12,1);
lcd.write(4);
  lcd.setCursor(14,0);
lcd.write(1);
lcd.setCursor(14,1);
lcd.write(2);
lcd.setCursor(15,0);
lcd.write(3);
lcd.setCursor(15,1);
lcd.write(4);
delay(2000);
lcd.clear();


for (int a=0; a<16;a++)     //for loop to repeat marios animation until the end of the display
{
int b=a+1;
int c=a+2;
int d=a+3;
int e=a+4; 
  
lcd.createChar(1, mario11);
lcd.createChar(2, mario12);
lcd.createChar(3, mario13);
lcd.createChar(4, mario14);
lcd.createChar(5, mario15);
lcd.createChar(6, mario16);
lcd.createChar(7, clean);

lcd.setCursor(a,0);
lcd.write(1);
lcd.setCursor(a,1);
lcd.write(2);
lcd.setCursor(b,0);
lcd.write(3);
lcd.setCursor(b,1);
lcd.write(4);
lcd.setCursor(c,0);
lcd.write(5);
lcd.setCursor(c,1);
lcd.write(6);
delay(s);

lcd.createChar(1, mario21);
lcd.createChar(2, mario22);
lcd.createChar(3, mario23);
lcd.createChar(4, mario24);
lcd.createChar(5, mario25);
lcd.createChar(6, mario26);

lcd.setCursor(a,0);
lcd.write(1);
lcd.setCursor(a,1);
lcd.write(2);
lcd.setCursor(b,0);
lcd.write(3);
lcd.setCursor(b,1);
lcd.write(4);
lcd.setCursor(c,0);
lcd.write(5);
lcd.setCursor(c,1);
lcd.write(6);

delay(s);

  lcd.createChar(1, mario31);
lcd.createChar(2, mario32);
lcd.createChar(3, mario33);
lcd.createChar(4, mario34);
lcd.createChar(5, mario35);
lcd.createChar(6, mario36);

lcd.setCursor(a,0);
lcd.write(1);
lcd.setCursor(a,1);
lcd.write(2);
lcd.setCursor(b,0);
lcd.write(3);
lcd.setCursor(b,1);
lcd.write(4);
lcd.setCursor(c,0);
lcd.write(5);
lcd.setCursor(c,1);
lcd.write(6);

delay(s);

lcd.createChar(1, mario41);
lcd.createChar(2, mario42);
lcd.createChar(3, mario43);
lcd.createChar(4, mario44);
lcd.createChar(7, clean);
  lcd.setCursor(a,0);
lcd.write(7);
lcd.setCursor(a,1);
lcd.write(7);
lcd.setCursor(b,0);
lcd.write(1);
lcd.setCursor(b,1);
lcd.write(2);
lcd.setCursor(c,0);
lcd.write(3);
lcd.setCursor(c,1);
lcd.write(4);


delay(s);


lcd.createChar(1, mario51);
lcd.createChar(2, mario52);
lcd.createChar(3, mario53);
lcd.createChar(4, mario54);
lcd.createChar(5, mario55);
lcd.createChar(6, mario56);
lcd.createChar(7, clean);
lcd.setCursor(a,0);
lcd.write(7);
lcd.setCursor(a,1);
lcd.write(7);
lcd.setCursor(b,0);
lcd.write(1);
lcd.setCursor(b,1);
lcd.write(2);
lcd.setCursor(c,0);
lcd.write(3);
lcd.setCursor(c,1);
lcd.write(4);
lcd.setCursor(d,0);
lcd.write(5);
lcd.setCursor(d,1);
lcd.write(6);

delay(s);

  lcd.createChar(1, mario61);
lcd.createChar(2, mario62);
lcd.createChar(3, mario63);
lcd.createChar(4, mario64);
lcd.createChar(5, mario65);
lcd.createChar(6, mario66);
lcd.setCursor(b,0);
lcd.write(1);
lcd.setCursor(b,1);
lcd.write(2);
lcd.setCursor(c,0);
lcd.write(3);
lcd.setCursor(c,1);
lcd.write(4);
lcd.setCursor(d,0);
lcd.write(5);
lcd.setCursor(d,1);
lcd.write(6);

delay(s);
}
}

int song = 0;

void sing(int s) {
  // iterate over the notes of the melody:
  song = s;
  if (song == 2) {
    Serial.println(" 'Underworld Theme'");
    int size = sizeof(underworld_melody) / sizeof(int);
    for (int thisNote = 0; thisNote < size; thisNote++) {

      // to calculate the note duration, take one second
      // divided by the note type.
      //e.g. quarter note = 1000 / 4, eighth note = 1000/8, etc.
      int noteDuration = 1000 / underworld_tempo[thisNote];

      buzz(melodyPin, underworld_melody[thisNote], noteDuration);

      // to distinguish the notes, set a minimum time between them.
      // the note's duration + 30% seems to work well:
      int pauseBetweenNotes = noteDuration * 1.30;
      delay(pauseBetweenNotes);

      // stop the tone playing:
      buzz(melodyPin, 0, noteDuration);

    }

  } else {

    Serial.println(" 'Mario Theme'");
    int size = sizeof(melody) / sizeof(int);
    for (int thisNote = 0; thisNote < size; thisNote++) {

      // to calculate the note duration, take one second
      // divided by the note type.
      //e.g. quarter note = 1000 / 4, eighth note = 1000/8, etc.
      int noteDuration = 1000 / tempo[thisNote];

      buzz(melodyPin, melody[thisNote], noteDuration);

      // to distinguish the notes, set a minimum time between them.
      // the note's duration + 30% seems to work well:
      int pauseBetweenNotes = noteDuration * 1.30;
      delay(pauseBetweenNotes);

      // stop the tone playing:
      buzz(melodyPin, 0, noteDuration);

    }
  }
}

void buzz(int targetPin, long frequency, long length) {
  digitalWrite(13, HIGH);
  long delayValue = 1000000 / frequency / 2; // calculate the delay value between transitions
  //// 1 second's worth of microseconds, divided by the frequency, then split in half since
  //// there are two phases to each cycle
  long numCycles = frequency * length / 1000; // calculate the number of cycles for proper timing
  //// multiply frequency, which is really cycles per second, by the number of seconds to
  //// get the total number of cycles to produce
  for (long i = 0; i < numCycles; i++) { // for the calculated length of time...
    digitalWrite(targetPin, HIGH); // write the buzzer pin high to push out the diaphram
    delayMicroseconds(delayValue); // wait for the calculated delay value
    digitalWrite(targetPin, LOW); // write the buzzer pin low to pull back the diaphram
    delayMicroseconds(delayValue); // wait again or the calculated delay value
  }
  digitalWrite(13, LOW);

}
```
Parts of the code is taken from these sources: [Theme song](http://www.princetronics.com/supermariothemesong/), [Animation](http://forum.arduino.cc/index.php?topic=203873.0)