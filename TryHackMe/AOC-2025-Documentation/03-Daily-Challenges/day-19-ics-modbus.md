# Day 19: ICS / Modbus - Claus for Concern

## 📋 Quick Facts
- **Date Completed:** December 19, 2025
- **Time Spent:** 2 hours
- **Difficulty:** ★★★★ (Hard)
- **Category:** ICS / SCADA / OT Security / Protocol Analysis
- **Room URL:** https://tryhackme.com/room/ICS-modbus-aoc2025-g3m6n9b1v4

---

## 🎯 Challenge Overview

This challenge introduced Industrial Control Systems (ICS) and the Modbus protocol through a Christmas-themed scenario. The environment simulated a SCADA-controlled system where Programmable Logic Controllers (PLCs) manage physical processes (like Santa's factory equipment). Using Python 3 and Modbus communications, the goal was to understand how to read and manipulate PLC data over the network, identify insecure design patterns, and see how attackers can abuse ICS protocols that lack built-in security.

**Learning Objectives:**
- Understand basic ICS/SCADA concepts and components
- Learn what PLCs are and how they relate to field devices
- Understand what Modbus is and why it's still widely used
- See how Modbus messages look and behave over TCP/IP
- Use Python 3 to interact with Modbus (reading/writing registers/coils)
- Recognize why ICS/OT protocols are risky when exposed

---

## 💡 What I Learned

### ICS, SCADA, and PLCs – New Territory

This room covered a domain that is **rarely touched in Security+** and most entry-level material:

**ICS (Industrial Control Systems):**
- Systems that control industrial processes (factories, power plants, pipelines, water treatment, etc.)
- Focused on **safety, reliability, and uptime**, not just confidentiality

**SCADA (Supervisory Control and Data Acquisition):**
- Type of ICS typically used for **large, distributed systems**
- Central SCADA server talks to **remote devices** to monitor and control them
- Example: Monitoring tank levels, opening/closing valves, starting/stopping pumps

**PLCs (Programmable Logic Controllers):**
- Rugged industrial computers that directly control **physical equipment**
- Read inputs (sensors, switches) and drive outputs (motors, relays, valves)
- Execute ladder logic or similar control programs in real time

**Key Point:**
- In IT security, we protect **data and systems**
- In OT/ICS security, we protect **physical processes and safety**

### Modbus – Simple, Old, and Insecure

**What is Modbus?**
- One of the **oldest and most common industrial protocols**
- Originally designed for serial communication (Modbus RTU)
- Now commonly used over TCP/IP (Modbus/TCP)
- Very simple, widely supported by PLCs and SCADA systems

**Basic Modbus Concepts:**
- **Client/Server model** (often called Master/Slave in ICS terms)
- Client (SCADA / HMI / script) sends a **request**
- Server (PLC or device) sends a **response**

**Typical Actions:**
- Read coils (on/off bits)
- Read holding registers (values)
- Write single coil
- Write single register
- Write multiple coils/registers

**Critical Limitation:**
- **No authentication**
- **No encryption**
- **No integrity protection**

If someone can reach the Modbus port (usually TCP 502), they can often:
- Read process values
- Change setpoints
- Turn equipment on/off
- Potentially cause physical damage or safety incidents

### Using Python 3 with Modbus

One of the biggest jumps in this room was using **Python 3 not just to run a script**, but to actively interact with an ICS protocol.

**New Experiences for Me:**
- Importing libraries in Python 3 (e.g., `from pymodbus.client import ModbusTcpClient` or similar)
- Creating a client object and connecting to a target IP/port
- Sending read/write requests to Modbus registers or coils
- Parsing responses in Python (values, status)

**General Flow in Code (Conceptual):**
```python
from pymodbus.client import ModbusTcpClient

client = ModbusTcpClient("MACHINE_IP", port=502)
client.connect()

# Read holding registers
result = client.read_holding_registers(address=0, count=10, unit=1)
print(result.registers)

# Write a single register
client.write_register(address=1, value=123, unit=1)

client.close()
```

**Why This Was Hard:**
- I usually just "run Python scripts" without modifying them
- Here, I had to understand what the script was doing
- Needed to know which function to call to interact with Modbus
- Had to connect ICS concepts (PLCs, registers, coils) with Python code

### Security Implications of ICS/Modbus

This room highlighted why ICS/OT security is **different and dangerous**:

- Modbus has **no built-in security**
- ICS networks historically assumed **trusted, isolated environments**
- Modern connectivity (IT/OT convergence, remote access, cloud) breaks that assumption

**Risks:**
- Unauthenticated writes to PLCs can:
  - Stop production
  - Damage equipment
  - Create unsafe conditions
  - Lead to environmental impact

**Famous Real-World Examples:**
- Stuxnet (targeting Iranian nuclear centrifuges)
- Attacks on power grids and water treatment plants

**Key Takeaway:**
- A simple Python script + open Modbus port = potential to cause REAL physical consequences

---

## 🤔 Challenges I Faced

**Entirely New Domain:**
- SCADA, ICS, PLCs, and Modbus are **not** typically covered deeply in Security+
- First time seeing these concepts in a hands-on way
- Hard to map mental model from traditional IT to OT/ICS

**Python 3 Usage:**
- I’ve only used Python 3 to **run** scripts, not to actively build or modify them
- Understanding imports, client connections, function calls was confusing
- Mapping Modbus functions (read/write registers/coils) to Python methods took effort

**Conceptual Jump:**
- Moving from "web apps and Windows logs" to "industrial protocols controlling physical systems"
- Understanding that a "register" in Modbus corresponds to an actual physical parameter (like temperature, motor speed, valve position)

**Overall:**
- Hard to grasp at first (★★★★ fits)
- But also very interesting because it’s a **rare and high-value niche**

---

## ✅ How This Helps My Career

ICS/OT security is a **high-demand, high-paying specialization** that most people never touch at entry level.

**Why This Room is Valuable:**
- Exposed me to **ICS/SCADA** concepts most junior analysts never see
- Showed how **old, insecure protocols** are still used to control critical infrastructure
- Gave a taste of **Python scripting for protocol interaction**, not just normal scripting

**Career Applications:**

**Blue Team / SOC:**
- Recognize Modbus traffic in PCAPs or logs
- Understand why ICS protocols on flat networks are dangerous
- Escalate incidents involving OT networks appropriately

**Incident Response / Forensics:**
- Investigate suspicious Modbus commands
- Understand potential physical impact
- Work with OT engineers during incidents

**Threat Hunting:**
- Hunt for Modbus traffic crossing boundaries where it shouldn’t
- Look for suspicious writes to PLC registers

**Long-Term Potential:**
- ICS security consultants and OT security engineers are relatively rare
- Niche specialization can lead to higher salaries and unique opportunities

---

## 📚 Key Takeaways for Future Reference

- **ICS/SCADA ≠ regular IT** – priorities are safety and uptime, not just CIA triad
- **PLCs** are the brains controlling physical devices in industrial systems
- **Modbus** is simple but dangerously insecure: no auth, no encryption
- If you can reach Modbus/TCP (port 502), you can often read/write critical process values
- Python can be used to **directly talk to PLCs** via Modbus libraries
- ICS/OT security is a niche but **high-impact** and **high-value** area for a Blue Team career
