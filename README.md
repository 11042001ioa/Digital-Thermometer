#include <LiquidCrystal_I2C.h> 
#include <Wire.h> 
LiquidCrystal_I2C lcd(0x27,16,2); 
#define sensor A0//we define the sensor 
byte degree_symbol[8] =// the degree symbol is created using the custom 
character symbol 
{ 
0b00111, 
0b00101, 
0b00111, 
0b00000, 
0b00000, 
0b00000, 
0b00000, 
0b00000 
}; 
void setup() 
{ 
Serial.begin(9600); 
lcd.init(); 
lcd.backlight(); 
pinMode(3,INPUT); 
pinMode(4,OUTPUT); 
digitalWrite(4,HIGH); 
lcd.createChar(1, degree_symbol); 
lcd.setCursor(0,0); 
lcd.print("Temp. Sensor "); 
} 
void loop() 
{  
float reading=analogRead(sensor); 
float temperature=reading*(5.0/1023.0)*100;//formula pt a converti din 
analog in digital 
delay(10); 
digitalWrite(4,HIGH); 
lcd.setCursor(0,1); 
lcd.print(temperature); 
lcd.write(1); 
lcd.print("C"); 
lcd.setCursor(8,1); 
lcd.print((temperature* 9)/5 + 32); //turning the celsius into fahrehait 
lcd.print("F"); 
delay(1000); 
} 
