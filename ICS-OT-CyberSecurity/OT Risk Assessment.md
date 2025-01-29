# OT Risk Assessment

It is the process of identifying, analyzing, and evaluating risks associated with operational technology systems. OT systems include hardware and software that control industrial processes, such as SCADA (Supervisory Control and Data Acquisition), PLCs (Programmable Logic Controllers), DCS (Distributed Control Systems), and other equipment used in industries like manufacturing, energy, transportation, and utilities.

The goal of an OT risk assessment is to ensure the safety, security, and reliability of critical systems by identifying potential vulnerabilities and threats and implementing measures to mitigate risks.
 
## System under consideration (**SUC**)
![Image](https://github.com/user-attachments/assets/09d6f5bb-66bd-476e-ac99-5416373038a2)

### Importance of Risk Assessment in OT
- Indentify Vulnerabilty
- Evaluating Threat Landscape
- Understanding Consequences:
    -  Direct harm to human life
    - Enviromental damage
    - financial loss
### Process of Risk Assessment
* Identifying Assets and systems
* Treat Modeling
* Vulnerability Analysis (Tools and methods)
*  Impact Assessment.

### Approaches and Best Practices
* Utilizing Frameworks and Standards
     - NIST Special Publication 800-30
     - IEC 62443-3-2
     - ISO 31000:2018
     - ISO/IEC 27005:2011 
* Create a Multidisciplinary Team (Collaboration between IT, OT, and management).
* Make continuous Monitoring and Mitigation Strategies

### What is Risk ?

     Risk = Threat X Vunerability X Consequence

![Image](https://github.com/user-attachments/assets/05d9a595-da4d-47e2-95fd-8131d20dac18)

#### Example of Risk calculation
       Risk = Threat X Vunerability X Consequence

       - SUC (System Under Consideration)
    A car manufacturing plant with automated assembly lines controlled by an Industrial Automation and Control System(IACS)
        - Threat
    Malware infection introduced through a USB device
        - Vunerability
    No restrictions or controls over the use of USB devices in the control systems
        - Consequence
    Disruption or manipulation of the automated assembly lines leading to production halt, faulty manufacturing and potential safety risks

    1. Threat (probability of malware infection):3 (due to common usage of USB device without restriction)
    
    2. Vulnerability (weakness in the system):4 (due to lack of controls over USB usage in  control systems)

    3. Consequence (impact of exploitation):4 (significant potential financial, operational, and safety impacts)

    Then we have:

    Risk = 3 x 4 x 4 = 48 Very high

## Prerequisites 
* Gather information on **System Under Consideration (SUC)**
    - Asset Inventory
    - System Architecture
    - Network Diagrams
* Risk Matrix (depending on each organization)
* Process Hazard Analysis (**PHAs**)/Hazard and Operability Analysis (**HAZOP**)
* Garther **Threat** information
* Garther **Vulnerability Assessment** Report

## Workflow of the Risk Assessment

* Calculate the **Initial Risk** (Unmitigated Risk)
    - Risk = Threat X Vunerability X Consequence
* Put Countermeasure
    - Re-calculate the Risk (**Mitigated Risk**)
* Take Decision
    - Additional Countermeasures 
    - Accept risk 
    - discard risk
    - Transfer the risk
## System under consideration (**SUC**)
![Image](https://github.com/user-attachments/assets/09d6f5bb-66bd-476e-ac99-5416373038a2)

## IEC 62443-3-2 Standards: Detailed Risk Assessment in IACS
![Image](https://github.com/user-attachments/assets/99d84743-48ec-47ef-928a-49dcde1d5c64)
![Image](https://github.com/user-attachments/assets/5ac1dc05-b1da-4f11-9972-554395bf18ea)
### Asset Inventory

![Image](https://github.com/user-attachments/assets/3f06039a-1463-419b-a677-59c1c8b5161c)
### Risk Assessment Matrix

![Image](https://github.com/user-attachments/assets/1794cf81-942b-4d77-a9f5-a6bc2500c11d)

### Scoring
![Image](https://github.com/user-attachments/assets/03175200-e4ce-47ae-9a9b-8541e8dbe093)

## Risk assessment
![Image](https://github.com/user-attachments/assets/963324d4-1dec-4b61-a20d-03e58db07206)