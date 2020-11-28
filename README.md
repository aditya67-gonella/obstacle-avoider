# obstacle-avoider


#define SC1 D1 // ena1 pin of motor driver/speed control of motor 1
#define SC2 D2 // ena2 pin of motor driver/speed control of motor 2
#define M1 D5 // motor1 wire 1
#define M2 D6 // motor1 wire 2
#define M3 D7 // motor2 wire 1
#define M4 D8 // motor2 wire 2

#define trigPin D3 //declaring trigger pin
#define echoPin D4 //declaring echo pin

long duration; // declaring variable for storing time 
int distance; // declaring variable for storing distance 

int spd=200;

//....................forward()....................
void forward()
{
  analogWrite(SC1, spd); // writing the speed to left motor
  analogWrite(SC2, spd); // writing the speed to right motor
  // left motor forward direction
  digitalWrite(M1, HIGH);
  digitalWrite(M2, LOW);
  //right motor forward direction
  digitalWrite(M3, HIGH);
  digitalWrite(M4, LOW);
  delay(50);
  Serial.println("FORWARD");
}
//....................backward()....................
void backward()
{
  analogWrite(SC1, spd); // writing the speed to left motor
  analogWrite(SC2, spd); // writing the speed to right motor
  // left motor backward direction
  digitalWrite(M1, LOW);
  digitalWrite(M2, HIGH);
  //right motor backward direction
  digitalWrite(M3, LOW);
  digitalWrite(M4, HIGH);
  delay(50);
  Serial.println("BACKWARD");
}
//....................left()....................
void left()
{
  analogWrite(SC1, spd); // writing the speed to left motor
  analogWrite(SC2, spd); // writing the speed to right motor
  // left motor backward direction
  digitalWrite(M1, LOW);
  digitalWrite(M2, HIGH);
  //right motor forward direction
  digitalWrite(M3, HIGH);
  digitalWrite(M4, LOW);
  delay(50);
  Serial.println("LEFT");
}
//....................right()....................
void right()
{
  analogWrite(SC1, spd); // writing the speed to left motor
  analogWrite(SC2, spd); // writing the speed to right motor
  // left motor forward direction
  digitalWrite(M1, HIGH);
  digitalWrite(M2, LOW);
  //right motor backward direction
  digitalWrite(M3, LOW);
  digitalWrite(M4, HIGH);
  delay(50);
  Serial.println("RIGHT");
}
//....................STOP()....................
void STOP()
{
 
  analogWrite(SC1, spd); // writing the speed to left motor
  analogWrite(SC2, spd); // writing the speed to right motor
  // left motor stop
  digitalWrite(M1, LOW);
  digitalWrite(M2, LOW);
  //right motor stop
  digitalWrite(M3, LOW);
  digitalWrite(M4, LOW);
  delay(50);
  Serial.println("STOP");
}

//.................. ultrasonic().................. 
void ultrasonic()
{
digitalWrite(trigPin, LOW);//Intialize trigpin to low
delayMicroseconds(2);//wait for 2 micro seconds

digitalWrite(trigPin, HIGH); // Sets the trigPin on HIGH state for 10 micro seconds
delayMicroseconds(10);
digitalWrite(trigPin, LOW);// After 10 micro seconds make it low


duration = pulseIn(echoPin, HIGH);// Reads the echoPin, returns the sound wave travel time in microseconds

distance= duration*0.034/2; // Calculating the distance

// Prints the distance on the Serial Monitor
Serial.println("Distance: ");
Serial.print(distance);
delay(100);
}

//....................setup()....................
void setup() {
  pinMode(SC1,OUTPUT);
  pinMode(SC2,OUTPUT);
  pinMode(M1, OUTPUT);
  pinMode(M2, OUTPUT);
  pinMode(M3, OUTPUT);
  pinMode(M4, OUTPUT);
  // initially stop the motor
  digitalWrite(M1, LOW);
  digitalWrite(M2, LOW);
  digitalWrite(M3, LOW);
  digitalWrite(M4, LOW);
  Serial.begin(9600);// Starts the serial communication
  pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
  pinMode(echoPin, INPUT); // Sets the echoPin as an Input
}

//....................loop()....................

void loop() {
  ultrasonic();//calling ultrasonic function  

  if(distance>20)
  {
     forward();
  }
  else
  {
      STOP();//stop the bot
      backward(); //get backward
      delay(1000);
      STOP();//stop the bot
      int i=random(100);// generate random number between 0 to 100
      if(i%2==0)//if the number is even
      {
          left();// turn left
          delay(1000);
          STOP();//stop the bot
    }
    else//if the number is odd
    {
          right();// turn right
          delay(1000);
          STOP();//stop the bot
    }
    
  }
  
 }
 


