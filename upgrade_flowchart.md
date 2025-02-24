```mermaid
graph LR
    classDef process fill:#E5F6FF,stroke:#73A6FF,stroke-width:2px;
    classDef decision fill:#FFF6CC,stroke:#FFBC52,stroke-width:2px;
    RolloutGeneric[Roll out patch container v1<br><div style="margin-left:0px;border:2px dashed black;padding:0px;text-align:left;">Upgrade GCU<br>Upgrade sonic yang mgmt<br>Upgrade sonic yang models</div>Roll out gnmi container v1]
    RollbackGeneric[Roll out patch container v2<br><div style="margin-left:0px;border:2px dashed black;padding:0px;text-align:left;">Revert GCU<br>Revert sonic yang mgmt<br>Revert sonic yang models</div>Roll out gnmi container v2]
    subgraph Watchdog
        WatchdogGCU{Run yang validation}
        WatchdogGNMI{Check GNMI/GNOI service}
    end
    Start(Start) --> RolloutGeneric:::process
    RolloutGeneric --> WatchdogGCU:::decision
    WatchdogGCU --> |passed|WatchdogGNMI:::decision
    WatchdogGCU --> |failed|RollbackGeneric:::process
    WatchdogGNMI --> |GNMI/GNOI service<br>works well|End(End)
    WatchdogGNMI --> |GNMI/GNOI service<br>does not work|RollbackGeneric:::process
    RollbackGeneric --> End
```
