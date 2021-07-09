# Ultrasonic-sensor-with-two-arduino-only
in this project i implemented the first part of the service evaluation robot where it detect the person and if he stay for 3 sec the first arduino will send signal for the second arduino which it will turn on LED


**Tibkercad Link:** https://www.tinkercad.com/things/cTocAe1NpRF-sizzling-hillar-kasi/editel?tenant=circuits


**Circuit diagram:**

![image](https://user-images.githubusercontent.com/5675794/125007797-bd79dc00-e069-11eb-9ae4-60bde9365867.png)


**Code for first arduino:**

```ruby
const int echoPin = 2;
const int trigPin = 3;


long duration;
int distance; 

void setup() {
  pinMode(trigPin, OUTPUT);      // Sets the trigPin as an OUTPUT
  pinMode(echoPin, INPUT);       // Sets the echoPin as an INPUT
  Serial.begin(9600);            // Serial Communication is starting with 9600 of baudrate speed

}
void loop() {

  while(getDistance() > 25){ }

  int startTime = millis(); 
  
  while(getDistance() <25){ 
   int newTime = millis();        //record the current time

  if (newTime - startTime > 3000){ 
    Serial.write("1");            // send message to screen to open
    Serial.println('\n');
    break;                        // get out so only send message once
  }
  }
  
  
  while(getDistance() < 25){ }
}

int getDistance(){                // defining the function to calculate the distance
   
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
 
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;         // Calculating the distance
  
  return distance;
}
```

**Code for second arduino:**

```ruby


void setup()
{
Serial.begin(9600);
  pinMode(12, OUTPUT);
}

void loop()
{
  if(Serial.available() > 0){
  if(Serial.read() == '1')
    digitalWrite(12, HIGH);
    delay(3000);
    digitalWrite(12, LOW);
  }
  
}
```
