
# bengala-especial

   #include<Ultrasonic.h>



#define trigger_pin 11 //saida
#define echo_pin 12 // entrada
int buzzer=10;
int led=8;      // led no pino 13
int botao=9;  // botão no pino 12
int var=0;       // valor instantaneo enviado pelo botão
int var2=0;     // valor guardado
int estado=0;  // guarda o valor 0 ou 1 (HIGH ou LOW)
 float cmMsec=0;
Ultrasonic ultrasonic(trigger_pin,echo_pin);
void setup()
{
  pinMode(led,OUTPUT);
  pinMode(botao,INPUT);
  pinMode(trigger_pin,OUTPUT);
  pinMode(echo_pin,INPUT);
  pinMode(buzzer,OUTPUT);
  Serial.begin(9600);
}
void loop()
{

  long microsec = ultrasonic.timing();
  var=digitalRead(botao); // ler o valor enviado pelo botão: "HIGH" ou "LOW"
  digitalWrite(8,LOW);
  Serial.println(cmMsec);

  
 
   if ((var == HIGH) && (var2 == LOW))
  {
    estado = 1 - estado;
    delay(20); // de-bouncing
    tone(buzzer,1000);
    delay(500);
    noTone(buzzer);
  }

   
  var2=var;
  
   
  
  if (estado == 1)
  {
    digitalWrite(led, HIGH); // liga o led
    cmMsec = 0;
    cmMsec = ultrasonic.convert(microsec, Ultrasonic::CM);
    Serial.print(" CM:  ");
    Serial.print(cmMsec);
    Serial.print("\n");
    digitalWrite(10,LOW);

 
   
  if (cmMsec >= 1 && cmMsec< 30)
  {
    for(int i=0;i<3;i++)
    {
      tone (buzzer,10);
      delay(100);
      noTone(buzzer);
   
    }
    
    Serial.println("Entrei no 1");
    
  }

 if (cmMsec >= 30 && cmMsec < 60 )
  {
    for(int i=0;i<3;i++)
    {
      tone (buzzer,10);
      delay(500);
      noTone(buzzer);
      delay(500);
   
    }
  Serial.println("Entrei no 30");
  }


   if (cmMsec >= 60 && cmMsec <=100)
  {
    for(int i=0;i<2;i++)
    {
      tone (buzzer,10);
      delay(1000);
      noTone(buzzer);
      delay(1000);

    }
   Serial.println("Entrei no 50");
  }
 }

  else
  {
    noTone(buzzer);
    digitalWrite(led,LOW);
  }
  }
