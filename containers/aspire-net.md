# Aspire
Building observable, production-ready distributed apps
Key capabilities: orchestration (local development), integrations, consistent tooling  

**NB** A replacement for Docker Compose when developing. instead of markup, code


## The Starter Projects  

| Project | Type | Depends On | Notes |
| --- | --- | --- | --- |
| Api | backend | ServiceDefaults | 
| Web | frontend | ServiceDefaults | 
| ServiceDefaults | Base project | | Shared project to manage connections that are reused - discovery, telemetry | 
| AppHost | Orchestrator | Api & Web | Startup project | 

## App Host  
The program configures how the *Orchestration* works. Health dependencies between front and backend.


## Segways
Redis - distributed cache