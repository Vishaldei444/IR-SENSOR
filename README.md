# Smart Obstacle Detection System using HC-SR04 and Arduino UNO

A simple Arduino-based obstacle detection system that uses the HC-SR04 ultrasonic sensor to measure distance and automatically turns an LED ON when an object is detected within a predefined range.

## 📌 Project Overview

This project demonstrates how ultrasonic sensing works for obstacle detection.

- Distance < 50 cm → LED ON
- Distance ≥ 50 cm → LED OFF

The measured distance is displayed on the Serial Monitor in real time.

## ✨ Features

- Real-time distance measurement
- Obstacle detection using ultrasonic waves
- LED status indication
- Serial Monitor output
- Easy simulation using Wokwi

## 🛠️ Components Required

- Arduino UNO
- HC-SR04 Ultrasonic Sensor
- LED
- 220Ω Resistor
- Jumper Wires

## 🔌 Circuit Connections

### HC-SR04 to Arduino UNO

| HC-SR04 Pin | Arduino Pin |
|------------|-------------|
| VCC | 5V |
| GND | GND |
| TRIG | D9 |
| ECHO | D10 |

### LED Connection

| LED Pin | Arduino Pin |
|---------|-------------|
| Anode (+) | D8 |
| Cathode (-) | GND through 220Ω resistor |

## ⚙️ Working Principle

1. Arduino sends a 10 µs pulse to the TRIG pin.
2. The HC-SR04 emits ultrasonic waves.
3. The waves reflect from the object and return to the sensor.
4. The ECHO pin remains HIGH for the round-trip duration.
5. Arduino measures the duration using `pulseIn()`.
6. Distance is calculated using:

```text
Distance (cm) = (Duration × 0.034) / 2
```

Where:

- `0.034 cm/µs` is the speed of sound.
- Division by `2` accounts for the forward and return journey.

7. If the measured distance is less than 50 cm, the LED turns ON; otherwise, it turns OFF.

## 💻 Arduino Code

```cpp
#define TRIG_PIN 9
#define ECHO_PIN 10
#define LED_PIN 8

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(LED_PIN, OUTPUT);

  Serial.begin(9600);
}

void loop() {

  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);

  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  long duration = pulseIn(ECHO_PIN, HIGH);

  float distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance < 50) {
    digitalWrite(LED_PIN, HIGH);
  } else {
    digitalWrite(LED_PIN, LOW);
  }

  delay(200);
}
```

## 🔗 Project Links

- **Wokwi Simulation:** https://wokwi.com/projects/YOUR_PROJECT_ID
- **Demo Video:** https://youtu.be/YOUR_VIDEO_ID

## ▶️ How to Run

### Using Wokwi

1. Open the Wokwi project link.
2. Click **Start Simulation**.
3. Adjust the obstacle distance using the sensor controls.
4. Open the Serial Monitor to view distance readings.
5. Observe the LED turning ON and OFF based on the measured distance.

### Using Physical Hardware

1. Complete all circuit connections.
2. Open the Arduino IDE.
3. Select **Arduino UNO** as the board.
4. Select the correct COM port.
5. Upload the code.
6. Open the Serial Monitor at **9600 baud**.

## 🚀 Future Improvements

- Add a buzzer for audio alerts
- Display distance on an LCD or OLED screen
- Send notifications using ESP8266/ESP32
- Upload sensor data to ThingSpeak
- Add multiple sensors for wider coverage

## 📚 Applications

- Obstacle avoidance robots
- Smart parking systems
- Automatic doors
- Distance measurement devices
- Security systems


