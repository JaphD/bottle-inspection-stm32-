# bottle-inspection-stm32

A simulated quality control system for beverage bottling lines using the **STM32F103C6** microcontroller.  
This project demonstrates a complete embedded system that **inspects bottles**, **displays real-time feedback**, and **diverts defective units**, all within a virtual environment using **Proteus** and **UART terminal output**.

---

## 🚀 Features

- **Water Level Sensing Simulation (ADC)**  
  A potentiometer connected to an ADC pin simulates a water level sensor.  
  The MCU reads the water level during the bottle inspection phase.

- **UART Status Display**  
  Displays real-time messages such as:
  - "Bottle Filling"
  - "Bottle Checking"
  - "Process Halted"
  - "Process Resumed"  
  These are viewable on a UART virtual terminal in Proteus.

- **16x2 LCD Feedback (I2C)**  
  Displays whether a bottle was **ACCEPTED** or **REJECTED** after inspection.  
  The second line shows counters for accepted and rejected bottles.

- **Defect Diversion Using PWM Servo**  
  A servo motor controlled via PWM diverts rejected bottles.  
  A **motor driver module** is included to interface the servo with the STM32 safely.

- **Emergency Halt via Interrupt**  
  A push-button connected to an external interrupt (EXTI) halts the system:
  - While pressed, UART displays "Process Halted", and all activity stops.
  - When released, UART displays "Process Resumed", and operation continues.

---

## 🧰 Components (Simulated in Proteus)

- STM32F103C6 (Blue Pill MCU)
- Potentiometer (simulating analog water level)
- 16x2 LCD with I2C module
- Servo Motor 
- Motor Driver (e.g., ULN2003 or similar)
- Push Button (for EXTI interrupt)
- UART Virtual Terminal (in Proteus)
- 5V power supply

---

## 🔧 How the System Works

1. **Idle State**  
   System runs continuously, checking for simulated bottle input.

2. **Bottle Filling Phase**  
   UART shows "Bottle Filling" while ADC reads the water level from the potentiometer.

3. **Bottle Checking Phase**  
   System determines if the fill level is acceptable.

4. **Decision & Output**  
   - **Accepted:** LCD displays "ACCEPTED", and the accepted count is incremented.
   - **Rejected:** LCD displays "REJECTED", rejected count is incremented, and the servo (via driver) diverts the bottle.

5. **Emergency Button**  
   - When pressed: System halts, and UART shows "Process Halted".
   - When released: System resumes, and UART shows "Process Resumed".

---

## 📁 Project Structure

```plaintext
bottle-inspection-stm32/
├── bottle_inspection.pdsprj      # Proteus project file
├── schematic.pdschematic         # Proteus schematic file
├── main.c                        # STM32 firmware source code
├── program.hex                   # Compiled firmware for Proteus simulation
├── lcd_lib.h                     # LCD driver library (by Fatay)
├── lcd_config.h                  # Pin configuration for the LCD
├── README.md

▶️ How to Run the Simulation in Proteus
Open the Project

Launch bottle_inspection.pdsprj in Proteus.

Load the HEX File

Double-click the STM32 MCU.

In Edit Properties, set the program file to program.hex.

Run the Simulation

Press Play in Proteus.

Rotate the potentiometer to simulate different water levels.

Use the push button to test halt/resume functionality.

🧾 Credits
lcd_lib.h was written by Fatay — a lightweight custom driver library for 16x2 LCDs.

Minor adaptations were made to integrate it with this STM32F103C6 project.

GPIO assignments are managed in lcd_config.h.

