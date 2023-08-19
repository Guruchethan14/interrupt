#include <MFRC522.h>

#define RST_PIN 9
#define SS_PIN 10
#define IRQ_PIN 2

MFRC522 mfrc522(SS_PIN, RST_PIN);

volatile bool rfidInterrupt = false;

void onRFIDInterrupt() {
    rfidInterrupt = true;
}

void setup() {
    Serial.begin(9600);
    SPI.begin();
    mfrc522.PCD_Init();
    pinMode(IRQ_PIN, INPUT_PULLUP);
    attachInterrupt(digitalPinToInterrupt(IRQ_PIN), onRFIDInterrupt, CHANGE);
}

void loop() {
    if (rfidInterrupt) {
        Serial.println("RFID tag detected!");
        Serial.println("add your interrupt code here!");
        rfidInterrupt = false;
        // Perform the desired wake-up actions here
    }

    for (int i = 0; i < 100; i++) {
        Serial.print("x=");
        Serial.println(i);
        delay(500);
    }
}
