# Arduino-HBridge-L298n

![LNa](https://github.com/ICAREMAKER/Arduino-HBridge-LN298n/assets/107696317/a7abafc2-93a1-4f82-9c95-3fbf4ea08760)
![LN](https://github.com/ICAREMAKER/Arduino-HBridge-LN298n/assets/107696317/f80e77cf-6318-4ef7-9e9f-3ea6d60af4d5)


## Code
```C
//Ports de commande du moteur 
int motorAPin1 = 8;
int motorAPin2 = 9;
int vitessePin = 5;
 
// Vitesse du moteur
int vitesse = 0;
/*
Le programme permet de mettre en mouvement le moteur connecté 
au pont A en passant par le port série.
Par l’intermédiaire du moniteur série, on envoie un entier entre -255 et 255 
pour actionner le moteur, la valeur 0 signifiant « arrêt du moteur ».
*/


void setup() {
    // Configuration des ports en mode "sortie"
    pinMode(motorPin1, OUTPUT);
    pinMode(motorPin2, OUTPUT);
    pinMode(enablePin, OUTPUT);
    
    // Initialisation du port série
    Serial.begin(9600);
}
 
void loop() {
    if (Serial.available() > 0)
    {
      // Lecture de l'entier passé au port série
     vitesse = Serial.parseInt();

      //
      // Sens du mouvement
      //
      if (vitesse > 0) // avant
      {
        digitalWrite(motorAPin1, HIGH); 
        digitalWrite(motorAPin2, LOW);
        Serial.print("Avant");
        Serial.println(vitesse);
      }
      else if (vitesse < 0) // arrière
      {
        digitalWrite(motorPin1, LOW); 
        digitalWrite(motorPin2, HIGH);
        Serial.print("Arriere");
        Serial.println(vitesse);
      }
      else // Stop (freinage)
      {
        digitalWrite(motorPin1, HIGH); 
        digitalWrite(motorPin2, HIGH);
        Serial.println("Stop");
      }

      // Vitesse du mouvement
      
      analogWrite(vitessePin, abs(vitesse));
    }
    delay(100);
}
```
