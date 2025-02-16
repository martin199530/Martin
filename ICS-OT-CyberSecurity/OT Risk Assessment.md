# OT (Operational Technology) Risk Assessment

It is the process of **Identifying, Analyzing, and Evaluating risks** associated with **Operational Technology** systems. **OT systems** include **Hardware and Software** that control industrial processes, such as **SCADA (Supervisory Control and Data Acquisition)**, **PLCs (Programmable Logic Controllers)**, **DCS (Distributed Control Systems)**, and other equipment used in industries like *manufacturing, energy, transportation, and utilities*.

The goal of an **OT risk assessment** is to ensure the **safety, security, and reliability** of critical systems by identifying **potential vulnerabilities** and **threats** and implementing **measures to mitigate risks**.
 
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
[IEC 62443-3-2](https://github.com/martin199530/Martin/blob/51459e8bc1f018797ff318158473cc7d7e421cfb/ICS-OT-CyberSecurity/IEC%2062443-3-2%20standard.md)

![Image](https://github.com/user-attachments/assets/99d84743-48ec-47ef-928a-49dcde1d5c64)
![Image](https://github.com/user-attachments/assets/5ac1dc05-b1da-4f11-9972-554395bf18ea)
### Asset Inventory
An **Asset Inventory** is a comprehensive record of all **hardware, software, network components**, and **data assets** within an organization. It helps cybersecurity teams **identify**, **manage**, and **protect critical assets** against **cyber threats** and **operational risks**.

![Image](https://github.com/user-attachments/assets/3f06039a-1463-419b-a677-59c1c8b5161c)
### Risk Assessment Matrix
A **Risk Assessment Matrix** is a tool used to **evaluate** and **prioritize risks** based on their likelihood (probability) and impact (severity). It helps organizations make **informed decisions** about **mitigating cybersecurity threats** and **vulnerabilities**. This Tool varies from one organazation to another.

![Image](https://github.com/user-attachments/assets/1d45a6ab-2bb6-4e73-8909-96b2fb212388)

### Scoring
![Image](https://github.com/user-attachments/assets/2190046c-f17b-4324-8b1d-2d5260e049a1)

## Risk assessment
1. Lets assess our first asset: **HMI Station** and find the **Risk** without countermeasure

![Image](https://github.com/user-attachments/assets/daed0121-994a-40d7-821e-372be807018e)

* let's apply **countermeasure** 

![Image](https://github.com/user-attachments/assets/b90c459e-d895-4288-ab94-8abc0093db6a)

* let's apply **Recommendations** 

![Image](https://github.com/user-attachments/assets/98cfbaf9-5575-4983-a7a5-917def7511da)

2. lets complet the entire **Risk Assessment**

![Image](https://github.com/user-attachments/assets/a4c28174-7ae4-433e-a101-8fb1777f8684)

## Next Steps for the Asset Owner:

The **detailed findings** and **recommendations** provided in this assessment equip the asset owner to make an informed decision about the **identified risks**. The following options are available for each risk:

* **Accept the Risk**: For risks deemed acceptable after mitigation.

* **Implement Additional Countermeasures**: For high-priority risks that require further mitigation.

* **Transfer the Risk**: Outsource risk through insurance or third-party agreements.

* **Eliminate the Risk**: Adjust operational strategies to remove high-risk scenarios entirely.
