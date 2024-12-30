


```mermaid
graph TD
    subgraph Main Application
        START[Start Application] --> PARSE[Parse Arguments]
        PARSE --> LOAD[Load Characters]
        LOAD --> INIT[Initialize System]
    end

    subgraph Character Configuration
        LOAD --> |Read| CONFIG[Character Config]
        CONFIG --> |Validate| VALID[Validate Character]
        CONFIG --> |Extract| SETTINGS[Settings & Secrets]
        CONFIG --> |Define| CLIENTS[Client Types]
        CONFIG --> |Load| PLUGINS[Plugins]
    end

    subgraph Database Layer
        INIT --> |Initialize| DB{Database Type}
        DB --> |Option 1| POSTGRES[PostgreSQL Adapter]
        DB --> |Option 2| SQLITE[SQLite Adapter]
        POSTGRES --> DBINIT[Database Initialization]
        SQLITE --> DBINIT
    end

    subgraph Cache System
        DBINIT --> CACHE{Cache Type}
        CACHE --> |Option 1| FSCACHE[FileSystem Cache]
        CACHE --> |Option 2| DBCACHE[Database Cache]
        FSCACHE --> CACHEMGR[Cache Manager]
        DBCACHE --> CACHEMGR
    end

    subgraph Agent Runtime
        CACHEMGR --> RUNTIME[Create Agent Runtime]
        RUNTIME --> |Configure| MODEL[Model Provider]
        RUNTIME --> |Load| RTPLUGINS[Runtime Plugins]
        RUNTIME --> |Setup| EVALUATORS[Evaluators]
        RUNTIME --> |Initialize| SERVICES[Services]
    end

    subgraph Client Interfaces
        RUNTIME --> CLIENTINIT[Initialize Clients]
        CLIENTINIT --> AUTO[Auto Client]
        CLIENTINIT --> DISCORD[Discord Client]
        CLIENTINIT --> TELEGRAM[Telegram Client]
        CLIENTINIT --> TWITTER[Twitter Client]
        CLIENTINIT --> DIRECT[Direct Client]
    end

    subgraph Message Flow
        USER[User Input] --> |Send| INTERFACE[Client Interface]
        INTERFACE --> |Process| RUNTIME
        RUNTIME --> |Generate| RESPONSE[Response]
        RESPONSE --> |Return| INTERFACE
        INTERFACE --> |Display| OUTPUT[User Output]
    end

    subgraph Plugin System
        RTPLUGINS --> BOOTSTRAP[Bootstrap Plugin]
        RTPLUGINS --> NODE[Node Plugin]
        RTPLUGINS --> SOLANA[Solana Plugin]
        BOOTSTRAP --> |Extend| RUNTIME
        NODE --> |Extend| RUNTIME
        SOLANA --> |Extend| RUNTIME
    end

    subgraph Error Handling
        ERROR[Error Handler] --> |Log| LOGGER[Logger]
        ERROR --> |Notify| INTERFACE
        ERROR --> |Recover| RUNTIME
    end

    %% Relationships
    RUNTIME --> ERROR
    CLIENTINIT --> ERROR
    DB --> ERROR
    CACHE --> ERROR
    
    ```