# Attacking ICS Plant
![Image](https://github.com/user-attachments/assets/5848bca1-4525-4aad-9b1c-96f45e389472)

## Introduction to OT/ICS

**Operational Technology (OT)** and **Industrial Control Systems (ICS)** are critical components in managing and controlling industrial processes and infrastructure. **OT** refers to the hardware and software used to change, monitor, or control physical devices, processes, and events in the enterprise. **ICS** is a major segment within OT, specifically designed to manage and automate industrial processes.

### Key Components of ICS:
1. **Supervisory Control and Data Acquisition (SCADA)**

1. **Distributed Control Systems (DCS)**

3. **Programmable Logic Controllers (PLC)**

4. **Human-Machine Interface (HMI)**

8. **Remote Terminal Units (RTU)**

## Introduction to Modbus protocol

**Modbus protocol** is a widely used communication protocol in the field of **Industrial Automation and Control Systems(IACS)**. Developed in 1979 by Modicon (now Schneider Electric) for use with its Programmable Logic Controllers (PLCs), Modbus has become a de facto standard for communication between industrial electronic devices. It is known for its simplicity, openness, and ease of use.

**Modbus protocol** is a master/slave protocol: the master reads and writes slaves' registers.

Modbus RTU is usually used via **RS-485** (serial network): one master is present with one or more slaves. Each slave has an unique **8-bit address**. 

Modbus data is used to read and write **"registers"** which are 16-bit long. The most common register is called **"holding register"** which is **readable and writable**; registry type "input register" is readable only. The registers **"coil"** and **"discrete input"** are 1-bit long: coils are readable and writable, **discrete inputs** are readable only.

**Modbus register types:**
* Discrete Input (Status Input): 1bit, RO

* Coil (Discrete Output): 1bit, R/W

* Input Register: 16bit, RO

* Holding Register: 16bit R/W

**Question 1 :** Which is the function used to read holding registers in pymodbus library?

![Image](https://github.com/user-attachments/assets/256715b6-36a3-47dd-8961-eb016e27df49)

      Answer : read_holding_registers

**Question 2 :** Which is the function used to write holding registers in pymodbus library?

![Image](https://github.com/user-attachments/assets/cf4786ba-55f0-4ea2-8f57-ea73ad08b235)

      Answer : write_register

## Discovery : VirtuaPlant

**VirtuaPlant** is a Industrial Control Systems simulator which adds a “similar to real-world control logic” to the basic “read/write tags” feature of most **PLC simulators**. Paired with a game library and 2d physics engine, VirtuaPlant is able to present a GUI simulating the “world view” behind the control system allowing the user to have a vision of the would-be actions behind the control systems.

![Image](https://github.com/user-attachments/assets/62eb0d22-60b1-43dc-8c5b-76c700ed42e4)

**We have three phases:**

1. **Initialization**: the plant is starting from the beginning. The roller moves the first bottle under the nozzle.

2. **Filling**: once a bottle is under the nozzle, the nozzle opens and the water flows in the bottle.

3. **Moving**: once the bottle is filled, the roller starts again moving the next empty bottle under the nozzle.

When the **phase 3** ends, the plant starts again with **phase 2**.

From the three phases described above, we can observe:

* **Sensors**: used to read a state of the plant.

* **Actuators**: used to alter the state of the plant.

### Example: 
A sensor can detect if a bottle is under the nozzle, while an actuator can open or close the nozzle.

**Question 1:** How many phases can we observe?

      Answer : 3

**Question 2:** How many sensors can we observe? 

      Answer : 2

**Question 3:** How many actuators can we observe?

      Answer : 3

**Question 4 :** Using the script discovery.py, how many registers can we count?
![Image](https://github.com/user-attachments/assets/90ef4ffa-b12f-4560-80d7-cb71d8d4e47b)
![Image](https://github.com/user-attachments/assets/e7e8cfbc-33c8-4188-abed-d72b53464ee9)

        Answer : 16

**Question 5:** After the plant is started and a bottle is loaded, how many registers are continuously changing their values?
![Image](https://github.com/user-attachments/assets/4cd4ace1-6e1e-46aa-adfa-d55f7ddeb6dd)

        Answer : 4

**Question 6:** Which is the minimum observed value?

        Answer : 0

**Question 7:** Which is the maximum observed value?

        Answer : 1
**Question 8:** Which registry is holding its value?
![Image](https://github.com/user-attachments/assets/6796c883-50ff-43be-8d4e-c38551072f10)

        Answer : 16

**Question 9:** Which registries are set to 1 while the nozzle is filling a bottle?

![alt text](image.png)

        Answer :   2  4

**Question 10:** Which registries are set to 1 while the roller is moving the bottles?
![Image](https://github.com/user-attachments/assets/d075b802-ecd9-43c5-80b0-e613fb19c301)

        Answer :   1  3

**Question 11:** Which is the color of the water level sensor?

        Answer :   red
**Question 12:** Which is the color of the bottle sensor?

        Answer :   green

**Question 13:** If you observe the plant at the very beginning, which is the registry associated with the roller?

![Image](https://github.com/user-attachments/assets/ae02d435-d818-41e0-aa9e-a7ea94fb167b)

        Answer :   3
**Question 14 :** Based on the previous answer, which is the registry associated with the water level sensor?
![Image](https://github.com/user-attachments/assets/000803e6-c0d0-42e6-b773-81e5d6cd5cc9)

        Answer :   1


## So far let talk about **registries**:

* **Bottle-filling plant** exposes **16 registries**, but only 5 are used.

* **Registry 16** is associated with the **start/stop button**: **1** means plant is on, **0** means plant is off.
* **Registries 1 and 3** usually have the same value, except in the initialization phase.
* **Registries 2 and 4** always have the same value.


### We observed three phases, and the associated registries are:

* **Initialization**: [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1]

* **Filling**: once a bottle is under the nozzle, the nozzle opens and the water flows in the bottle.
* **Moving**: once the bottle is filled, the roller starts again moving the next empty bottle under the nozzle.

### We also assumed the plant has two sensors and three actuators. 

**Actuators:**

- **Start/stop button:** registry 16.
* **Roller engine:** registry 3.
- **Nozzle:**  registry 2 or 4. 

**Sensors:**

* **Water level:** 1 (red sensor)
* **Bottle position:** 2 or 4 (green sensor). 

## Review

**Registry 1**: associated with the bottle sensor. Value is 1 if the bottle is under the nozzle.

**Registry 2:** associated with the water level sensor. Value is 1 if the bottle is filled.

**Registry 3:** associated with the roller actuators. Value 1 turns the roller on.

**Registry 4:** associated with the nozzle. Value 1 opens the nozzle.

**Registry 16:** associated with the plant. Value 1 starts the plant