# MENSAJE-CON-LCD

#include <LiquidCrystal.h>                    // libreria para la LCD
char texto;                                   // texto para ingresar 
int i=0;                                      // variable i
String palabra="";                               // variable palabra
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);        //inicializar la librería indicando los pins de la interfaz
 
void setup() 
{
    lcd.begin(16,2);                          //configuracion de la lcd en este caso 16 columnas y 2 filas
    Serial.begin(9600);                       //configuración monitor serie
    Serial.println("INGRESE TEXTO");          //ingrese el usuario texto
}
 
void loop()
  {
    if (Serial.available())                  
      {
        texto=Serial.read();                   // lee el texto ingresado
        palabra+=texto;                        // Obtenemos el tamaño del texto

        if(texto=='-')
          {
             for( ; i<300 ; i++)                // Mostramos entrada texto por la izquierda
              {
                  lcd.setCursor(i, 0);  
                  lcd.print(palabra);          // Escribimos el texto   
                  delay(450);                  // Esperamos
                  lcd.setCursor(i, 0);         //Situamos el cursor
                  lcd.println("");
              }

              for(int i=16; i>=0;i--)          // Desplazamos el texto hacia la derecha
              {
                  lcd.setCursor(i, 1);  
                  lcd.print(palabra);          // Escribimos el texto   
                  delay(450);                  // Esperamos
                  lcd.setCursor(i, 1);         //Situamos el cursor
                  lcd.println("");
              }
   }
  }
 }
