#include <MFRC522.h>

#define RST_PIN   9     // Define the reset pin
#define SS_PIN    10    // Define the SS (Slave Select) pin
#define IRQ_PIN   2     // Define the interrupt pin

MFRC522 mfrc522(SS_PIN, RST_PIN);  // Create MFRC522 instance

void setup() {
  Serial.begin(9600);
  SPI.begin();        // Start SPI communication
  mfrc522.PCD_Init(); // Initialize MFRC522
  pinMode(IRQ_PIN, INPUT_PULLUP);  // Set the IRQ pin as input with internal pull-up resistor
  attachInterrupt(digitalPinToInterrupt(IRQ_PIN), onRFIDInterrupt, CHANGE);
}

void loop() {
  for(int i=0;i<100;i++)
  {
    Serial.print("x=");
    Serial.println(i);
    delay(500);
  }
  
    // Your main code here
}

void onRFIDInterrupt() {
  // This function will be called when an RFID interrupt is triggered
  Serial.println("RFID tag detected!");
  // Perform the desired wake-up actions here
}
