🚦 Advanced Railway Gate Tracking System

This project is an IoT-based Railway Gate Monitoring System designed to automatically track and display the gate status (Open/Closed) and location using an ESP8266 microcontroller, GPS module, and LCD display. It also hosts a web interface where users can view the real-time status and GPS coordinates.

🧠 Project Overview

The Advanced Railway Gate Tracking System enhances railway safety and efficiency by monitoring the gate position and broadcasting its status online.
It uses a Wi-Fi-enabled microcontroller (ESP8266) to send live data to a web page and an LCD display for local status updates.

⚙️ Features

🚉 Real-time Gate Status Monitoring (Open/Closed)

🌍 GPS Location Tracking

🌐 Web-based Interface showing live gate status

📟 LCD Display for instant local feedback

📶 Wi-Fi Connectivity using ESP8266

🧩 Simple and low-cost hardware implementation
🪛 Hardware Components
Component	Description
ESP8266 NodeMCU	Wi-Fi-enabled microcontroller
TinyGPS++ Module	For obtaining latitude and longitude
LCD Display (16x2)	To show gate status and GPS data
Push Button	Simulates gate open/close control
Breadboard & Jump Wires	For connections and testing
🧩 Circuit Connections
Component	ESP8266 Pin
GPS RX	D1
GPS TX	D2
Button	D3
LCD RS	D7
LCD EN	D6
LCD D4	D5
LCD D5	D0
LCD D6	A0
LCD D7	D1
💻 Software Requirements

Arduino IDE

ESP8266 Board Package

Libraries:

ESP8266WiFi.h

ESP8266WebServer.h

TinyGPS++.h

LiquidCrystal.h

🔧 Setup Instructions

Install the required libraries in Arduino IDE.

Select the board: NodeMCU 1.0 (ESP-12E Module) under Tools → Board.

Connect your NodeMCU via USB.

Update Wi-Fi credentials in the code:

const char* ssid = "project";
const char* password = "12345678";


Upload the code to your ESP8266.

Open Serial Monitor (baud rate: 9600) to see the assigned IP address.

Access the web interface by entering that IP address in your browser.

🌐 Web Interface

The hosted webpage displays:

Current Gate Status: Open / Closed

Current GPS Location: Latitude, Longitude

Example output:

Status: Closed
Location: 16.4821, 80.6914

🧾 Working Principle

The system continuously reads GPS data.

When the button is pressed, the gate status changes to Closed.

The LCD and webpage update automatically to reflect the new state.

The GPS coordinates and gate status can be viewed remotely from any Wi-Fi-enabled device.

📊 Applications

Railway crossing safety automation

Smart transportation systems

IoT-based infrastructure monitoring

Remote tracking and reporting

🏆 Project Info

Title: Advanced Railway Gate Tracking System

Type: IoT-based Embedded Project

Developed Under: EPICS Initiative

Selected For: ICCCNT 2025

📚 Contributors

IDAMAKANTI VENKATA NAGA SUMANI

Team EPICS | ICCCNT 2025

📜 License

This project is open source under the MIT License.
Feel free to modify and improve it for educational or research purposes.
