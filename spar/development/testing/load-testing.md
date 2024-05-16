---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Load Testing

## Setup

K8S Cluster

POD Configurations

DB Specific configurations

Test Server

Test Tool

## Approach

The methodology is detailed for every API

### Resolve API

10 Million Records created

#### Test Script description

Link for the Test Script - github

**Before firing the Test**

Mapper POD - CPU, Memory, CPU Throttling, Load Average - Readings + Charts

DB POD - CPU, Memory, CPU Throttling, Load Average - Readings + Charts



**Test Case**

<mark style="color:purple;">**8 concurrent users, 1000 requests per API, 1 second ramp up time per user**</mark>

**During the Test**

Mapper POD - CPU, Memory, CPU Throttling, Load Average - Readings + Charts

DB POD - CPU, Memory, CPU Throttling, Load Average - Readings + Charts

Locust Statistics - Reading + Charts

<mark style="color:purple;">**< 8 Users, > 1000 Requests per API**</mark>


