// Purpose: To echo user-inputted characters to a 14-segment display.
// Reference: http://darcy.rsgc.on.ca/ACES/TEI3M/1920/Tasks.html#PoV
// Author: A. Goldman
// Date: Nov. 9, 2019
// Status: Working

#include <EEPROM.h>       // Includes the EEPROM library
uint8_t switchPin = 14;   // Assigns 14 as the switch pin
uint8_t clockPin = 13;    // Assigns 13 as the clock pin, SR 11
uint8_t dataPin = 11;     // Assigns 11 as the data pin, SR 14
uint8_t latchPin = 10;    // Assigns 10 as the latch pin, SR 12
uint8_t outputEnable = 5; // Assigns 5 as the output enable pin, SR 13
uint8_t letter1;          // Creates the variable for the first ASCII input
uint8_t letter2;          // Creates the variable for the second ASCII input
uint8_t brightness = 240; // Sets value for brightness of displays

void setup()
{
    Serial.begin(9600);                    // Initializes the serial monitor
    pinMode(switchPin, OUTPUT);            // Assigns switchPin as an output pin
    pinMode(clockPin, OUTPUT);             // Assigns clockPin as an output pin
    pinMode(dataPin, OUTPUT);              // Assigns dataPin as an output pin
    pinMode(latchPin, OUTPUT);             // Assigns latchPin as an output pin
    pinMode(outputEnable, OUTPUT);         // Assigns outputEnable as an output pin
    analogWrite(outputEnable, brightness); // Sets brightness of displys
}

void loop()
{
    while (!Serial.available()); // Waits until serial input available
    if (Serial.available() == 1)
    {                                 // If the first input is available,
        letter1 = Serial.read();      // Read it and assign to letter1
        constrain(letter1, 'A', 'z'); // Constrain as upper/lowercase letter
        delay(10);                    // Delay for 10 milliseconds
    }
    if (Serial.available() >= 1)
    {                                 // If the second input is available,
        letter2 = Serial.read();      // Read it and assign to letter2
        constrain(letter2, 'A', 'z'); // Contrain as upper/lowercase letter
        delay(10);                    // Delay for 10 milliseconds
    }
    if (letter1 >= 96 && letter1 <= 122)
    {                           // Converts lower to
        letter1 = letter1 - 32; // uppercase letter by subtracting 32
    }
    if (letter2 >= 96 && letter2 <= 122)
    {                           // Converts lower to
        letter2 = letter2 - 32; // uppercase letter by subtracting 32
    }
    while (1)
    {                                // Runs forever; while is always true
        digitalWrite(latchPin, LOW); // Latch pin low; begin to receive data

        shiftOut(dataPin, clockPin, LSBFIRST, EEPROM.read(letter1 + 26));
        shiftOut(dataPin, clockPin, LSBFIRST, EEPROM.read(letter1));
        digitalWrite(latchPin, HIGH); // After maps read from EEPROM, output
        digitalWrite(switchPin, LOW); // Turns current digit off, other on
        delay(1);                     // Delay for 1 millisecond
        digitalWrite(latchPin, LOW);  // Latch pin low; begin to receive data
        shiftOut(dataPin, clockPin, LSBFIRST, EEPROM.read(letter2 + 26));
        shiftOut(dataPin, clockPin, LSBFIRST, EEPROM.read(letter2));
        digitalWrite(latchPin, HIGH);  // After maps read from EEPROM, output
        digitalWrite(switchPin, HIGH); // Turns current digit off, other on
        delay(1);                      // Delay for 1 millisecond
    }
}
