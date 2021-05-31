#include <LiquidCrystal.h>

#include<Servo.h>

int RS=2;

int EN=3;

int DB4=4;

int DB5=5;

int DB6=6;

int DB7=7;

//Pin setup of LCD display
LiquidCrystal lcd(RS, EN, DB4, DB5, DB6, DB7);

//Pins for lighting alerts
int red=13;

int yellow = 12;

int green = 11;

//Pin for the piezo buzzer that is used for sound alert
int sound_alert=9;

//Pin for braking system from servo motor
int braking_system=6;

//Pin for ultrasonic distance sensor
int trigger=10;

int echo=8;

//Servo motor for simulating braking system
Servo servo;

void setup() 
{
  //Set display for LCD
  lcd.begin(16, 2);
  
 //Output mode for LEDs, buzzer and trigger pin
  pinMode(red, OUTPUT);
  
  pinMode(yellow, OUTPUT);
  
  pinMode(green, OUTPUT);
  
  pinMode(trigger, OUTPUT);
  
  pinMode(sound_alert,OUTPUT);
  
  //Input mode for 'echo' for reading pulse of echo pin
  pinMode(echo, INPUT);
  
  //Attach braking system, i.e. servo motor
  servo.attach(braking_system);
}

void loop() 
{
  //To find distance between object and sensor 
  digitalWrite (trigger, HIGH);
  
  delay(10);
  
  digitalWrite (trigger, LOW);
  
  int time=pulseIn (echo, HIGH);
  
  /*The speed of sound from the echo pin will double because the wave travels forward and backward(bounces).
    So, to calculate the distance, we need to divide it by 2 */
  int distance=(time*0.034)/2;
  
  /*First level(safe) of warning - Green LED light glows, slight dip in maximum speed of servo motor.
    There will not be any sound alert since it is a fairly safe distance*/
  if(distance>120 && distance<200)
  {
        lcd.setCursor(0, 0);
    
    	lcd.clear();
    
        lcd.print("Object nearby");
    
   		digitalWrite(green, HIGH);
    
    	digitalWrite(red, LOW);
    
    	digitalWrite(yellow, LOW);
    
    	digitalWrite(sound_alert, LOW);
    
    	int position=0;
    
    	for (position=1;position<=179;position++)
    	{
      		servo.write(position);
          
      		delay(10);
    	}
    	for (position=179;position>=1;position--)
    	{
      		servo.write(position);
    	}

  		
  }
  
  /*Second level of warning- Yellow LED light glows, servo motor slows down considerably
    Sound alert occurs, but with low frequency*/
  else if(distance>=61 && distance<=120)
  {
        lcd.setCursor(0, 0);
    
    	lcd.clear();
    
        lcd.print("Slowing down...");
    
   		digitalWrite(yellow, HIGH);
    
    	digitalWrite(red, LOW);
    
    	digitalWrite(green, LOW);
    
   		digitalWrite(sound_alert, HIGH);
    
    	int position=0;
    
    	for (position=1;position<=179;position++)
    	{
      		servo.write(position);
          
      		delay(30);
    	}
    	for (position=179;position>=1;position--)
    	{
      		servo.write(position);
    	}

  		delay(500);
  }
  
  /*Third level of warning- Red LED light glows, brakes are applied and the motor stops rotating
    Sound alert occurs with high frequency*/
  else if(distance<60)
  {
   	    lcd.setCursor(0, 0);
    
    	lcd.clear();
    
    	lcd.print("Brakes applied");
    
   		digitalWrite(red, HIGH);
    
    	digitalWrite(green, LOW);
    
    	digitalWrite(yellow, LOW);
    
   		digitalWrite(sound_alert, HIGH);
    
    	tone(sound_alert,1000,500);
    
  		delay(500);
  }
  
  /*Any other safe distance from object -> There will be no lighting or sound alert
    Servo motor rotates normally without any reduction in speed*/
  else 
  {
        lcd.setCursor(0, 0);
    
    	lcd.clear();
    
    	lcd.print("No object nearby");
    
    	digitalWrite(red, LOW);
    
    	digitalWrite(yellow, LOW);
    
    	digitalWrite(green, LOW);
    
    	digitalWrite(sound_alert, LOW);
    
    	int position=0;
    
    	for (position=1;position<=179;position++)
    	{
      		servo.write(position);
          
      		delay(5);
    	}
    	for (position=179;position>=1;position--)
    	{
      		servo.write(position);
    	}
    
    	delay(500);
  }    
}