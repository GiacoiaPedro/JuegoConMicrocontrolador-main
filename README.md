# 🔐 Recordar la Contraseña - Juego Interactivo con Atmega328P

Este proyecto implementa un juego interactivo llamado **"Recordar la Contraseña"**, diseñado para funcionar sobre un microcontrolador **Atmega328p**, utilizando un **display LCD 2x16**, un **teclado matricial 4x4**, e interrupciones de **Timer**. El objetivo del juego es memorizar y luego ingresar correctamente una palabra aleatoria de 5 caracteres seleccionada desde un diccionario. 
El codigo fue testeado y cargado sobre un atmega328P fisico, pero las simulaciones se llevaron a cabo usando PROTEUS.

---

![image](https://github.com/user-attachments/assets/2ae61d05-9dc4-4d52-8ea0-4eb8a96bff63)



## 🎯 Objetivo del Juego

1. Al presionar la tecla `*`, el sistema selecciona una palabra aleatoria del diccionario.

2.  ![image](https://github.com/user-attachments/assets/a5c29450-d418-47fc-aa1e-45edebd6cbcd)

3. La palabra se muestra durante 2 segundos en el LCD.

4. ![image](https://github.com/user-attachments/assets/e6dbb320-4a10-4be3-a6bd-6f0050354520)

5. Luego de desaparecer, el jugador debe ingresar la palabra carácter por carácter usando el teclado en cifrado ASCII.
6. Cada letra ingresada se confirma con la tecla `#`.

7. ![image](https://github.com/user-attachments/assets/e99b35f6-6981-4698-b8fc-15ca249e9125)

8. Si se ingresa correctamente la palabra:
Se muestra un mensaje de **"victoria"** junto con el tiempo que tomó completarla.

9. ![image](https://github.com/user-attachments/assets/6a507db9-da0f-4d00-9906-9575803cb75a)

10. Si se cometen **3 errores**, se muestra un mensaje de **"derrota"** y se reinicia el juego tras 5 segundos.
    
11. ![image](https://github.com/user-attachments/assets/6dabe98f-8139-4ab0-8359-022351b907c6)

---

## 📦 Estructura del Proyecto

El proyecto está modularizado por archivos:

- `fsm.c / fsm.h` – Lógica principal del juego con una Máquina de Estados Finita (MEF).
- `dict.c / dict.h` – Diccionario de palabras y funciones de selección aleatoria.
- `lcd.c / lcd.h` – Control del display LCD.
- `keypad.c / keypad.h` – Lectura de teclas del teclado matricial 4x4.
- `timer.c / timer.h` – Configuración e interrupción del Timer para temporización.
- `main.c` – Inicialización general y bucle principal.

---

## ⚙️ Requisitos Técnicos

- Microcontrolador: **Atmega328P**
- Display: **LCD 2x16 (HD44780 compatible)**
- Entrada: **Teclado matricial 4x4**
- Compilador: Compatible con **AVR-GCC**
- IDE sugerido: **Microchip Studio**
- Simulador recomendado: **Proteus**

---

## 🧠 Lógica del Juego (MEF)

- **ST_IDLE**: Espera la tecla `*` para comenzar.
- **ST_SHOW_WORD**: Muestra una palabra aleatoria durante 2 segundos.
- **ST_TYPING**: El jugador debe ingresar la palabra, confirmando cada letra con `#`.
- **ST_CHECK**: Verifica si el carácter ingresado es correcto.
- **ST_VICTORY / ST_DEFEAT**: Muestra resultado final y espera 5 segundos antes de reiniciar.

---

## 📚 Diccionario de Palabras

Contiene palabras de 5 letras, incluyendo mayúsculas, minúsculas y combinaciones:

Arbol, Boton, CDyMC, ClavE, Facil, Gafas, Hojas, LiBro, Lanza,
Nieve, PeRro, PecES, PiAno, PrYKe, RUEDa, SERIE, SalUd, Salud,
Silla, Tecla, Valor, Verde, YnHRz, hARdD, silla

Arbol → 65#114#98#111#108#

Boton → 66#111#116#111#110#

CDyMC → 67#68#121#77#67#

ClavE → 67#108#97#118#69#

Facil → 70#97#99#105#108#

Gafas → 71#97#102#97#115#

Hojas → 72#111#106#97#115#

LiBro → 76#105#66#114#111#

Lanza → 76#97#110#122#97#

Nieve → 78#105#101#118#101#

PeRro → 80#101#82#114#111#

PecES → 80#101#99#69#83#

PiAno → 80#105#65#110#111#

PrYKe → 80#114#89#75#101#

RUEDa → 82#85#69#68#97#

SERIE → 83#69#82#73#69#

SalUd → 83#97#108#85#100#

Salud → 83#97#108#117#100#

Silla → 83#105#108#108#97#

Tecla → 84#101#99#108#97#

Valor → 86#97#108#111#114#

Verde → 86#101#114#100#101#

YnHRz → 89#110#72#82#122#

hARdD → 104#65#82#100#68#

silla → 115#105#108#108#97#
---

## 🧪 Simulación en Proteus

Se puede simular el juego usando Proteus con:
- Atmega328p.
- Módulo LCD 2x16 conectado al puerto correspondiente.
- Teclado 4x4 conectado a los pines configurados.
- Oscilador a 16 MHz (recomendado).

---

## 🔁 Temporización

- La MEF se ejecuta mediante una **interrupción periódica de Timer**, no con retardo activo.
- Los tiempos (2s y 5s) se gestionan con una variable de milisegundos (`ticksMS`) incrementada en la ISR del Timer.

---

## ✅ Características Adicionales

- Manejo de errores (máximo 3 fallos).
- Rechazo de caracteres no alfabéticos (contabilizados como error).
- Randomización basada en `ticksMS` para obtener una palabra distinta en cada juego.
- Pantallas adaptadas a cada estado del juego.
