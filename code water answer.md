const int soilMoisturePin = A0;    
const int pumpPin = 9;            
int threshold = 500;          
bool isWatering = false;          

void setup() {
  pinMode(soilMoisturePin, INPUT);
  pinMode(pumpPin, OUTPUT);
}

void loop() {
  int soilMoisture = analogRead(soilMoisturePin);

  // Check if soil moisture is below threshold and not currently watering
  if (soilMoisture < threshold && !isWatering) {
    startWatering();
  } 
  // Check if soil moisture is above threshold and currently watering
  else if (soilMoisture >= threshold && isWatering) {
    stopWatering();
  }
  
  delay(1000); // Check soil moisture every second
}

void startWatering() {
  digitalWrite(pumpPin, HIGH); // Turn on water pump
  isWatering = true;           // Set watering flag
  delay(5000);                 // Watering duration 
  digitalWrite(pumpPin, LOW);  // Turn off water pump
  isWatering = false;          // Reset watering flag
}

void stopWatering() {
  digitalWrite(pumpPin, LOW);  // Turn off water pump
  isWatering = false;          // Reset watering flag
}