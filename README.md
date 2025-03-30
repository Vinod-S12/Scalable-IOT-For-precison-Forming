#include <DHT.h>
#define DHTPIN 7    // Pin connected to the DHT11 sensor
#define DHTTYPE DHT11 // Type of DHT sensor
DHT dht(DHTPIN, DHTTYPE);
#define IN1 8
#define IN2 9
#define IN3 10
#define IN4 11
 int pump = 6;


void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);

  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);
  pinMode(pump, OUTPUT);
    digitalWrite(pump,HIGH);
       pinMode(A0,INPUT);
 dht.begin();


}

void loop() {
  // put your main code here, to run repeatedly:
  int soil = analogRead(A0);
soil = map(soil,0,1024,100,0);
Serial.print("soil: ");
Serial.println(soil);
float humidity = dht.readHumidity();
float temperature = dht.readTemperature();

      // Check if any errors occurred while reading the sensor
      if (isnan(humidity) || isnan(temperature)) {
        Serial.println("Failed to read data from DHT11 sensor");
        return;
      }

        // Print the temperature and humidity to the serial monitor
      Serial.print("Temperature: ");
      Serial.println(temperature);
      
      Serial.print("Humidity: ");
      Serial.print(humidity);
      Serial.println(" %");
if(Serial.available()>0){
        String motiondata=Serial.readString();
        int direction = motiondata.toInt();
        if(direction==1){
          carforward();
        }
         if(direction==2){
         carbackward();
        
        }
         if(direction==3){
        carturnleft();
        }
         if(direction==4){
         carturnright();
        }
        if(direction==5){
          carStop();
        }
         if(direction==6){
          pumpon();
        }
         if(direction==7){
          
           pumpoff();
        }

}

}

void carforward() {

  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
}
void carbackward() {

  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}
void carturnleft() {

  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}
void carturnright() {

  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
}
void carStop() {
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);
}

void pumpon(){
digitalWrite(pump,LOW);

}
void pumpoff(){
digitalWrite(pump,HIGH);

}
