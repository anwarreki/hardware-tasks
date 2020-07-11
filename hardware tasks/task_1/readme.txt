display message "I love UOB task 1" using lcd 16*2
#include <LiquidCrystal.h>

// with the arduino pin number it is connected to
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

// make some custom characters:
byte heart[8] = {
  0b00000,
  0b01010,
  0b11111,
  0b11111,
  0b11111,
  0b01110,
  0b00100,
  0b00000
};

byte smiley[8] = {
  0b00000,
  0b00000,
  0b01010,
  0b00000,
  0b00000,
  0b10001,
  0b01110,
  0b00000
};

byte frownie[8] = {
  0b00000,
  0b00000,
  0b01010,
  0b00000,
  0b00000,
  0b00000,
  0b01110,
  0b10001
};

byte armsDown[8] = {
  0b00100,
  0b01010,
  0b00100,
  0b00100,
  0b01110,
  0b10101,
  0b00100,
  0b01010
};

byte armsUp[8] = {
  0b00100,
  0b01010,
  0b00100,
  0b10101,
  0b01110,
  0b00100,
  0b00100,
  0b01010
};

void setup() {
  // initialize LCD and set up the number of columns and rows:
  lcd.begin(16, 2);
  lcd.createChar(0, heart);         // create a new character
  lcd.createChar(1, smiley);        // create a new character
  lcd.createChar(2, frownie);       // create a new character
  lcd.createChar(3, armsDown);      // create a new character
  lcd.createChar(4, armsUp);        // create a new character
  lcd.setCursor(0, 0);              // set the cursor to the top left

  // Print a message to the lcd.
  lcd.print("I ");
  lcd.write(byte(0));               // when calling lcd.write() '0' must be cast as a byte
  lcd.print(" UOB Task 1  ");
  lcd.write((byte)1);

}

void loop() {
 
  int sensorReading = analogRead(A0);                         // read the potentiometer on A0:
  int delayTime = map(sensorReading, 0, 1023, 200, 1000);     // map the result to 200 - 1000:
  
  lcd.setCursor(4, 1);                                        // set the cursor to the bottom row, 5th position:
  lcd.write(3);                                               // draw the little man, arms down:
  delay(delayTime);
  
  lcd.setCursor(4, 1);
  lcd.write(4);                                               // draw him arms up:
  delay(delayTime);
}
