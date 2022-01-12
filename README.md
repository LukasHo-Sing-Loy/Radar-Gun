# Radar-Gun
//It uses PIR sensors to find the speed of objects passing both sensors.

const int PIR1 = 10;
const int PIR2 = 13;
const int ledPin1 = 11;
const int ledPin2 = 12;

int bs1;
int bs2;
int t1;
int t2;

double result1;
double result2;
double result3;
double result4;

void setup() {
  Serial.begin(9600);
  pinMode(PIR1,INPUT);
  pinMode(PIR2,INPUT);
  pinMode(ledPin1,OUTPUT);
  pinMode(ledPin2,OUTPUT);
}

void loop() { 
  int bs1_new = digitalRead(PIR1);
  int bs2_new = digitalRead(PIR2);
 
  if(bs1_new == HIGH && bs1 == LOW){    //If when the sensor reads high, after it was low, it takes the time in milliseconds and turns the light on.
    t1 = millis();
    digitalWrite(ledPin1,HIGH);
  }else{
    digitalWrite(ledPin1,LOW);
  }
      
  if(bs2_new == HIGH && bs2 == LOW){
    t2 = millis();
    digitalWrite(ledPin2,HIGH);
  }else{
    digitalWrite(ledPin2,LOW);
  }

  double result1 = (t1 * .001);    //Time from the first sensor, turned from milliseconds to seconds.
  double result2 = (t2 * .001);    //Same thing but for the second sensor.
  double result3 = abs(result2 - result1);    //Adds both results together, and accounts for if the sensors trip backwards
  double result4 = 16/result3;   //Turns it into inches per second. 
 
  bs1 = bs1_new;
  bs2 = bs2_new;

  Serial.print("Inch/second: ");
  Serial.println(result4);
  delay(1000);
}
