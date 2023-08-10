// Air Pollution Monitoring System using MQ-135 Gas Sensor

const int analogPin = A0; // Connect MQ-135 analog output to A0
const float VCC = 5.0; // Supply voltage of the sensor (in volts)
const float R0 = 76.63; // Sensor resistance in clean air (Calibrate this value based on your sensor)

void setup() {
  Serial.begin(9600);
}

void loop() {
  int sensorValue = analogRead(analogPin);
  float sensorVoltage = (sensorValue / 1023.0) * VCC;
  
  float RS_gas = (VCC - sensorVoltage) / sensorVoltage;
  
  // Using the ratio of RS_gas and R0 to estimate the PPM value of air pollution (CO2 equivalent)
  float ppm = 116.6020682 * pow(RS_gas / R0, -2.769034857);
  
  Serial.print("Air Pollution (PPM): ");
  Serial.println(ppm);
  
  delay(2000); // You can adjust the delay time based on your requirement
}
