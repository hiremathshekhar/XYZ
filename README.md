graph LR
    subgraph "ABC FMCG Enterprise Network"
        subgraph "IT Network Zone (Corporate)"
            IT_Users[IT Users]
            IT_Servers[IT Servers & Services]
            Corp_Firewall[Corporate Firewall]
        end

        subgraph "DMZ (Demilitarized Zone)"
            Remote_Access_VPN[Remote Access VPN Gateway]
            Patch_Servers[Patch Management Servers]
            AV_Update_Servers[Antivirus Update Servers]
            DMZ_Firewall[DMZ Firewall]
        end

        subgraph "OT/ICS Network Zone (Industrial)"
            OT_Firewall[OT/ICS Firewall]

            subgraph "Level 0/1: Process & Control (Field Level)"
                PLCs[PLCs/Controllers]
                Sensors_Actuators[Sensors & Actuators]
                IO_Modules[I/O Modules]
                Industrial_Network_L01[Industrial Network (e.g., Profinet, Ethernet/IP)]
            end

            subgraph "Level 2: Supervisory Control"
                SCADA_Servers[SCADA/HMI Servers]
                Historian_Servers[Historian Servers]
                Engineering_Workstations[Engineering Workstations]
                Operator_Stations[Operator Stations (HMIs)]
                Industrial_Network_L2[Industrial Network (e.g., Industrial Ethernet)]
            end

            subgraph "Level 3: Manufacturing Operations (Site Level)"
                MES_Servers[MES Servers]
                Asset_Management_Servers[Asset Management Servers]
                OT_Domain_Controllers[OT Domain Controllers (if applicable)]
                Industrial_Network_L3[Industrial Network]
            end
        end

        Internet[Internet]

        IT_Users --> Corp_Firewall
        IT_Servers --> Corp_Firewall
        Corp_Firewall -- "IT Traffic" --> DMZ_Firewall
        DMZ_Firewall --> Remote_Access_VPN
        DMZ_Firewall --> Patch_Servers
        DMZ_Firewall --> AV_Update_Servers
        DMZ_Firewall -- "OT/ICS Management Traffic" --> OT_Firewall
        OT_Firewall --> Industrial_Network_L3
        OT_Firewall --> Industrial_Network_L2
        OT_Firewall --> Industrial_Network_L01
        Industrial_Network_L01 --> PLCs
        Industrial_Network_L01 --> Sensors_Actuators
        Industrial_Network_L01 --> IO_Modules
        Industrial_Network_L2 --> SCADA_Servers
        Industrial_Network_L2 --> Historian_Servers
        Industrial_Network_L2 --> Engineering_Workstations
        Industrial_Network_L2 --> Operator_Stations
        Industrial_Network_L3 --> MES_Servers
        Industrial_Network_L3 --> Asset_Management_Servers
        Industrial_Network_L3 --> OT_Domain_Controllers

        Corp_Firewall -- "Internet Access (Filtered)" --> Internet
        Remote_Access_VPN -- "Secure Remote Access (MFA, PAM)" --> Internet

        style Corp_Firewall fill:#f9f,stroke:#333,stroke-width:2px
        style DMZ_Firewall fill:#f9f,stroke:#333,stroke-width:2px
        style OT_Firewall fill:#f9f,stroke:#333,stroke-width:2px
        style Remote_Access_VPN fill:#ccf,stroke:#333,stroke-width:2px
        style Patch_Servers fill:#ccf,stroke:#333,stroke-width:2px
        style AV_Update_Servers fill:#ccf,stroke:#333,stroke-width:2px
        style SCADA_Servers fill:#cce,stroke:#333,stroke-width:2px
        style Historian_Servers fill:#cce,stroke:#333,stroke-width:2px
        style Engineering_Workstations fill:#cce,stroke:#333,stroke-width:2px
        style Operator_Stations fill:#cce,stroke:#333,stroke-width:2px
        style MES_Servers fill:#cce,stroke:#333,stroke-width:2px
        style Asset_Management_Servers fill:#cce,stroke:#333,stroke-width:2px
        style OT_Domain_Controllers fill:#cce,stroke:#333,stroke-width:2px
        style PLCs fill:#eee,stroke:#333,stroke-width:2px
        style Sensors_Actuators fill:#eee,stroke:#333,stroke-width:2px
        style IO_Modules fill:#eee,stroke:#333,stroke-width:2px
    end
