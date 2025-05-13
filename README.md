Sure! Here's a detailed yet concise `README.md` file for your **Smart Home Control System** project, covering all three components: ESP32 firmware, Flask server, and Flet application.

---

# 🏠 Smart Home Control System

This project is a complete smart home control system composed of three core components:

1. **ESP32 Firmware** (Arduino-based)
2. **Flask Web Server** (for communication and visualization)
3. **Flet Desktop App** (for interactive control and real-time monitoring)

Together, they enable sensor data collection, device control, and seamless communication between the physical world (ESP32) and a user-friendly graphical interface.

---

## 📡 1. ESP32 Firmware

### Features:

* Reads values from:

  * **Potentiometer** (`ANALOG_PIN`)
  * **Button** (`BUTTON_PIN`)
  * **PIR Motion Sensor** (`PIR_PIN`)
* Controls:

  * **LED** (`LEDPIN`)
  * **Servo Motor** (`SERVO_PIN`)
* Sends sensor data to the Flask server (`/esp/update`)
* Retrieves control commands from the server (`/esp/control`)
* Motion detection events are logged via Serial
* Servo locks/unlocks and LED toggles based on Flet UI input

### Requirements:

* Arduino IDE with the following libraries:

  * `WiFi.h`
  * `HTTPClient.h`
  * `ArduinoJson.h`
  * `ESP32Servo.h`

### Setup:

1. Replace WiFi credentials in the sketch:

   ```cpp
   const char* ssid = "Galaxy";
   const char* password = "hiwc2593";
   ```
2. Replace the server IP with your local IP:

   ```cpp
   const char* serverIP = "192.168.208.49";
   ```

---

## 🌐 2. Flask Web Server

### Features:

* Serves as the **communication bridge** between the ESP32 and the Flet app
* Web dashboard displays:

  * Sensor values from the ESP32
  * Current control values from the Flet app
* API Endpoints:

  * `POST /esp/update`: Receives sensor data from ESP
  * `GET /esp/control`: Sends control values to ESP
  * `POST /flet/update`: Receives control input from Flet app
  * `GET /dashboard`: Returns combined ESP + Flet state (JSON)
  * `GET /`: HTML dashboard showing system status

### Running the server:

```bash
python app.py
```

Make sure `flask`, `flask_cors`, and any other dependencies are installed.

---

## 🧩 3. Flet App

### Features:

* Control the ESP32 remotely using:

  * **LED ON/OFF toggle**
  * **Servo Lock/Unlock**
* Displays:

  * **Potentiometer value**
  * **Button press state**
  * **Motion detection**
* Visual indicators + historical table for motion & analog data
* Periodic updates via background thread

### Requirements:

Install Flet:

```bash
pip install flet
```

### Running the Flet app:

```bash
python main.py
```

### Configuration:

Ensure the `SERVER_URL` in the Flet app matches the IP of the Flask server:

```python
SERVER_URL = "http://192.168.208.49:5000"
```

---

## 🔄 Data Flow Summary

```
ESP32 ➡️ [Sensor Data] ➡️ Flask Server ➡️ 🖥️ Flet App
ESP32 ⬅️ [Control Commands] ⬅️ Flask Server ⬅️ 🖥️ Flet App
```

* The ESP32 regularly pushes sensor data to the server
* The Flet app sends control commands to the server
* The server acts as a sync layer between the two

---

## 🛠️ Future Improvements

* Add support for more sensors (e.g., DHT11 for temperature/humidity)
* Secure endpoints with token authentication
* Store historical data in a database
* Add real-time charts in the Flet app

---

## 📷 Schematic

*![image](https://github.com/user-attachments/assets/985704e8-c015-4989-bc8a-c617d92ceb99)
*

---

## 👨‍💻 Author

**Smart Home Control System** developed by \Albert Mduduze Hlelesi.

