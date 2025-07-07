# CDR Service Discovery (Eureka Server)

A Netflix Eureka-based service registry that enables service discovery in the CDR microservices architecture. This service allows microservices to register themselves and discover other services without hard-coded hostnames and ports.

## Features

- Service registration and discovery
- Health monitoring of registered services
- High availability configuration support
- Integration with Spring Cloud ecosystem
- Actuator endpoints for monitoring

## Prerequisites

- Java 17 or higher
- Maven 3.6.3 or higher
- Access to Config Server (if using centralized configuration)

## Environment Variables

### Required Configuration

```properties
# Server Configuration
SERVER_PORT=8761

# Spring Application Name
SPRING_APPLICATION_NAME=eurekaserver

# Eureka Server Configuration
EUREKA_CLIENT_REGISTER_WITH_EUREKA=false
EUREKA_CLIENT_FETCH_REGISTRY=false

# Optional: Config Server Integration
SPRING_CLOUD_CONFIG_URI=http://localhost:8071
```

### Optional Configuration

```properties
# Enable self-preservation mode (default: true)
EUREKA_SERVER_ENABLE_SELF_PRESERVATION=true

# Eviction timer interval in milliseconds (default: 60000)
EUREKA_SERVER_EVICTION_INTERVAL_TIMER_IN_MS=60000

# Response cache update interval in milliseconds (default: 30000)
EUREKA_SERVER_RESPONSE_CACHE_UPDATE_INTERVAL_MS=30000

# Enable/disable the Eureka server's web interface (default: true)
EUREKA_DASHBOARD_ENABLED=true
```

## Getting Started

1. **Build the application**
   ```bash
   mvn clean install
   ```

2. **Run the application**
   ```bash
   java -jar target/service-discovery-1.0.0.jar
   ```
   Or using Maven:
   ```bash
   mvn spring-boot:run
   ```

3. **Access the Eureka Dashboard**
   Open a web browser and navigate to:
   ```
   http://localhost:8761/
   ```

## High Availability Setup

For production environments, it's recommended to run multiple instances of the Eureka Server for high availability:

1. **First instance** (peer1):
   ```properties
   SPRING_APPLICATION_NAME=eurekaserver
   SERVER_PORT=8761
   EUREKA_CLIENT_SERVICE_URL_DEFAULTZONE=http://peer2:8762/eureka/
   ```

2. **Second instance** (peer2):
   ```properties
   SPRING_APPLICATION_NAME=eurekaserver
   SERVER_PORT=8762
   EUREKA_CLIENT_SERVICE_URL_DEFAULTZONE=http://peer1:8761/eureka/
   ```

## Monitoring

The service exposes the following monitoring endpoints:

- Health: `GET /actuator/health`
- Info: `GET /actuator/info`
- Metrics: `GET /actuator/metrics`
- Service Registry: `GET /eureka/apps`

## Security Considerations

- In production, secure the Eureka Server with authentication
- Use HTTPS for all communications
- Configure appropriate firewall rules to limit access to the Eureka Server
- Consider using Spring Security to protect the Eureka dashboard

## Dependencies

- Spring Cloud Netflix Eureka Server
- Spring Boot Actuator
- Spring Cloud Config Client (for centralized configuration)
- Spring Security (optional, for securing the dashboard)

## License

[Specify your license here]

## Contact

[Your contact information]
