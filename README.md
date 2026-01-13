# The Pit Wall – Arduino F1 Manager Game

## 1. Description
**The Pit Wall** is an F1 Manager simulation game built on Arduino that puts the player in the role of a **Team Principal**. You are given full control over one of the 10 official teams from the 2025 season, with the possibility of unlocking a secret 11th team: **ApexGP**.

Throughout a career spanning **10 seasons**, you are directly responsible for your team’s destiny:

- **Management:** Manage the team budget, develop car upgrades, and oversee driver contracts and morale.
- **Strategy:** Make critical, real-time decisions during races, including tire compounds, pit stops, and team orders.
- **Adaptation:** Face periodic regulation changes that can disrupt the competitive order, forcing you to rethink your technical strategy from scratch.

Inspired by the strategic depth of *Motorsport Manager* and *F1 Clash*, **The Pit Wall** challenges you to complete all **24 rounds** of the Formula 1 calendar, following the real-world structure of Practice, Qualifying, and Race sessions.

---

## 2. Key Features

### Team Management
You control the economy and long-term evolution of your team.

- **Transfer Market:** Manage a dedicated budget used for negotiating contracts and exchanging drivers with other teams.
- **R&D Progression:** Earn Upgrade Points based on race results. Reinvest them to permanently improve car performance (Aerodynamics, Power) or driver attributes.

### Race Strategy
Race results are calculated by a dynamic simulation formula, and you control the key variables.

- **Pace Modes:** Adjust lap-time behavior in real time.  
  - *Push:* Faster lap times at the cost of higher tire wear and error risk.  
  - *Conserve:* Slower pace but extended tire life.
- **Tire Physics:** As tires degrade, lap times increase. You must decide the optimal pit window before performance drops too far.
- **Weather System:** Track conditions can shift between Dry and Wet, requiring immediate strategic reactions.

### Career Mode
A long-term simulation spanning **10 full seasons**.

- **Regulation Changes:** Every three seasons, the FIA introduces new technical regulations. These reset performance points across the grid, affecting top teams more heavily and allowing midfield teams to close the gap.

### Time Dilation & Flow Control
You control the flow of time itself.

- **Strategy Freeze:** A dedicated pause button instantly freezes the simulation, allowing you to analyze the situation without time pressure.
- **Variable Simulation Speed:** Using a gesture-based ultrasonic sensor, you can fast-forward through uneventful laps or return to normal speed to observe critical moments.

---

## 3. Hardware Architecture

- **Microcontroller:** Arduino Mega 2560  
  *(Chosen for its higher memory capacity required by the 10-season career database)*
- **Display:** 3.5" TFT LCD Shield (480×320 resolution)  
  *(Acts as the main “Pit Wall” race monitor and UI)*
- **Input:** Joystick for menu navigation and live race commands
- **Audio:** Buzzer for race alerts and UI feedback
- **Push Button:** Dedicated “Strategy Pause” button to freeze race logic
- **Ultrasonic Sensor (HC-SR04):**  
  Acts as a “Time Warp” controller. Bringing your hand closer accelerates the simulation, while removing it returns the game to normal speed.
- **Data Persistence:** EEPROM  
  Automatically saves career progress after each race event (season, budget, standings), allowing long-term play sessions to be resumed.

---

## System Design Questions

### Q1 – What is the system boundary?
The system is fully contained within the **Arduino Mega 2560**.

- **Inside the system:**  
  Microcontroller, TFT LCD shield, joystick, ultrasonic sensor, buzzer, and game firmware.
- **Outside the system:**  
  The user.

---

### Q2 – Where does intelligence live?
All intelligence lives **entirely on the device**, centralized on the microcontroller.  
Race calculations, user input handling, game logic, and graphics rendering are all processed locally without external computation.

---

### Q3 – What is the hardest technical problem?
**Graphics rendering and memory optimization.**  
The simulation tracks many variables simultaneously (cars, tire wear, weather, race state) while maintaining smooth rendering on the TFT display. This must be achieved within the limited SRAM and processing speed of the Arduino Mega, without screen flickering or performance drops.

---

### Q4 – What is the minimum demo?
The minimum demo is a **playable race simulation**.  
The user must be able to observe cars on track, modify race variables such as tire wear and pace mode, and clearly see the impact of these decisions on race outcomes.

---

### Q5 – Why is this not just a tutorial?
This is not a tutorial-based project because it involves designing a custom simulation engine that supports real-time user interaction, race logic, and persistent career progression.  
It also requires creating an intuitive interface for both race control and long-term management within the constraints of an embedded platform.
