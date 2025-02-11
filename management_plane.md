flowchart TD
    subgraph UserSpace
        direction TB
        subgraph Apps
            A[teamd]
            B[teamsynd]
            C[bgpd]
            D[fpmsynd]
            E[lldpd]
            F[lldpsynd]
            G[dhcrelay]
            H[Other Apps]
        end
        subgraph Orch
            I[Orchangent]
            J[SWSS]
        end
        subgraph RedisDB
            K[Redis]
        end
        subgraph SyncComp
            L[Synd]
            M[SDK]
            N[SAI]
        end
        subgraph CLITools
            O[CLI]
            P[Sonic - cfggen]
        end
        A --> K
        B --> K
        C --> K
        D --> K
        E --> K
        F --> K
        G --> K
        H --> K
        I --> K
        J --> K
        K --> L
        K --> M
        K --> N
        L --> N
        M --> N
        K --> O
        K --> P
    end
    subgraph KernelSpace
        Q[Linux]
        R[Switch Abstraction Interface]
        Q --> R
    end
    UserSpace --> KernelSpace
