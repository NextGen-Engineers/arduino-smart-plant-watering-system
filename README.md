#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27, 16, 2);

// Pin definitions
const int pumpPin = 2;  // Pin controlling the water pump
const int buttonPin = 3;  // Pin connected to the push button
bool pumpState = LOW;  // Initial pump state (OFF)
bool lastButtonState = HIGH;  // To store the last button state
unsigned long lastDebounceTime = 0;  // Debounce timer
unsigned long debounceDelay = 200;  // Debounce delay (in milliseconds)

void setup() {
  Serial.begin(9600);
  lcd.init();
  lcd.backlight();
  lcd.clear();
  
  pinMode(pumpPin, OUTPUT);
  pinMode(buttonPin, INPUT_PULLUP);  // Configure the button pin with internal arduino pull-up resistor
  digitalWrite(pumpPin, HIGH);  // Set initial state to pump OFF
  
  delay(1000);
  
  lcd.setCursor(0, 0);
  lcd.print("IRRIGATION");
  lcd.setCursor(0, 1);
  lcd.print("SYSTEM IS ON");
  delay(3000);
  lcd.clear();
}

void loop() {
  int moistureValue = analogRead(A0);  // Read the moisture sensor value
  Serial.println(moistureValue);
  
  // Read the button state
  int buttonState = digitalRead(buttonPin);
  
  // Check if the button state has changed and apply debouncing
  if (buttonState != lastButtonState) {
    lastDebounceTime = millis();  // Reset the debounce timer
  }

  if ((millis() - lastDebounceTime) > debounceDelay) {
    // If the button state has changed (pressed and released)
    if (buttonState == LOW) {
      pumpState = !pumpState;  // Toggle pump state
      digitalWrite(pumpPin, pumpState);  // Update the pump
      
      // Display pump status on the LCD
      lcd.clear();
      if (pumpState == HIGH) {
        lcd.setCursor(0, 0);
        lcd.print("Manual Contol ");
      } else {
        lcd.setCursor(0, 0);
        lcd.print("Manual Control");
      }
      delay(700);  // Wait for the pump to stabilize (prevents multiple toggles)
    }
  }
  
  // Update lastButtonState
  lastButtonState = buttonState;

  // Automatic control based on moisture level
  if (moistureValue > 700 && pumpState == LOW) {
    digitalWrite(pumpPin, LOW);  // Pump ON if moisture is low
    lcd.setCursor(0, 0);
    lcd.print("Water Pump is ON ");
  } else if (moistureValue <= 500 && pumpState == LOW) {
    digitalWrite(pumpPin, HIGH);  // Pump OFF if moisture is sufficient
    lcd.setCursor(0, 0);
    lcd.print("Water Pump is OFF");
  }

  // Display moisture level
  if (moistureValue < 500) {
    lcd.setCursor(0, 1);
    lcd.print("Moisture : HIGH");
  } else if (moistureValue >= 500 && moistureValue < 700) {
    lcd.setCursor(0, 1);
    lcd.print("Moisture : MID ");
  } else {
    lcd.setCursor(0, 1);
    lcd.print("Moisture : LOW ");
  }
}
