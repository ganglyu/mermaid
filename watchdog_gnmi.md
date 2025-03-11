```mermaid
sequenceDiagram
    box SONiC
        participant kubelet
        participant Watchdog
        participant Generic host patch container
        participant GNMI container
        participant SONiC host service
    end
    kubelet->>Watchdog: Health Check Request
    Watchdog->>SONiC host service: Check SONiC host service health
    SONiC host service->>Watchdog: SONiC host service health status
    Watchdog->>GNMI container: Check GNMI service health
    GNMI container->>Watchdog: GNMI service health status
    Watchdog->>kubelet: Health Check Response
    kubelet->>Generic host patch container: If service is not running, roll back generic host patch container
    Generic host patch container ->> SONiC host service: Roll back SONiC host service
    kubelet->>GNMI container: If service is not running, roll back GNMI container
```
