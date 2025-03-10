```mermaid
sequenceDiagram
    participant client
    box SONiC
        participant GNMI server on GNMI container
        participant SONiC host
    end
    client->>GNMI server on GNMI container: GNMI set request
    GNMI server on GNMI container->>GNMI server on GNMI container: Run GCU commands
    GNMI server on GNMI container->>SONiC host: Invoke SONiC host service with DBUS
    SONiC host->>SONiC host: Restart service if needed
    SONiC host-->>GNMI server on GNMI container: result
    GNMI server on GNMI container->>client: GNMI set response
```
