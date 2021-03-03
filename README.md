# Manipulator
include <Servo.h>
Servo myservo; 
int resultInt; 
int x; 
int z;

void setup() {
    myservo.attach(10);
    Serial.begin(9600);
}
void loop() {
    if (Serial.available()>0) {
        delay(7);
    }
    resultInt = serReadInt();
//    Serial.println(resultInt);
//    z=char(resultInt);
//    Serial.println(resultInt);
    x=myservo.read();
    switch (resultInt) {
        case 1: 
            myservo.write(x+=20);
            Serial.println(resultInt);
            resultInt = 0;
            break;
        case 2:
            myservo.write(x-=20);
            Serial.println(resultInt);
            resultInt = 0;
            break;
        default:
            Serial.println("stopped");
            break;
        delay(1000);
    }
}

int serReadInt() {
    int i, serAva;
    char inputBytes [7]; 
    char * inputBytesPtr = &inputBytes[0]; 
    if (Serial.available() > 0); 
    {
        delay(7);
        serAva = Serial.available(); 
        for (i=0; i<serAva; i++) {
            inputBytes[i] = Serial.read();
        }
        inputBytes[i+1] = '\0';
//        Serial.println(inputBytes[i]);
        memset(inputBytes, serAva, '\0');
        
        return atoi(inputBytesPtr);
    }
}
