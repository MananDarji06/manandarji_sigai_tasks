# manandarji_sigai_tasks
Task 3: A digital lock system using Arduino, a  breadboard, and 4 pushbuttons

Code:

const int buttonPins[4] = {2, 3, 4, 5};  // Pushbuttons

const int greenLED = 8;

const int redLED = 9;

// Correct passcode sequence

int passcode[4] = {1, 3, 2, 4};

int entered[4];

int index = 0;


void setup() {

  for (int i = 0; i < 4; i++) {

    pinMode(buttonPins[i], INPUT);

  }

  pinMode(greenLED, OUTPUT);

  pinMode(redLED, OUTPUT);

  Serial.begin(9600); // For debugging

}



void loop() {


 
  for (int i = 0; i < 4; i++) {
 
    if (digitalRead(buttonPins[i]) == HIGH) {
 
      entered[index] = i + 1;   // Button 1 → digit 1, etc.
 
      Serial.print("Pressed: ");
  
      Serial.println(i + 1);    // Debugging output
  
      index++;
  
      delay(300);               // Debounce
      
  
      if (index == 4) {
   
        checkPasscode();
   
        index = 0;              // Reset for next attempt
 
      }
 
    }

  }

}



void checkPasscode() {

  bool correct = true;

  for (int i = 0; i < 4; i++) {

    if (entered[i] != passcode[i]) {

      correct = false;

      break;

    }

  }



  if (correct) {

    Serial.println("Access Granted!");

    for (int i = 0; i < 3; i++) {

      digitalWrite(greenLED, HIGH);

      delay(300);

      digitalWrite(greenLED, LOW);

      delay(300);

    }

  } 
  
  else {
 
    Serial.println("Access Denied!");

    for (int i = 0; i < 3; i++) {

      digitalWrite(redLED, HIGH);

      delay(300);

      digitalWrite(redLED, LOW);

      delay(300);
 
    }
 
  }

}
