
#include <Arduino.h>

const int moistureSensorPin = A0; // Pin for soil moisture sensor
const int relayPin = 7;            // Pin for relay module
const int moistureThreshold = 300;  // Adjust this value based on your sensor

void setup() {
    pinMode(relayPin, OUTPUT);     // Set relay pin as output
    digitalWrite(relayPin, LOW);   // Ensure pump is off at start
    Serial.begin(9600);             // Initialize serial communication
}

void loop() {
    int moistureLevel = analogRead(moistureSensorPin); // Read moisture level
    Serial.print("Moisture Level: ");
    Serial.println(moistureLevel); // Print moisture level to serial monitor

    // Check if the soil is dry
    if (moistureLevel > moistureThreshold) {
        Serial.println("Soil is dry. Turning on the pump.");
        digitalWrite(relayPin, HIGH); // Turn on the pump
        delay(5000);                   // Pump water for 5 seconds
        digitalWrite(relayPin, LOW);  // Turn off the pump
        Serial.println("Pump turned off.");
    } else {
        Serial.println("Soil is wet. No need to water.");
    }

    delay(10000); // Wait for 10 seconds before the next reading
}
 
