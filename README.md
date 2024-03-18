server:
  port: 8080
#eureka:
#  client:
#    serviceUrl:
#      defaultZone: http://localhost:8761/eureka
spring:
  cloud:
    gateway:
      routes:
        - uri: lb://first-service # Load Balancer URI handled by ReactiveLoadBalancerClientFilter
          predicates:
            - Path=/first/**
      loadbalancer:
        configurations: health-check # Required for enabling SDC with health checks
      discovery:
        client:
          simple: # SimpleDiscoveryClient to configure statically services
            instances:
              first-service:
                - secure: false
                  port: 8081
                  host: localhost
#                  instanceId: first-service
                - secure: false
                  port: 8082
                  host: localhost
#                  instanceId: second-service


  main:
    web-application-type: reactive
  application:
    name: API-Gateway
