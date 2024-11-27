#include <IRremote.h>

const int RECV_PIN = 15;  // GPIO pin connected to the IR receiver

void setup() {
  Serial.begin(115200);  // Start the Serial Monitor
  IrReceiver.begin(RECV_PIN, ENABLE_LED_FEEDBACK);  // Initialize the IR receiver on GPIO 15
  Serial.println("IR Receiver Initialized. Waiting for IR signals...");
}

void loop() {
  if (IrReceiver.decode()) {  // Check if a signal has been received
    Serial.println("IR Signal Received!");

    // Display the raw received IR code in HEX format
    Serial.print("Received Code (HEX): ");
    Serial.println(IrReceiver.decodedIRData.decodedRawData, HEX);

    // Display the protocol of the received signal
    Serial.print("Protocol: ");
    Serial.println(IrReceiver.getProtocolString());

    // Display the address and command if available
    Serial.print("Address: ");
    Serial.println(IrReceiver.decodedIRData.address, HEX);
    Serial.print("Command: ");
    Serial.println(IrReceiver.decodedIRData.command, HEX);

    // Resume listening for the next signal
    IrReceiver.resume();
  }
}
