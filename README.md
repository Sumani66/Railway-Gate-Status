# Railway-Gate-Status
#include <ESP8266WiFi.h>
#include <ESP8266WebServer.h>
#include <TinyGPS++.h>
#include <LiquidCrystal.h>

// Wi-Fi credentials
const char* ssid = "project";
const char* password = "12345678";

// Web server setup
ESP8266WebServer server(80);

// GPS and button setup
TinyGPSPlus gps;
// RX (D1), TX (D2) for GPS module
const int buttonPin = D3;          // Button connected to D3

// LCD setup (adjust the pins according to your wiring)
const int rs = D7, en = D6, d4 = D5, d5 = D0, d6 = A0, d7 = D1;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

void setup() {
  Serial.begin(9600);

  pinMode(buttonPin, INPUT_PULLUP);  // Button set as input with pull-up resistor
  
  // Initialize the LCD
  lcd.begin(16, 2);
  lcd.print("Connecting...");

  // Connect to Wi-Fi
  WiFi.begin(ssid, password);
  Serial.print("Connecting to Wi-Fi...");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nConnected!");
  
  // Print IP address
  Serial.print("IP Address: ");
  Serial.println(WiFi.localIP());

  // Display Wi-Fi status on LCD
  lcd.clear();
  lcd.print("WiFi Connected");
  lcd.setCursor(0, 1);
  lcd.print("IP: ");
  lcd.print(WiFi.localIP());

  // Set up web server routes
  server.on("/", handleRoot);
  server.begin();
  Serial.println("Web server started.");
}

void loop() {
  server.handleClient();

  // Update GPS data
  while (Serial.available() > 0) {
    gps.encode(Serial.read());
  }

  // Update LCD with GPS info if available
  if (gps.location.isValid()) {
    lcd.clear();
    lcd.print("Location:");
    lcd.setCursor(0, 1);
    lcd.print(gps.location.lat(), 6);
    lcd.print(",");
    lcd.print(gps.location.lng(), 6);
  } else {
    lcd.clear();
    lcd.print("Location:");
    lcd.setCursor(0, 1);
    lcd.print("Acquiring...");
  }

  // Display gate status on LCD based on button state
  if (digitalRead(buttonPin) == LOW) {  // Button pressed
    lcd.clear();
    lcd.print("Gate Status:");
    lcd.setCursor(0, 1);
    lcd.print("Closed");
  } else {
    lcd.clear();
    lcd.print("Gate Status:");
    lcd.setCursor(0, 1);
    lcd.print("Open");
  }
}

// Web server root handler
void handleRoot() {
  String page = "<html><head>";
  page += "<style>";
  page += "body { font-family: Arial, sans-serif; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; background-color: #f4f4f9; }";
  page += "h1 { font-size: 3em; color: #333; text-align: center; }";
  page += "p { font-size: 2em; color: #555; text-align: center; }";
  page += "</style>";
  page += "</head><body>";
  page += "<div>";
  page += "<h1>Railway Gate Status</h1>";
  
  // Display "Closed" if button is pressed, otherwise "Open"
  if (digitalRead(buttonPin) == LOW) {
    page += "<p>Status: <strong>Closed</strong></p>";
  } else {
    page += "<p>Status: <strong>Open</strong></p>";
  }

  // GPS information
 
    page += "<p>Location: <strong>" + String(16.4821) + ", " + String(80.6914) + "</strong></p>";
  

  page += "</div>";
  page += "</body></html>";

  server.send(200, "text/html", page);
}
