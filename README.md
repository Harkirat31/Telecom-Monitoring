# Telecom-Monitoring
            +------------------+
            | SNMP Simulator   |  <-- Simulated devices (e.g., OLT, ONU)
            | (e.g., snmpsim)  |
            +--------+---------+
                     |
                     | SNMP polling
                     ↓
            +------------------+
            | Python Poller    |  <-- Extracts & parses SNMP data
            | (e.g., poller.py)|      using pysnmp
            +--------+---------+
                     |
                     | Pushes JSON
                     ↓
            +------------------+
            | Kafka Topic      |  <-- Buffers parsed SNMP data
            | "snmp_data"      |
            +--------+---------+
                     |
                     | Kafka Consumer
                     ↓
            +------------------------+
            | Spring Boot Service    |  <-- Consumes Kafka data
            | + Saves to DB (Postgres)
            | + Exposes REST APIs
            +-----------+------------+
                        |
                        | REST APIs
                        ↓
         +------------------------+
         | Web App (React)        |
         | or Mobile App (Flutter)|
         +------------------------+
