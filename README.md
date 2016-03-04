# Arduino-nano-ile-park-sens-r-proje-kodlar-

 #include <LiquidCrystal.h>
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
const int echo = 8;
const int trig = 9;
int sure = 0;
int mesafe = 0;

void setup() {
  pinMode(trig, OUTPUT);
  pinMode(echo, INPUT );
  pinMode(10, OUTPUT);
  pinMode(7, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(13, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  lcd.begin(16, 2);
  lcd.clear();
  digitalWrite(trig, HIGH);
  delayMicroseconds(1000);
  digitalWrite(trig, LOW);
  //----------------------
  sure = pulseIn(echo, HIGH);
  mesafe = (sure / 2) / 29.1;
  Serial.print("Mesafe: ");
  Serial.println(mesafe);
  Serial.print("Cm ");
  lcd.setCursor(0, 0);
  lcd.print(">> Mesafe= ");
  lcd.setCursor(0, 1);
  lcd.print(mesafe);
  lcd.print("  cm ");
  if (mesafe > 10) // cm cinsinden
  {
    digitalWrite(7, HIGH );
    digitalWrite(10, LOW );
    digitalWrite(13, LOW );
    analogWrite(6, 0);

  }
  if (mesafe >= 5 && mesafe <= 10) // cm cinsinden
  {
    digitalWrite(7, LOW );
    digitalWrite(10, LOW );
    analogWrite(6, 50);
    digitalWrite(13, HIGH);
    delay(1000);
    digitalWrite(13, LOW);
    delay(1000);
  }
  if (mesafe < 5) // cm cinsinden
  {
    digitalWrite(7, LOW );
    digitalWrite(13, LOW );
    analogWrite(6, 250);
    digitalWrite(10, HIGH);
    delay(100);
    digitalWrite(10, LOW);
    delay(100);
  }

  delay(500);
}
