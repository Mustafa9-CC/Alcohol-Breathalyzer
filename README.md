🍷 **Alcohol Breathalyzer Using ESP32 & MQ Sensor**

**An open-source alcohol detection system built using an ESP32 microcontroller, MQ-series gas sensor (e.g., MQ-3/MQ-135), and an I2C LCD.
The project detects alcohol concentration in breath and categorizes it into states: Sober, Possible Alcohol, or High Alcohol.**

🧰 **Features**
🔹 Automatic sensor calibration for baseline R₀
🔹 Real-time alcohol detection and categorization
🔹 LCD display output (status + sensor values)
🔹 Serial monitor debug output for deeper analysis
🔹 Adjustable thresholds for fine-tuning accuracy

⚙️ **Hardware Components**

ESP32--Microcontroller--Reads analog data from MQ sensor
MQ-3 / MQ-135--Sensor	Gas sensor--Detects alcohol in breath
16x2 I2C LCD--Display--Shows status and readings
Wires & Power Supply--For connections and powering modules

🔌 **Circuit Connections**
Component	ESP32 Pin
MQ Sensor Output (A0)--GPIO 34 (Analog Input)
LCD SDA--GPIO 21
LCD SCL--GPIO 22
VCC--3.3V / 5V
GND--GND 
⚠️ **(The analog input pin may vary — change the SENSOR_PIN constant in the code if needed).**

💻 **Software Setup**
1. Install Arduino IDE (latest version).
2. Add ESP32 board via Boards Manager.
3. Install required libraries:
   .LiquidCrystal_I2C
   .Wire
4. Open the code file:
    src/alcohol_breathalyzer.ino
5. Select **Board → ESP32 Dev Module.**
6. Upload and monitor output at 115200 baud.

🧮 Working Principle
   .During calibration, the sensor measures baseline resistance (R₀) in clean air.
   .During measurement:
     .Sensor resistance (Rₛ) is calculated from analog voltage.
     .The ratio Rₛ/R₀ indicates alcohol presence.
     .Based on thresholds:
     .Rₛ/R₀ > 0.8 → Sober
     .0.6 < Rₛ/R₀ ≤ 0.8 → Possible Alcohol
     .Rₛ/R₀ ≤ 0.6 → High Alcohol
    You can modify these threshold values in the code for calibration to your specific sensor.

🧩 **Code Highlights**

const float THRESHOLD_TIPSY = 0.8;
const float THRESHOLD_DRUNK = 0.6;
float R0 = 0;

float Rs = 5000 * (4095.0 / analogRead(SENSOR_PIN) - 1.0);
float ratio = Rs / R0;

if (ratio < THRESHOLD_DRUNK) status = "High Alcohol!";
else if (ratio < THRESHOLD_TIPSY) status = "Possible Alcohol";
else status = "Sober";

**Example Output**
  LCD Display:
      Alcohol Analyzer
      Status: Possible Alcohol

**Serial Monitor:**
   Sensor ADC: 1320   Rs: 6400   R0: 8200   Ratio: 0.78
   Status: Possible Alcohol 
   
🧪 **Calibration Tips**
  Run the device in fresh air for calibration.
  Avoid blowing on the sensor during warm-up.
  Note the displayed R₀ and use it as your baseline.
  You can tweak thresholds based on your test results.

🪄 **Future Improvements**
  Add buzzer or LED alerts for high alcohol detection
  Add Bluetooth module to send readings to a phone
  Display BAC estimate (Blood Alcohol Concentration)
  Log readings on a web dashboard using ESP32 Wi-Fi
🧑‍💻 **Author**
  TEAM DESTRUCTORS-- 
    Team Lead-- Vasu Singh 
      Team Members-- 
       1. Mohd Mustafa 
       2. Kashif Ansari 
       3. Saksham Pratap Singh 
       4. Krish Pratap Singh 
       5. Ikbal Khan 
                     



